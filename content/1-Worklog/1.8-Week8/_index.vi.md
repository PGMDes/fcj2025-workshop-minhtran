---
title: "Worklog Tuần 8"
date: "2025-10-27"
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Mục tiêu tuần 8:

- Hoàn thành các khóa học về NLP (Natural Language Processing)
- Tìm hiểu thêm về FastAPI để chuẩn bị cho dự án sắp tới.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày kết thúc | Nguồn tài liệu và ghi chú học tập |
|---|---|---|---|---|
| 2 | **Module 01: NLP cơ bản & Vector Spaces**<br>- Phân tích cảm xúc (Logistic Regression, Naive Bayes).<br>- Mô hình không gian Vector, Dịch máy & Tìm kiếm tài liệu. | 27/10/2025 | 27/10/2025 | |
| 3 | **Module 02: Mô hình Xác suất (Probabilistic Models)**<br>- Autocorrect, Gắn thẻ từ loại (POS Tagging - HMMs).<br>- Language Models & Word Embeddings. | 28/10/2025 | 28/10/2025 | |
| 4 | **Module 03: Mô hình Chuỗi (Sequence Models)**<br>- Mạng RNNs, LSTMs và nhận dạng thực thể tên (NER).<br>- Mạng Siamese Networks. | 29/10/2025 | 29/10/2025 | |
| 5 | **Module 04: Mô hình Attention (Attention Models)**<br>- Dịch máy Neural (NMT).<br>- Tóm tắt văn bản (Text Summarization) & Hỏi đáp (QA). | 30/10/2025 | 30/10/2025 | |
| 6 | **Deployment & API:**<br>- Triển khai mô hình ML thành API.<br>- Xây dựng ứng dụng CRUD hoàn chỉnh với **FastAPI**. | 31/10/2025 | 31/10/2025 | |



### Kết quả đạt được tuần 8:

#### 1. Module 01 - Xử Lý Ngôn Ngữ Tự Nhiên với Phân Loại và Không Gian Vectơ

**Week 01: Phân Tích Tình Cảm với Hồi Quy Logistic**

- Hiểu về binary classification cho sentiment analysis
- Xây dựng model logistic regression từ đầu
- Feature extraction với Bag of Words
- Preprocessing: tokenization, stemming, stop words removal
- Đánh giá model với accuracy, precision, recall

**Week 02: Phân Tích Tình Cảm với Naive Bayes**

- Hiểu về Bayes' Theorem và conditional probability
- Xây dựng Naive Bayes classifier
- So sánh performance với Logistic Regression
- Hiểu về independence assumption
- Laplacian smoothing để xử lý zero probability

**Week 03: Mô Hình Không Gian Vector**

- Vector space models và word representations
- Cosine similarity để đo độ tương đồng
- PCA (Principal Component Analysis) để giảm chiều
- Visualize word embeddings
- Euclidean distance vs Cosine similarity

**Week 04: Dịch Máy và Tìm Kiếm Tài Liệu**

- Word alignment cho machine translation
- Hash tables và locality sensitive hashing
- Document search và information retrieval
- K-nearest neighbors trong NLP
- Transformation matrices cho word translation

#### 2. Module 02 - Xử Lý Ngôn Ngữ Tự Nhiên với Mô Hình Xác Suất

**Week 01: Tự Động Sửa Lỗi và Khoảng Cách Chỉnh Sửa Tối Thiểu**

- Edit distance (Levenshtein distance)
- Dynamic programming cho minimum edit distance
- Spelling correction algorithms
- Probability-based error correction
- N-gram models cho spell checking

**Week 02: Gắn Thẻ Từ Loại và Mô Hình Markov Ẩn**

- Part-of-Speech (POS) tagging
- Hidden Markov Models (HMMs)
- Viterbi algorithm cho sequence labeling
- Transition và emission probabilities
- Training HMMs với tagged corpus

**Week 03: Autocomplete và Language Models**

