---
title: "Week 9 Worklog"
date: "2025-11-03"
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

- FastAPI project with MongoDB
- Vietnamese STT library selected and integrated
- Vietnamese OCR library selected and tested
- NLP extraction: amount, category, date, jar detection (REQ-027)
- Detect multiple transactions (REQ-027)
- Publish events to RabbitMQ

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Project Setup:** FastAPI structure, Docker, MongoDB setup.<br>**Tech Research:** Research optimal Vietnamese OCR (Bills) and STT (Voice) models. | 03/11/2025 | 03/11/2025 | |
| Tue | **Core API Development:**<br>- Setup Endpoints, Pydantic models.<br>- Configure Middleware (CORS, Error handling) & Logging. | 04/11/2025 | 04/11/2025 | |
| Wed | **Voice & OCR Implementation:**<br>- Voice: Install STT libs, audio pre-processing.<br>- OCR: Install libs, research image pre-processing techniques. | 05/11/2025 | 05/11/2025 | |
| Thu | **Optimization:**<br>- **Voice:** Implement **PhoWhisper** (VinAI), transaction/timestamp detection.<br>- **OCR:** Enhance image quality, collect Vietnamese bill datasets. | 06/11/2025 | 06/11/2025 | |
| Fri | **Integration & Testing:**<br>- Handle background tasks.<br>- E2E Testing for Voice flow.<br>- Evaluate OCR models (Tesseract, EasyOCR, etc.). | 07/11/2025 | 07/11/2025 | |

### Week 9 Achievements:

#### 1. Project Setup and Infrastructure

- Completed FastAPI project structure with standard directories (/app, /models, /services, /utils, /routers, /schemas, /ai-models)
- Setup Python 3.11+ environment with virtual environment
- Installed and configured local MongoDB using Docker
- Created `ai_service_db` database and collections for Bills and Voices
- Setup MongoDB connection with MongoEngine and lifecycle management

#### 2. API Structure and Middleware

- Setup API endpoints for Voice and Bill processing
- Created Pydantic models for request/response validation
- Configured CORS middleware and error handling middleware
- Implemented health check endpoint (GET /health)
- Integrated structlog for logging system

#### 3. Voice Processing (Speech-to-Text)

- Researched and selected **PhoWhisper from VinAI** for Vietnamese STT
- Implemented audio preprocessing and Voice-to-Text integration
- Tested model accuracy and voice detection capability
- Configured endpoint to return correct defined categories
- Tested processing multiple transactions simultaneously
- Setup time detection for transactions from speech
- Created transaction objects from voice data

#### 4. Bill Processing (OCR)

- Researched and selected appropriate OCR libraries (Tesseract, EasyOCR)
- Implemented image preprocessing to optimize quality before OCR
- Collected diverse Vietnamese bill dataset (electricity, supermarket, restaurants, convenience stores, coffee shops)
- Tested OCR models with real bill images

#### 5. NLP Extraction and Data Processing

- Implemented information extraction: amount, category, date (REQ-027)
- Jar detection
- Multiple transaction detection in a single request

#### 6. RabbitMQ Integration

- Setup event publishing to RabbitMQ
- Handled background tasks for Voice and Bill processing

#### 7. Testing and Quality Assurance

- End-to-end testing for Voice processing pipeline (Recording → Processing → Return Endpoint)
- Evaluated and improved Voice processing accuracy
- Tested OCR models with real dataset

**Summary:** Week 9 successfully completed all objectives, including FastAPI-MongoDB infrastructure setup, PhoWhisper model integration for Vietnamese STT, OCR implementation for bill processing, and event publishing system with RabbitMQ. NLP functions for transaction information extraction were implemented and successfully tested.
