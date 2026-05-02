# 🧠 Mental Health Support Chatbot (Fine-Tuned LLM)


A fine-tuned language model that provides empathetic, emotionally supportive responses for users dealing with stress, anxiety, and emotional challenges.

---

## 🎯 Objective

Fine-tune a small open-source language model on real empathetic human dialogues so it learns to respond with warmth and emotional intelligence — not just information.

---

## 📂 Dataset

- **Name:** [EmpatheticDialogues](https://huggingface.co/datasets/empathetic_dialogues) by Facebook AI Research
- **Size:** ~25,000 conversation pairs across 32 emotion categories
- **Emotions include:** Joy, Sadness, Anger, Fear, Surprise, Disgust, Anxiety, and more
- **Source:** Hugging Face Datasets (auto-downloaded)

---

## 🤖 Model

| Component | Detail |
|---|---|
| Base Model | `distilgpt2` (82M parameters) |
| Fine-tuning Method | Causal Language Modeling (CLM) |
| Training Framework | Hugging Face `Trainer` API |
| Training Samples | 5,000 (subset for speed — increase for quality) |
| Epochs | 3 |
| Interface | Command-line + optional Streamlit web app |

> **Alternatives:** Replace `distilgpt2` with `EleutherAI/gpt-neo-1.3B` or `mistralai/Mistral-7B-Instruct-v0.2` for significantly better response quality.

---

## 💬 Example Interactions

```
User: I've been feeling really anxious lately and can't sleep.
Bot : I hear you — anxiety can be exhausting. It might help to try a short
      breathing exercise before bed. You're not alone in this. Have you been
      able to talk to anyone about what's on your mind?

User: I'm overwhelmed with work and feel like I can't cope.
Bot : That sounds really tough, and it's okay to feel overwhelmed sometimes.
      Taking it one step at a time can help. Is there something small you
      could set aside today to give yourself a break?
```

---

## 🔐 Safety Features

| Trigger | Response |
|---|---|
| Crisis keywords (suicide, self-harm, kill myself) | Immediately redirects to professional crisis resources |
| Emotional distress signals | Empathetic acknowledgment + gentle guidance |
| General wellness queries | Supportive, non-prescriptive advice |

---

## 🚀 How to Run

```bash
# 1. Clone the repo
git clone https://github.com/engineermuhammadtalha/mental-health-chatbot-finetuned
cd mental-health-chatbot-finetuned

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the notebook for fine-tuning + inference
jupyter notebook Task5_Mental_Health_Chatbot.ipynb

# 4. (Optional) Launch Streamlit web app
streamlit run app.py
```

---

## 📦 Requirements

```
transformers
datasets
torch
accelerate
evaluate
streamlit
jupyter
```

Install all at once:
```bash
pip install transformers datasets torch accelerate evaluate streamlit jupyter
```

> **GPU strongly recommended.** Fine-tuning on CPU is possible but slow (~1–2 hours for 5,000 samples).

---

## 📁 Project Structure

```
mental-health-chatbot-finetuned/
│
├── Mental_Health_Chatbot.ipynb    # Fine-tuning + inference notebook
├── app.py                               # Streamlit chat interface
├── mental_health_chatbot_final/         # Saved fine-tuned model (after training)
│   ├── config.json
│   ├── pytorch_model.bin
│   └── tokenizer files
├── requirements.txt                     # Dependencies
└── README.md                            # This file
```

---

## 🖥️ Streamlit Interface Preview

Once trained, launch the web UI:
```bash
streamlit run app.py
```
Features:
- Clean chat interface with message history
- Automatic crisis detection and redirection
- Runs locally — no data sent to external servers

---

## 💡 Key Learnings

- **Fine-tuning** adapts a general-purpose LLM to a specific emotional tone using domain data
- **Causal LM** training on dialogue pairs teaches the model conversational turn-taking
- **Safety filters at inference time** are essential for mental health applications
- Larger base models (GPT-Neo, Mistral) produce significantly more coherent and empathetic responses

---

## 🔮 Future Improvements

- Fine-tune on full EmpatheticDialogues dataset (25K+ samples)
- Use RLHF (Reinforcement Learning from Human Feedback) for alignment
- Add mood tracking and session memory
- Integrate professional resource recommendations based on detected emotion

---

## ⚠️ Disclaimer

This chatbot is for **educational and emotional support purposes only**. It is **not** a replacement for professional mental health care. If you or someone you know is in crisis, please contact a mental health professional or a crisis helpline immediately.

---

## 👤 Author

MUHAMMAD TALHA