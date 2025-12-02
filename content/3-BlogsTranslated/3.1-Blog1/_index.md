---
title: "Blog 1"
date: "2025-09-09"
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
---
# New capabilities in Amazon SageMaker AI continue to transform how organizations develop AI models

*By Ankur Mehrotra | July 10, 2025 | related: [Amazon Bedrock](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/amazon-machine-learning/amazon-bedrock/), [Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-ai/), [Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-hyperpod/), [Amazon SageMaker JumpStart](https://aws.amazon.com/blogs/machine-learning/category/artificial-intelligence/sagemaker/amazon-sagemaker-jumpstart/), [Announcements](https://aws.amazon.com/blogs/machine-learning/category/post-types/announcements/)*

As AI models become more complex and specialized, the ability to train and customize models quickly can mean the difference between leading and falling behind. That’s why hundreds of thousands of customers worldwide rely on [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/) — a platform that provides robust infrastructure, comprehensive tools, and managed workflows to scale and accelerate model development. Since its 2017 launch, SageMaker AI has reshaped how organizations build models by reducing complexity and optimizing performance and scalability. AWS continues to innovate — adding over 420 features since launch — delivering advanced tools to build, train, and deploy AI models faster, more flexibly, and efficiently. Today we introduce the latest SageMaker AI enhancements designed to speed up model development and training, helping organizations shorten innovation cycles and unlock AI’s potential.

## **Amazon SageMaker HyperPod: Infrastructure built for large-scale model development**

AWS launched [Amazon SageMaker HyperPod](https://aws.amazon.com/sagemaker/ai/hyperpod/) in 2023 to reduce complexity and maximize performance and efficiency when building AI models. HyperPod lets you scale generative AI development across thousands of accelerators, cutting training and fine-tuning costs for foundation models (FMs) by up to ~40%. Many leading models today are trained on HyperPod, including models from Hugging Face, Luma AI, Perplexity AI, Salesforce, Thomson Reuters, Writer, and Amazon. Training Amazon’s Nova FMs on HyperPod saved months of work and increased compute utilization above 90%.

*[Amazon Trains Nova Foundation Models at Scale with SageMaker HyperPod | Amazon Web Services](https://youtu.be/aS1EU_kkGcI)*

To streamline workflows and accelerate model development and deployment, a new unified CLI and SDK provide a consistent interface that simplifies infrastructure management, unifies job submission for training and inference, and supports both recipe-driven and custom workflows with integrated monitoring and control. Today we’re adding two HyperPod capabilities to further reduce training cost and speed model development.

## **Cut troubleshooting time from days to minutes with HyperPod observability**

To rapidly bring AI innovations to market, teams need end-to-end observability over model development jobs and compute resources to optimize training performance and detect and fix bottlenecks early. For example, when investigating whether a training or fine-tuning job failed due to hardware, data scientists and ML engineers want to quickly filter and view metrics for the specific GPUs that ran the job, rather than manually scanning cluster hardware to correlate job failures with hardware faults.

[One-click observability in SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/accelerate-foundation-model-development-with-one-click-observability-in-amazon-sagemaker-hyperpod/) changes how you monitor and optimize model workloads. Through a preconfigured unified dashboard in [Amazon Managed Grafana](https://aws.amazon.com/grafana/) with metrics automatically sent to an [Amazon Managed Service for Prometheus](https://aws.amazon.com/prometheus/) workspace, you can view generative AI job performance, resource utilization, and cluster health in a single pane. Teams can quickly spot bottlenecks, prevent costly delays, and optimize compute. You can define automatic alerts, select metrics and events per use case, and surface them in the unified dashboard with a few clicks.

By cutting mean time to resolution from days to minutes, this capability speeds production timelines and maximizes ROI on AI investments.

![image1](/images/3-BlogsTranslated/01.jpg)

DatologyAI builds tools to automatically select the best data for training deep learning models.

“We’re excited to use HyperPod’s one-click observability. Our execs need deep visibility into GPU usage. The prebuilt Grafana dashboards give exactly what we need — immediate metrics from per-job GPU usage to FSx for Lustre performance — without operating monitoring infrastructure. As a fan of Prometheus Query Language, I like being able to write queries and analyze custom metrics without worrying about the underlying infra.”  
— Josh Wills, Engineering Team, DatologyAI

![image2](/images/3-BlogsTranslated/02.jpg)

Articul8 helps enterprises build sophisticated generative AI applications.

“With HyperPod observability, we can deploy data collection and visualization in one click, saving days of manual setup and improving cluster insights. Data scientists can quickly monitor task performance metrics like latency and identify hardware issues without manual configuration. HyperPod observability streamlines foundation model development so we can focus on delivering reliable, accessible AI innovation to customers.”  
— Renato Nascimento, CTO, Articul8

## **Deploy SageMaker JumpStart models on HyperPod for fast, scalable inference**

After developing generative models on HyperPod, many customers import them into [Amazon Bedrock](https://aws.amazon.com/bedrock/), a fully managed service for building and scaling generative AI applications. Some customers prefer to use HyperPod compute to speed evaluation and productionization.

You can now [deploy open-weight models](https://aws.amazon.com/blogs/machine-learning/amazon-sagemaker-hyperpod-launches-model-deployments-to-accelerate-the-generative-ai-model-development-lifecycle/) from Amazon SageMaker JumpStart, as well as customized fine-tuned models, on HyperPod within minutes without manual infra setup. Data scientists can run inference on JumpStart models with one click, simplifying and accelerating model evaluation. The one-shot provisioning reduces manual setup, delivering reliable, scalable inference with minimal effort. Large model download times shrink from hours to minutes, speeding deployment and time to market.

![image3](/images/3-BlogsTranslated/03.jpg)

H.AI exists to push the limits of ultra-intelligent, task-oriented AI.

“With HyperPod, we use high-performance compute to build and deploy the foundation models behind our agentic AI platform. Seamless transition from training to inference has streamlined our workflow, shortened time to production, and delivered stable performance in real environments. HyperPod helps us move from experimentation to real impact faster and more efficiently.”  
— Laurent Sifre, Co-founder & CTO, H.AI

## **Seamless access to SageMaker AI compute from local development environments**

Many customers use fully managed IDEs in SageMaker AI (JupyterLab, Code Editor based on Code-OSS, and RStudio) for model development. While these managed IDEs provide secure, efficient setups, some developers prefer local IDEs for deeper debugging and customization. Previously, local IDE users like Visual Studio Code couldn’t easily run model development tasks on SageMaker AI.

With [new remote connections to SageMaker AI](https://aws.amazon.com/blogs/machine-learning/supercharge-your-ai-workflows-by-connecting-to-sagemaker-studio-from-visual-studio-code), developers and data scientists can smoothly connect to SageMaker AI from local VS Code, keeping custom tools and familiar workflows while offloading execution to SageMaker AI. Developers can build and train models in their preferred IDE while SageMaker AI manages remote execution, giving them the benefits of SageMaker performance, scalability, and security. Now you can choose the IDE you prefer — managed cloud IDE or VS Code — to accelerate model development using SageMaker AI’s scalable compute and seamless integrations.

![image4](/images/3-BlogsTranslated/04.jpg)

CyberArk leads in Identity Security, offering a holistic approach centered on privileged access control.

“With SageMaker AI remote connections, our data scientists have the flexibility to choose the IDE that makes them most productive. Teams can leverage custom local setups while accessing SageMaker AI’s infrastructure and security controls. For a security-first company, that’s crucial: it ensures sensitive data stays protected while enabling secure collaboration and higher productivity.”  
— Nir Feldman, Senior Vice President of Engineering, CyberArk

## **Build models and generative AI applications faster with fully managed MLflow 3.0**

As customers across industries accelerate generative AI development, they need experiment tracking, behavior observability, and model/application performance evaluation. Customers like Cisco, SonRai, and Xometry use managed MLflow on SageMaker AI to manage ML experiments at scale. Introducing fully managed MLflow 3.0 on SageMaker AI enables experiment tracking, training monitoring, and deeper insights into model and application behavior within a single managed tool, helping accelerate generative AI development.

## **Conclusion**

This post shared several SageMaker AI innovations to speed how you build and train AI models.

To learn more about the new features, SageMaker AI, and customer use cases, see these resources:

* [Accelerate foundation model development with one-click observability in Amazon SageMaker HyperPod](https://aws.amazon.com/blogs/machine-learning/accelerate-foundation-model-development-with-one-click-observability-in-amazon-sagemaker-hyperpod)  
* [Supercharge your AI workflows by connecting to SageMaker Studio from Visual Studio Code](https://aws.amazon.com/blogs/machine-learning/supercharge-your-ai-workflows-by-connecting-to-sagemaker-studio-from-visual-studio-code)  
* [Accelerating generative AI development with fully managed MLflow 3.0 on Amazon SageMaker AI](https://aws.amazon.com/blogs/machine-learning/accelerating-generative-ai-development-with-fully-managed-mlflow-3-0-on-amazon-sagemaker-ai/)  
* [Amazon SageMaker HyperPod launches model deployments to accelerate the generative AI model development lifecycle](https://aws.amazon.com/blogs/machine-learning/amazon-sagemaker-hyperpod-launches-model-deployments-to-accelerate-the-generative-ai-model-development-lifecycle/)  
* [Amazon SageMaker AI](https://aws.amazon.com/sagemaker-ai/)  
* [Amazon SageMaker AI customers](https://aws.amazon.com/sagemaker-ai/customers/)

## **About the author**

**Ankur Mehrotra** joined Amazon in 2008 and is the General Manager of Amazon SageMaker AI. Before SageMaker AI, he helped build Amazon.com’s advertising systems and automated pricing technologies.

![image5](/images/3-BlogsTranslated/05.png)

