# 🤖 AI / ML Internship Projects — Muhammad Talha

> A curated collection of 8 end-to-end machine learning and AI projects spanning NLP, LLMs, Computer Vision, and classical ML pipelines — built and documented during my AI/ML internship.

---

## 👤 About

**Muhammad Talha** · AI Engineer
🔗 [GitHub Profile](https://github.com/engineermuhammadtalha)

---

## 🗂️ Repository Structure

```
AI-ML_INTERNSHIP/
│
├── bert-news-classifier-main/            ← NLP · Fine-tuned BERT · Gradio App
├── churn-prediction-pipeline-main/       ← ML Pipeline · scikit-learn · joblib
├── health-query-chatbot-llm-main/        ← LLM · Prompt Engineering · Safety Filters
├── house-price-prediction-ml-main/       ← Regression · EDA · Feature Engineering
├── mental-health-chatbot-finetuned-main/ ← Fine-tuned LLM · EmpatheticDialogues
├── multimodal-housing-price-main/        ← Deep Learning · ResNet-18 + MLP Fusion
├── rag-context-aware-chatbot-main/       ← RAG · Vector Search · LLM
├── support-ticket-auto-tagger-main/      ← NLP · Zero-shot / Few-shot / Fine-tuned
│
└── README.md                             ← This file
```

---

## 📋 Projects at a Glance

| # | Project | Domain | Key Tech | Best Metric |
|---|---------|--------|----------|-------------|
| 1 | [BERT News Classifier](#1--bert-news-classifier) | NLP | BERT, Gradio | 94–95% Accuracy |
| 2 | [Churn Prediction Pipeline](#2--churn-prediction-pipeline) | ML / MLOps | scikit-learn, joblib | 0.87 ROC-AUC |
| 3 | [Health Query Chatbot](#3--health-query-chatbot-llm) | LLM | GPT / Mistral-7B | Safety-first design |
| 4 | [House Price Prediction](#4--house-price-prediction-ml) | Regression | Gradient Boosting | High R² vs LR |
| 5 | [Mental Health Chatbot](#5--mental-health-chatbot-fine-tuned) | LLM Fine-tuning | distilgpt2, HuggingFace | Empathetic responses |
| 6 | [Multimodal Housing Price](#6--multimodal-housing-price) | CV + ML | ResNet-18, PyTorch | ~12–18% MAPE |
| 7 | [RAG Context-Aware Chatbot](#7--rag-context-aware-chatbot) | LLM + RAG | Vector DB, Embeddings | Context-grounded |
| 8 | [Support Ticket Auto-Tagger](#8--support-ticket-auto-tagger) | NLP | DistilBERT, Flan-T5 | 85–95% Accuracy |

---

## 📁 Project Details

---

### 1 · BERT News Classifier

📂 [`bert-news-classifier-main/`](./bert-news-classifier-main)

Fine-tuned `bert-base-uncased` on the AG News dataset (120K samples) to classify news headlines into 4 categories: **World, Sports, Business, Sci/Tech**. Deployed as an interactive Gradio web app.

**Key Results:**
- Test Accuracy: **94–95%** | F1-Macro: **~0.94**
- 3 epochs with AdamW optimizer, EarlyStoppingCallback picks optimal checkpoint
- int8 quantization reduces inference time ~40% with <1% accuracy drop
- Deployed as a live Gradio interface

**Tech Stack:** `Python` · `PyTorch` · `Hugging Face Transformers` · `Gradio` · `scikit-learn` · `Matplotlib`

---

### 2 · Churn Prediction Pipeline

📂 [`churn-prediction-pipeline-main/`](./churn-prediction-pipeline-main)

Production-ready, reusable ML pipeline using scikit-learn's `Pipeline` API to predict telecom customer churn. The full preprocessing + inference chain is exported as a single `.joblib` file for zero-code deployment.

**Key Results:**
- Best ROC-AUC: **0.87** (Random Forest) | Best F1-Score: **0.62**
- GridSearchCV with 5-fold StratifiedKFold; handles class imbalance (~26% churn rate)
- Contract type is the strongest predictor — month-to-month customers churn 3× more
- One-file deployment: `pipeline.predict_proba(df)` on any new data

**Tech Stack:** `Python` · `scikit-learn` · `pandas` · `NumPy` · `joblib` · `Matplotlib` · `Seaborn`

---

### 3 · Health Query Chatbot (LLM)

📂 [`health-query-chatbot-llm-main/`](./health-query-chatbot-llm-main)

Conversational health assistant using prompt engineering with GPT-3.5-turbo or the free Mistral-7B-Instruct model. Features pre-inference safety filters that block harmful queries before reaching the model.

**Key Design:**
- Safety filters run *before* the model call — not after
- System prompt enforces empathetic tone, declines diagnosis/prescription requests
- Multi-turn conversation with full history context maintained
- Supports both paid (OpenAI) and free (Hugging Face) backends — no locked-in dependency

**Tech Stack:** `Python` · `OpenAI API` · `Mistral-7B-Instruct` · `Hugging Face Transformers`

---

### 4 · House Price Prediction (ML)

📂 [`house-price-prediction-ml-main/`](./house-price-prediction-ml-main)

Regression project on the California Housing dataset with thorough EDA, engineered features, and a head-to-head comparison of Linear Regression vs. Gradient Boosting.

**Key Results:**
- Gradient Boosting consistently achieves higher R² and lower MAE/RMSE than LR
- Engineered features: `RoomsPerHousehold`, `BedroomsPerRoom`
- Geographic coordinates (latitude/longitude) carry strong house price signal
- Log-transforming the target reduces skew and stabilises linear model training

**Tech Stack:** `Python` · `scikit-learn` · `pandas` · `NumPy` · `Matplotlib` · `Seaborn`

---

### 5 · Mental Health Chatbot (Fine-Tuned)

📂 [`mental-health-chatbot-finetuned-main/`](./mental-health-chatbot-finetuned-main)

`distilgpt2` fine-tuned on the EmpatheticDialogues dataset (25,000 conversation pairs across 32 emotion categories) to generate warm, emotionally intelligent responses. Includes a Streamlit web UI and crisis safety filters.

**Key Design:**
- Causal Language Modelling (CLM) fine-tuning teaches conversational turn-taking
- Crisis keywords (suicide, self-harm) trigger immediate redirect to professional resources
- Clean Streamlit chat interface with session memory; runs fully locally
- Upgradeable to GPT-Neo-1.3B or Mistral-7B for production-quality responses

**Tech Stack:** `Python` · `distilgpt2` · `Hugging Face Trainer API` · `Datasets` · `Streamlit` · `PyTorch`

---

### 6 · Multimodal Housing Price Prediction

📂 [`multimodal-housing-price-main/`](./multimodal-housing-price-main)

Predicts housing sale prices by fusing two modalities — structured tabular features and house exterior images — using a late-fusion deep learning model (ResNet-18 CNN + MLP tabular branch) in a single unified PyTorch model.

**Key Results:**
- MAE: **~$25,000–$35,000** | MAPE: **~12–18%**
- Real house images give 5–8% RMSE reduction over tabular-only model
- Late fusion outperforms early fusion and both unimodal baselines
- Huber loss more robust than MSE for luxury price outliers

**Tech Stack:** `Python` · `PyTorch` · `torchvision` · `ResNet-18` · `scikit-learn` · `Pillow` · `NumPy`

---

### 7 · RAG Context-Aware Chatbot

📂 [`rag-context-aware-chatbot-main/`](./rag-context-aware-chatbot-main)

A Retrieval-Augmented Generation (RAG) chatbot that grounds its answers in retrieved document context using vector similarity search, significantly reducing hallucinations compared to a vanilla LLM.

**Key Design:**
- Document chunks embedded via Sentence Transformers and stored in FAISS / ChromaDB
- Top-k retrieved chunks injected as context into LLM prompt
- Grounded answers anchored to source documents — not model memorisation

**Tech Stack:** `Python` · `LangChain` · `FAISS` · `Sentence Transformers` · `LLM API`

---

### 8 · Support Ticket Auto-Tagger

📂 [`support-ticket-auto-tagger-main/`](./support-ticket-auto-tagger-main)

Automatically classifies customer support tickets into 8 categories and outputs the **top-3 most probable tags** per ticket. Benchmarks three LLM-based approaches from zero-shot to fine-tuning.

**Approach Comparison:**

| Approach | Model | Accuracy | F1-Macro | Training Data |
|----------|-------|----------|----------|---------------|
| Zero-Shot | BART-MNLI | 55–65% | 0.50–0.60 | None |
| Few-Shot | Flan-T5 | 65–75% | 0.60–0.70 | 8 examples |
| **Fine-Tuned** | **DistilBERT** | **85–95%** | **0.85–0.92** | ~32 per class |

**Categories:** Billing · Technical Issue · Account Access · Feature Request · Bug Report · Shipping/Delivery · Refund · Security

**Tech Stack:** `Python` · `PyTorch` · `DistilBERT` · `Flan-T5` · `BART-MNLI` · `Hugging Face Transformers`

---

## 🛠️ Skills Demonstrated

| Category | Technologies |
|----------|-------------|
| **NLP & Transformers** | BERT, DistilBERT, Flan-T5, BART-MNLI, GPT, Mistral-7B |
| **LLM Techniques** | Prompt Engineering, Fine-tuning (CLM), RAG, Zero/Few-shot |
| **Computer Vision** | ResNet-18, torchvision, Multimodal late fusion |
| **Classical ML** | Random Forest, Gradient Boosting, Logistic Regression |
| **MLOps** | scikit-learn Pipelines, joblib export, GridSearchCV |
| **Deployment** | Gradio, Streamlit, Jupyter |
| **Core Libraries** | PyTorch, Hugging Face, scikit-learn, pandas, NumPy, Matplotlib |

---

## ⚙️ Getting Started

Each project is self-contained in its own subfolder with a `README.md`, `requirements.txt`, and Jupyter notebook.

```bash
# Clone this repo
git clone https://github.com/engineermuhammadtalha/AI-ML_INTERNSHIP
cd AI-ML_INTERNSHIP

# Navigate to any project
cd bert-news-classifier-main

# Install dependencies
pip install -r requirements.txt

# Launch notebook
jupyter notebook
```

---

## 📄 License

All projects are released under the [MIT License](LICENSE).

---

> *Built with curiosity and code — Muhammad Talha*
