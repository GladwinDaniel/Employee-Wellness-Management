# Employee Wellness Management - Multilingual NLP Preprocessing Pipeline

This directory contains the implementation of Milestone 2 for the Employee Wellness Management portal. This phase expands the Reflect and Support Portal by integrating a robust, multilingual NLP preprocessing pipeline, automated translation, sentiment analysis, fine-grained emotion classification, and a crisis-safe interactive wellness chatbot.

## Core Features

### Multilingual NLP Preprocessing Pipeline
- **Text Normalization**: Utilizes the ftfy library to fix encoding issues and normalize raw input text automatically.
- **Language Detection**: Automatically detects the language of input text (supporting languages like Tamil, Telugu, Kannada, Hindi, and English) using the langdetect library.
- **Text Cleaning**: Cleans input by stripping URLs, emails, user mentions, hashtags, and emojis, followed by extra whitespace removal.
- **Tokenization and Filtering**: Tokenizes clean text and filters out punctuation, numbers, and language-specific stopwords dynamically using the stopwordsiso library (supporting 50+ languages).

### Translation and Lemmatization
- **Automated English Translation**: Automatically translates filtered non-English text to English using deep-translator to prepare it for sentiment and emotion analyzers.
- **Lemmatization**: Extracts lemmas (dictionary base forms) of words in the translated English text utilizing a spaCy pipeline (xx_sent_ud_sm).

### Sentiment and Emotion Analysis
- **Sentiment Scoring**: Computes positive, negative, neutral, and compound scores using VADER Sentiment Analysis on the translated text.
- **BERT Emotion Classification**: Utilizes a fine-tuned BERT base model (bhadresh-savani/bert-base-go-emotion) trained on the GoEmotions dataset to perform multi-label emotion classification, mapping 28 fine-grained emotions into six major wellness categories: Happy, Sad, Stress, Angry, Fear, and Neutral.

### Interactive Wellness Chatbot
- **Conversational Support**: Integrates an interactive chatbot utilizing the Qwen2.5-0.5B-Instruct causal language model to validate employee feelings and suggest coping strategies.
- **Crisis safety net**: Monitors inputs for specific crisis keywords (e.g., suicide, self-harm) and immediately responds with a predefined supportive message and hotline details, bypassing the AI generator for safety.

### Web Application and Backend APIs
- **FastAPI Endpoints**:
  - GET /health: Health status check.
  - POST /upload: Validates, size-limits, and parses CSV/TXT files, returning previews.
  - POST /analyze: Orchestrates the entire NLP pipeline, extracts columns for CSV, and returns preprocessed text, tokens, translation, sentiment scores, and emotion distributions.
  - POST /chat: Handles chatbot requests statefully from the client side.
- **Streamlit Frontend Dashboard**:
  - Interactive login, sign-up, and OTP verification flow.
  - Sidebar and main panels for file uploading, running NLP analysis, viewing processing statistics, and plotting interactive sentiment and emotion charts.
  - Wellness chat interface with options to carry over conversation history or reset the session.

## Technical Stack and Dependencies

- **Frameworks**: Streamlit, FastAPI
- **Web utilities**: Pyngrok, Uvicorn, Python-Multipart, Requests, PyJWT, Bcrypt, Python-Dotenv, Email-Validator
- **NLP and Translation**: SpaCy (xx_sent_ud_sm), ftfy, emoji, deep-translator, langdetect, stopwordsiso
- **Machine Learning and Modeling**: PyTorch, Transformers, Accelerate, VaderSentiment
- **Data Science and Visualization**: Pandas, Matplotlib

## Execution Guide

All modules (database initialization, authentication, email utilities, Streamlit app, NLP pipeline, and FastAPI backend) are packaged into the Colab Notebook.

1. Open NLP_Text_Preprocessing_Pipeline.ipynb in Google Colab.
2. In the Google Colab Secrets sidebar, add the required keys: DB_HOST, DB_PORT, DB_NAME, DB_USER, DB_PASSWORD, JWT_SECRET, SMTP_EMAIL, SMTP_APP_PASSWORD, NGROK_AUTHTOKEN.
3. Run the installation cell to download NLP models and dependencies.
4. Execute the subsequent cells to configure the environment, establish database tables, write script files, and run both servers.
5. Access the application using the public ngrok tunnel URL outputted at the end of the notebook.
