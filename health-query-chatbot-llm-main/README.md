# 🩺 General Health Query Chatbot

A prompt-engineered health chatbot that answers general medical questions using a Large Language Model — with built-in safety filters to prevent harmful outputs.

---

## 🎯 Objective

Design and build a conversational health assistant using prompt engineering techniques. The chatbot handles general health queries, responds empathetically, and safely declines harmful or dangerous requests.

---

## 🛠️ Tools & Models

| Option | Model | Cost |
|---|---|---|
| **Option A** | OpenAI GPT-3.5-turbo via API | Requires API key |
| **Option B** | Mistral-7B-Instruct (Hugging Face) | Free, no key needed |

---

## 💬 Example Interactions

```
User: What causes a sore throat?
Bot : A sore throat is usually caused by viral infections like the common cold
      or flu. Bacterial infections (like strep throat), dry air, allergies, or
      irritants can also be culprits. If it persists beyond a week, please
      consult a doctor.

User: Is paracetamol safe for children?
Bot : Paracetamol (acetaminophen) is generally considered safe for children
      when given in the correct dose for their weight and age. Always follow
      the dosage instructions on the packaging and consult a pediatrician for
      infants under 3 months.
```

---

## 🔐 Safety Features

| Scenario | Chatbot Behavior |
|---|---|
| Normal health query | Informative answer + "consult a doctor" reminder |
| Crisis keywords (overdose, self-harm) | Immediate redirect to professional help |
| Diagnosis / prescription request | Politely declines, advises professional consultation |
| Multi-turn conversation | Full conversation history maintained for context |

---

## ⚙️ Prompt Engineering Design

The system prompt instructs the model to:
- Act as a **friendly, knowledgeable health assistant**
- Always recommend **consulting a licensed doctor** for diagnosis/treatment
- Never **prescribe medications** or claim to diagnose conditions
- Be **empathetic and supportive** in tone
- **Decline** requests that could cause harm

---

## 🚀 How to Run

```bash
# 1. Clone the repo
git clone https://github.com/engineermuhammadtalha/health-query-chatbot-llm
cd health-query-chatbot-llm

# 2. Install dependencies
pip install -r requirements.txt

# 3. Launch the notebook
jupyter notebook Task4_Health_Query_Chatbot.ipynb
```

### For Option A (OpenAI):
Add your API key in the notebook:
```python
OPENAI_API_KEY = 'sk-your-key-here'
```

### For Option B (Hugging Face — Free):
No setup needed. The model downloads automatically on first run.

---

## 📦 Requirements

**Option A (OpenAI):**
```
openai
jupyter
```

**Option B (Hugging Face):**
```
transformers
torch
accelerate
sentencepiece
jupyter
```

---

## 📁 Project Structure

```
health-query-chatbot-llm/
│
├── Health_Query_Chatbot.ipynb   # Main notebook
├── requirements.txt                   # Dependencies
└── README.md                          # This file
```

---

## 💡 Key Learnings

- **System prompts** are the primary tool to shape LLM personality, scope, and safety
- **Safety filters** must run before sending to the model — not after
- Conversation history enables coherent multi-turn dialogue
- Open-source models (Mistral, Phi-2) are viable free alternatives to GPT-3.5

---

## ⚠️ Disclaimer

This chatbot provides **general health information only**. It is not a substitute for professional medical advice, diagnosis, or treatment. Always consult a qualified healthcare provider.

---

## 👤 Author

MUHAMMAD TALHA
