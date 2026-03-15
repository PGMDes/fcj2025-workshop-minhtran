---
title: "Blog 3"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# **Geospatial Data Lake with Amazon Redshift**

*By Jeremy Spell and Jeff DeMuth | July 10, 2025 | Related to [Amazon Redshift](https://aws.amazon.com/blogs/big-data/category/analytics/amazon-redshift-analytics/), [AWS Glue](https://aws.amazon.com/blogs/big-data/category/analytics/aws-glue/), [AWS Lake Formation](https://aws.amazon.com/blogs/big-data/category/analytics/aws-lake-formation/), [Technical How-to](https://aws.amazon.com/blogs/big-data/category/post-types/technical-how-to/)*

Data lake architecture helps organizations move data away from expensive storage systems while maintaining query and analysis capabilities. This approach is useful for geospatial data, where builders can have terabytes of infrequently accessed data in databases that need to maintain cost efficiency. However, this requires data lake query tools that support data types and functions of geographic information systems (GIS).

[Amazon Redshift](https://aws.amazon.com/redshift/) supports [geospatial data](https://docs.aws.amazon.com/redshift/latest/dg/geospatial-overview.html) queries, including GEOMETRY and GEOGRAPHY types and functions used in GIS system queries. Additionally, Amazon Redshift allows you to query geospatial data both in data lakes on Amazon S3 and in Redshift data warehouses, giving you flexibility in data access methods. Moreover, [AWS Lake Formation](https://aws.amazon.com/lake-formation/) and [AWS Identity and Access Management](https://aws.amazon.com/iam/) (IAM) support in Esri's [ArcGIS Pro](https://www.esri.com/en-us/arcgis/products/arcgis-pro/overview) provide a secure way to connect between geospatial data lakes and map visualization tools. You can set up, manage, and secure geospatial data lakes in the cloud with just a few clicks.

In this article, we guide you through setting up a geospatial data lake using Lake Formation and querying data with ArcGIS Pro via [Amazon Redshift Serverless](https://aws.amazon.com/redshift/redshift-serverless/).

## **Solution Overview**

In the example, a county health department uses Lake Formation to protect a data lake containing Protected Health Information (PHI) data. Epidemiologists want to create maps of clinics that provide vaccinations to the community. The county's GIS analysts need data lake access to create required maps but should not be allowed to access PHI data.

The solution uses Lake Formation tags to enable column-level access permissions in the database for public information including clinic name, address, zip code, and latitude/longitude coordinates, while denying access to PHI data in the same table. We use Redshift Serverless and [Amazon Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-getting-started-using-spectrum.html) to access this data from ArcGIS Pro, Esri's GIS mapping software, an AWS partner.

![image1](/images/3-BlogsTranslated/16.png)

Below is the sample schema for this article.

| Description | Column Name | Geoproperty Tag |
| :---- | :---- | :---- |
| Patient ID | patient_id | No |
| Clinic ID | clinic_id | Yes |
| Clinic Address | clinic_address | Yes |
| Clinic ZIP Code | clinic_zip | Yes |
| Clinic City | clinic_city | Yes |
| Patient First Name | first_name | No |
| Patient Last Name | last_name | No |
| Patient Address | patient_address | No |
| Patient ZIP Code | patient_zip | No |
| Vaccination Type | vaccination_type | No |
| Clinic Latitude | clinic_lat | Yes |
| Clinic Longitude | clinic_long | Yes |

Solution setup steps:

1. Deploy infrastructure using [AWS CloudFormation](http://aws.amazon.com/cloudformation).
2. Upload a CSV with sample data to an [Amazon S3](http://aws.amazon.com/s3) bucket and run an [AWS Glue](https://aws.amazon.com/glue) crawler to discover data.
3. Set up Lake Formation permissions.
4. Configure Amazon Redshift Query Editor v2.
5. Set up schema in Amazon Redshift.
6. Create a view in Amazon Redshift.
7. Create a local database user in ArcGIS Pro.
8. Connect ArcGIS Pro with Redshift database.

## **Prerequisites**

You need:

* AWS Account
* [Lake Formation enabled in target AWS Region](https://docs.aws.amazon.com/lake-formation/latest/dg/initial-lf-config.html)
* Understanding of Lake Formation and table permission setup
* [ArcGIS Pro](https://pro.arcgis.com/en/pro-app/latest/get-started/install-and-sign-in-to-arcgis-pro.htm)
* Network connectivity from ArcGIS Pro client to VPC where Amazon Redshift resources are deployed via [VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html) or [AWS Direct Connect](https://aws.amazon.com/directconnect/)

## **Set Up Infrastructure with AWS CloudFormation**

To create the demo environment, follow these steps:

* Sign in to the [AWS Management Console](http://aws.amazon.com/console) with an AWS administrator account and Lake Formation data lake administrator account—this account needs to be both account admin and data lake admin for the template to complete.
* Open the AWS CloudFormation console
* Select [Launch Stack](https://us-east-1.console.aws.amazon.com/cloudformation/home?region=us-east-1#/stacks/create?stackName=geo-sample&templateURL=https://aws-blogs-artifacts-public.s3.amazonaws.com/BDB-3975/infra_setup.yml).

The CloudFormation template creates the following components:

* S3 bucket – `samp-clinic-db-{ACCOUNT\_ID}`
* AWS Glue database – `samp-clinical-glue-db`
* AWS Glue crawler – `samp-glue-crawler`
* Redshift Serverless workgroup – `samp-clinical-rs-wg`
* Redshift Serverless namespace – `samp-clinical-rs-ns`
* IAM role for Amazon Redshift – `demo-RedshiftIAMRole-{UNIQUE\_ID}`
* IAM role for AWS Glue – `samp-clinical-glue-role`
* Lake Formation tag – `geoproperty`

## **Upload CSV to S3 and Run AWS Glue Crawler**

Next, create a data lake in the demo environment, then use AWS Glue crawler to populate the AWS Glue database and update schema and metadata in the AWS Glue Data Catalog.

The CloudFormation stack already created S3 bucket, AWS Glue database, and crawler. We provide a fictional sample dataset representing patient and clinic information. Download the file and follow these steps:

1. On the AWS CloudFormation console, open the stack you just launched.
2. On the Resources tab, select the link to the S3 bucket.
3. Select Upload and upload the CSV file (data-with-geocode.csv), then select Upload.
4. On the AWS Glue console, select Crawlers in the navigation.
5. Select the crawler you created with the stack and click Run.
   The crawler runs for about one minute and populates a table named `clinic-sample-s3\_ACCOUNT\_ID` with sample data.
6. Select Tables in the navigation and open the table created by the crawler.

You'll see the dataset contains PHI and personally identifiable information (PII) fields.

![image2](/images/3-BlogsTranslated/17.png)

Now we have a database and Data Catalog populated with schema and metadata for the rest of the process.

## **Set Up Lake Formation Permissions**

Next, we demonstrate how to protect PHI data for compliance while still supporting GIS analysts to work effectively. To protect the data lake, use AWS Lake Formation. To set up Lake Formation permissions correctly, you need to understand how data lake access is configured.

The Data Catalog provides metadata and schema that allow services to access data in the lake. To access the data lake from ArcGIS Pro, use the [ArcGIS Pro Redshift](https://pro.arcgis.com/en/pro-app/latest/help/data/databases/connect-redshift.htm) connector, which allows connections from ArcGIS Pro to Amazon Redshift. Amazon Redshift can access the Data Catalog and provide connections to the data lake. The CloudFormation template already created a Redshift Serverless instance and namespace with an IAM role to configure this connection. We still need to set up Lake Formation permissions so GIS analysts only access public fields, not fields containing PHI or PII. We'll assign Lake Formation tags to columns containing public information and assign permissions to GIS analysts to access columns with these tags.

By default, Lake Formation is configured with Super access to `IAMAllowedPrinciples`; this is for backward compatibility as noted in [changing default settings for data lake](https://docs.aws.amazon.com/lake-formation/latest/dg/change-settings.html). To demonstrate more secure configuration, we'll remove this default setting.

1. On the Lake Formation console, select **Administration** in the navigation.
2. Under **Data Catalog settings**, ensure **Use only IAM access control for new databases** and **Use only IAM access control for new tables in new databases** are not selected.
   ![image3](/images/3-BlogsTranslated/18.png)
3. In the navigation, under **Permissions**, select **Data permissions**.
4. Select `IAMAllowedPrincipals` and click Revoke.
5. Select **Tables** in the navigation.
6. Open table `clinic-sample-s3\_ACCOUNT\_ID` and select **Edit schema**.
7. Select fields starting with clinic\_ and select **Edit LF-Tags**.
8. The CloudFormation stack created a Lake Formation tag named `geoproperty`. Assign `geoproperty` as key and true as value for all `clinic_` fields, then select **Save**.
   Next, grant permissions to the Amazon Redshift IAM role to access fields tagged with `geoproperty = true`.
9. Select **Data lake permissions**, then select **Grant**.
10. For IAM role, select `demo-RedshiftIAMRole-UNIQUE_ID`.
11. Select `geoproperty` for key and true for value.
12. In **Database permissions**, select **Describe**, and in **Table permissions**, select **Select** and **Describe**.

## **Configure Amazon Redshift Query Editor v2**

Next, configure the initial Amazon Redshift setup necessary for database operations. We use an [AWS Secrets Manager](https://aws.amazon.com/secrets-manager/) secret created by the template to manage passwords securely following AWS best practices.

1. On the Amazon Redshift console, select **Query editor v2**.
2. On first launch, Amazon Redshift will show one-time configuration for the account. For this article, keep defaults and select **Configure account**.

See additional options at [Configuring your AWS account](https://docs.aws.amazon.com/redshift/latest/mgmt/query-editor-v2-getting-started.html).

![image4](/images/3-BlogsTranslated/19.png)

The query editor needs credentials to connect to the serverless instance; this information was created by the template and stored in Secrets Manager.

3. Select **Other ways to connect**, then select **AWS Secrets Manager**.
4. Under **Secret**, select (`Redshift-admin-credentials`).
5. Select **Save**.
   ![image5](/images/3-BlogsTranslated/20.png)

## **Set Up Schema in Amazon Redshift**

External schema in Amazon Redshift is a feature that references schema existing at external data sources. See [External schemas in Amazon Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-spectrum-external-schemas.html) for creating external schema. We use external schema to provide access to the data lake within Amazon Redshift. From ArcGIS Pro, we'll connect to Amazon Redshift to access geospatial data.

The IAM role used when creating external schema must be associated with the Redshift namespace. The template already set this up, but you should verify before proceeding.

1. In the Redshift Serverless console, select **Namespace configuration** in the navigation pane.
2. Select namespace (`sample-rs-namespace`).
   ![image6](/images/3-BlogsTranslated/21.png)
   On the **Security and encryption** tab, you'll see the IAM role created by CloudFormation. If the role or namespace doesn't exist, check the stack in AWS CloudFormation before proceeding.
3. Copy the ARN of the role for later use.
   ![image7](/images/3-BlogsTranslated/22.png)
4. Select **Query data** to return to the query editor.

![image8](/images/3-BlogsTranslated/23.png)

5. In the query editor, enter the following SQL command; remember to replace the example ARN with yours. This SQL command creates an external schema using the same Redshift role attached to the namespace to link to the AWS Glue database.

```
CREATE EXTERNAL SCHEMA samp_clinic_sch_ext FROM DATA CATALOG
database 'sample-glue-database'
IAM_ROLE 'arn:aws:iam::{ACCOUNT_ID}:role/demo-RedshiftIAMRole-{UNIQUE_ID}';
```

6. In the query editor, execute a select query on `sample-glue-database`
   ```
   SELECT * FROM "dev"."samp_clinic_sch_ext"."clinic-sample_s3_{ACCOUNT_ID}";
   ```
   Because the associated role has been granted access to columns tagged with `geoproperty = true`, only these fields will be returned, as shown in the following image (sample data is fictional).
   ![image9](/images/3-BlogsTranslated/24.png)

7. Use the following command to create a local schema in Amazon Redshift. External schema cannot be updated; we'll use local schema to add geometry fields using Redshift functions.
   ```
   CREATE SCHEMA samp_clinic_sch_local
   ```

## **Create a View in Amazon Redshift**

For data to display from ArcGIS Pro, we need to create a view. After schema setup, we create a view that can be accessed from ArcGIS Pro.

Amazon Redshift provides many [geospatial functions](https://docs.aws.amazon.com/redshift/latest/dg/geospatial-functions.html) used to create views with fields that ArcGIS Pro uses to add points to maps. We'll use one function since the dataset has latitude and longitude.

Use the following SQL command in Amazon Redshift Query Editor to create a view named `clinic_location_view`. Replace `{ACCOUNT_ID}` with your account ID.

```
CREATE OR REPLACE VIEW "samp_clinic_sch_local"."clinic_location_view" AS
SELECT
    clinic_id as id,
    clinic_lat as lat,
    clinic_long as long,
    ST_MAKEPOINT(long, lat) as geom
FROM
    "dev"."samp_clinic_sch_ext"."clinic-sample_s3_{ACCOUNT_ID}"
WITH NO SCHEMA BINDING;
```

The new view in the local schema will have a geom column containing map points used by ArcGIS Pro to add points when creating maps. The points in this example are clinic locations providing vaccinations. In practice, when new clinics are built and new data is added to the data lake, their locations will appear on maps using this data.

## **Create Local Database User for ArcGIS Pro**

In the demo, we use a database user and group to grant permissions to the ArcGIS Pro client. Enter the following SQL in Amazon Redshift Query Editor to create the user and group:

```
CREATE USER dbuser with PASSWORD 'SET_PASSWORD_HERE';
CREATE GROUP esri_developer_group;
ALTER GROUP esri_developer_group ADD USER dbuser;
```

After running this, use the following commands to grant permissions to the group:

```
GRANT USAGE ON SCHEMA samp_clinic_sch_local TO GROUP esri_developer_group;
ALTER DEFAULT PRIVILEGES IN SCHEMA samp_clinic_sch_local GRANT SELECT ON TABLES TO GROUP esri_developer_group;
GRANT SELECT ON ALL TABLES IN SCHEMA samp_clinic_sch_local TO GROUP esri_developer_group;
```

## **Connect ArcGIS Pro with Redshift Database**

To add database connections to ArcGIS Pro, you need the endpoint for your Redshift Serverless workgroup. You can view endpoint information on the detail page of workgroup `sample-rs-wg` on the Redshift Serverless console. The Redshift namespace and workgroup are listed by default, as shown in the image below.

![image10](/images/3-BlogsTranslated/25.png)

You can copy the endpoint in the **General information** section. This endpoint needs to be modified; the `:5439/dev` portion needs to be removed when configuring the connector in ArcGIS Pro.

![image11](/images/3-BlogsTranslated/26.png)

1. Open ArcGIS Pro with the project where you want to add the Redshift connection.

| Ensure you've installed the [Amazon Redshift ODBC connector](https://docs.aws.amazon.com/redshift/latest/mgmt/odbc20-install-config-win.html); this is required to connect. |
| :---- |

2. On the menu, select **Insert** then **Connections**, **Database**, and **New Database Connection**.
3. Under **Database Platform**, select **Amazon Redshift**.
4. Under **Server**, paste the copied endpoint (remove everything after .com from the endpoint).
5. Under **Database**, select your database.
   ![image12](/images/3-BlogsTranslated/27.png)

If your ArcGIS Pro client cannot access the endpoint, you'll get an error at this step. A network path must exist between the ArcGIS Pro client and the Redshift Serverless endpoint. You can establish the network path with [Direct Connect](https://docs.aws.amazon.com/whitepapers/latest/aws-vpc-connectivity-options/aws-direct-connect.html), [AWS Site-to-Site VPN](https://docs.aws.amazon.com/vpn/latest/s2svpn/VPC_VPN.html), or [AWS Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html). While not recommended for security reasons, you can also [configure a public endpoint](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-console-workgroups.html#serverless-workgroup-describe) for Amazon Redshift. Consult your network security team for best practices before allowing public access to Redshift Serverless.

If you have network connectivity but still get connection errors, check the security group to allow inbound from the ArcGIS Pro subnet over the port Redshift Serverless uses. The default is 5439, but port ranges can be configured depending on your environment; see [Connecting to Amazon Redshift Serverless](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-connecting.html) for more information.

If the connection is successful, ArcGIS Pro will add the Amazon Redshift connection under **Connection File Name**.

1. Select **OK**.
2. Select the connection to display the created view with geometry (`clinic_location_view`).
3. Right-click the view and select **Add To Current Map**.

ArcGIS Pro will add the points from the view to the map. The final map was edited to use red crosshair symbols representing clinics instead of circles.

![image13](/images/3-BlogsTranslated/28.png)

## **Clean Up Resources**

After completing the demo, follow these steps:

1. In the Amazon S3 console, open the bucket created by the CloudFormation stack and delete the `data-with-geocode.csv` file.
2. In the AWS CloudFormation console, delete the demo stack to remove created resources.

## **Conclusion**

This article has guided you through setting up Redshift Serverless to use geospatial data in your data lake to enhance maps in ArcGIS Pro. This technique helps builders and GIS analysts leverage existing datasets in the data lake and transform them in Amazon Redshift to enrich data before presenting it on maps. We also showed how to protect your data lake using Lake Formation, discover geospatial datasets with AWS Glue, and visualize data in ArcGIS Pro.

For more best practices on storing geospatial data in Amazon S3 and querying with Amazon Redshift, see [How to partition your geospatial data lake for analysis with Amazon Redshift](https://aws.amazon.com/blogs/publicsector/how-partition-geospatial-data-lake-analysis-amazon-redshift/). We welcome your feedback in the comments section.

## **About the Authors**

![image14](/images/3-BlogsTranslated/29.jpg) **Jeremy Spell** is a cloud infrastructure architect working at AWS Professional Services. He enjoys designing and building solutions for customers. In his spare time, Jeremy enjoys making Texas-style BBQ and spending time with family and church community.

![image15](/images/3-BlogsTranslated/30.jpg) **Jeff Demuth** is a solutions architect who joined AWS in 2016. He focuses on the geospatial community and is passionate about Geographic Information Systems (GIS) and technology. Outside of work, Jeff enjoys traveling, building IoT applications, and tinkering with new gadgets.
