---
title: "Week 8 Worklog"
date: "2025-10-27"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Objectives:

- Complete courses on NLP (Natural Language Processing)
- Learn more about FastAPI to prepare for the upcoming project

### Tasks to be carried out this week:

| Day | Task | Start Date | End Date | Resources & Notes |
|---|---|---|---|---|
| Mon | **Module 01: NLP Classification & Vector Spaces**<br>- Sentiment Analysis (Logistic Regression, Naive Bayes).<br>- Vector Space Models, Machine Translation & Doc Search. | 27/10/2025 | 27/10/2025 | |
| Tue | **Module 02: Probabilistic Models**<br>- Autocorrect & POS Tagging (Hidden Markov Models).<br>- Autocomplete, Language Models & Word Embeddings. | 28/10/2025 | 28/10/2025 | |
| Wed | **Module 03: Sequence Models**<br>- RNNs, LSTMs, and Named Entity Recognition (NER).<br>- Siamese Networks. | 29/10/2025 | 29/10/2025 | |
| Thu | **Module 04: Attention Models**<br>- Neural Machine Translation (NMT).<br>- Text Summarization & Question Answering (QA). | 30/10/2025 | 30/10/2025 | |
| Fri | **Deployment & API:**<br>- Deploying ML models as APIs.<br>- Building a complete CRUD application using **FastAPI**. | 31/10/2025 | 31/10/2025 | |

### Week 8 Achievements:

#### 1. Module 01 - Natural Language Processing with Classification and Vector Spaces

**Week 01: Sentiment Analysis with Logistic Regression**

- Understood binary classification for sentiment analysis
- Built logistic regression model from scratch
- Feature extraction with Bag of Words
- Preprocessing: tokenization, stemming, stop words removal
- Model evaluation with accuracy, precision, recall

**Week 02: Sentiment Analysis with Naive Bayes**

- Understood Bayes' Theorem and conditional probability
- Built Naive Bayes classifier
- Compared performance with Logistic Regression
- Understood independence assumption
- Laplacian smoothing to handle zero probability

**Week 03: Vector Space Models**

- Vector space models and word representations
- Cosine similarity to measure similarity
- PCA (Principal Component Analysis) for dimensionality reduction
- Visualized word embeddings
- Euclidean distance vs Cosine similarity

**Week 04: Machine Translation and Document Search**

- Word alignment for machine translation
- Hash tables and locality sensitive hashing
- Document search and information retrieval
- K-nearest neighbors in NLP
- Transformation matrices for word translation

#### 2. Module 02 - Natural Language Processing with Probabilistic Models

**Week 01: Auto-correction and Minimum Edit Distance**

- Edit distance (Levenshtein distance)
- Dynamic programming for minimum edit distance
- Spelling correction algorithms
- Probability-based error correction
- N-gram models for spell checking

**Week 02: Part-of-Speech Tagging and Hidden Markov Models**

- Part-of-Speech (POS) tagging
- Hidden Markov Models (HMMs)
- Viterbi algorithm for sequence labeling
- Transition and emission probabilities
- Training HMMs with tagged corpus

**Week 03: Autocomplete and Language Models**

- N-gram language models (unigram, bigram, trigram)
- Perplexity for evaluating language models
- Smoothing techniques (Laplace, Add-k)
- Backoff and interpolation
- Building autocomplete systems

**Week 04: Word Embeddings with Neural Networks**

- Continuous Bag of Words (CBOW)
- Skip-gram model
- Word2Vec architecture
- Training word embeddings
- Negative sampling
- Evaluating word embeddings

#### 3. Module 03 - Natural Language Processing with Sequence Models

**Week 01: Recurrent Neural Networks for Language Modeling**

- RNN architecture and forward propagation
- Backpropagation through time (BPTT)
- Vanishing and exploding gradient problems
- Language modeling with RNNs
- Text generation with RNNs
- GRU (Gated Recurrent Units)

**Week 02: LSTMs and Named Entity Recognition**

- Long Short-Term Memory (LSTM) architecture
- Cell state, forget gate, input gate, output gate
- Named Entity Recognition (NER) task
- Bidirectional LSTMs
- Training LSTMs for sequence labeling
- Evaluating NER systems

**Week 03: Siamese Networks**

- Siamese network architecture
- Triplet loss function
- One-shot learning
- Similarity learning
- Applications: question duplicate detection, semantic similarity
- Cosine similarity in neural networks

#### 4. Module 04 - Natural Language Processing with Attention Models

**Week 01: Neural Machine Translation**

- Sequence-to-sequence (Seq2Seq) models
- Encoder-decoder architecture
- Attention mechanism
- Teacher forcing
- BLEU score for machine translation
- Beam search decoding

**Week 02: Text Summarization**

- Extractive vs Abstractive summarization
- Seq2Seq with attention for summarization
- ROUGE scores (ROUGE-1, ROUGE-2, ROUGE-L)
- Coverage mechanism
- Pointer-generator networks
- Handling long documents

**Week 03: Question Answering**

- Question answering systems
- Context-based QA
- Attention mechanisms for QA
- SQuAD dataset
- Extractive QA models
- End-to-end trainable QA systems

#### 5. FastAPI and Machine Learning Model Deployment

**Machine Learning Model as API:**

- Setup FastAPI project structure
- Load and serve ML models
- Request/Response schemas with Pydantic
- Input validation and error handling
- Preprocessing pipelines in API
- Testing API endpoints
- Dockerize ML API

**FastAPI CRUD Application:**

- RESTful API design principles
- CRUD operations (Create, Read, Update, Delete)
- Database integration (SQLAlchemy)
- Async/await operations
- Authentication and authorization
- API documentation with Swagger/OpenAPI
- Dependency injection in FastAPI
- File structure best practices:
  - `app/main.py`: Entry point
  - `app/routers/`: API routes
  - `app/models/`: Database models
  - `app/schemas/`: Pydantic schemas
  - `app/crud/`: Database operations
  - `app/db/`: Database configuration

**FastAPI Key Features Mastered:**

- Path parameters and query parameters
- Request body validation
- Response models
- Background tasks
- Middleware
- CORS configuration
- Environment variables
- Testing with pytest

**Summary:** Week 8 completed the entire NLP curriculum from basic to advanced, including 4 modules covering topics from classification, probabilistic models, sequence models to attention mechanisms. Mastered techniques from traditional methods (Naive Bayes, HMM) to modern deep learning approaches (RNN, LSTM, Attention). Also mastered FastAPI framework to deploy ML models as production-ready APIs with full CRUD operations, validation, and best practices. Ready to apply NLP and FastAPI knowledge to real-world projects.