- N-gram language models (unigram, bigram, trigram)
- Perplexity để đánh giá language models
- Smoothing techniques (Laplace, Add-k)
- Backoff và interpolation
- Building autocomplete systems

**Week 04: Word Embeddings với Neural Networks**

- Continuous Bag of Words (CBOW)
- Skip-gram model
- Word2Vec architecture
- Training word embeddings
- Negative sampling
- Evaluating word embeddings

#### 3. Module 03 - Xử Lý Ngôn Ngữ Tự Nhiên với Mô Hình Chuỗi

**Week 01: Recurrent Neural Networks cho Language Modeling**

- RNN architecture và forward propagation
- Backpropagation through time (BPTT)
- Vanishing và exploding gradient problems
- Language modeling với RNNs
- Text generation với RNNs
- GRU (Gated Recurrent Units)

**Week 02: LSTMs và Named Entity Recognition**

- Long Short-Term Memory (LSTM) architecture
- Cell state, forget gate, input gate, output gate
- Named Entity Recognition (NER) task
- Bidirectional LSTMs
- Training LSTMs cho sequence labeling
- Evaluating NER systems

**Week 03: Siamese Networks**

- Siamese network architecture
- Triplet loss function
- One-shot learning
- Similarity learning
- Applications: question duplicate detection, semantic similarity
- Cosine similarity trong neural networks

#### 4. Module 04 - Xử Lý Ngôn Ngữ Tự Nhiên với Các Mô Hình Chú Ý

**Week 01: Neural Machine Translation**

- Sequence-to-sequence (Seq2Seq) models
- Encoder-decoder architecture
- Attention mechanism
- Teacher forcing
- BLEU score cho machine translation
- Beam search decoding

**Week 02: Tóm Tắt Văn Bản**

- Extractive vs Abstractive summarization
- Seq2Seq với attention cho summarization
- ROUGE scores (ROUGE-1, ROUGE-2, ROUGE-L)
- Coverage mechanism
- Pointer-generator networks
- Handling long documents

**Week 03: Question Answering**

- Question answering systems
- Context-based QA
- Attention mechanisms cho QA
- SQuAD dataset
- Extractive QA models
- End-to-end trainable QA systems

#### 5. FastAPI và Triển Khai Machine Learning Models

**Machine Learning Model as API:**

- Setup FastAPI project structure
- Load và serve ML models
- Request/Response schemas với Pydantic
- Input validation và error handling
- Preprocessing pipelines trong API
- Testing API endpoints
- Dockerize ML API

**FastAPI CRUD Application:**

- RESTful API design principles
- CRUD operations (Create, Read, Update, Delete)
- Database integration (SQLAlchemy)
- Async/await operations
- Authentication và authorization
- API documentation với Swagger/OpenAPI
- Dependency injection trong FastAPI
- File structure best practices:
  - `app/main.py`: Entry point
  - `app/routers/`: API routes
  - `app/models/`: Database models
  - `app/schemas/`: Pydantic schemas
  - `app/crud/`: Database operations
  - `app/db/`: Database configuration

**FastAPI Key Features Mastered:**

- Path parameters và query parameters
- Request body validation
- Response models
- Background tasks
- Middleware
- CORS configuration
- Environment variables
- Testing với pytest

**Tổng kết:** Tuần 8 đã hoàn thành toàn bộ chương trình học về NLP từ cơ bản đến nâng cao, bao gồm 4 modules với các chủ đề từ classification, probabilistic models, sequence models đến attention mechanisms. Nắm vững các kỹ thuật từ traditional methods (Naive Bayes, HMM) đến modern deep learning approaches (RNN, LSTM, Attention). Đồng thời thành thạo FastAPI framework để triển khai ML models thành production-ready APIs với đầy đủ CRUD operations, validation, và best practices. Đã sẵn sàng áp dụng kiến thức NLP và FastAPI vào dự án thực tế.
