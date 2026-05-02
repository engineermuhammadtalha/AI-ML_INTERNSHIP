# 🎫 Auto Tagging Support Tickets Using LLM



![Python](https://img.shields.io/badge/Python-3.10-blue?style=flat-square)
![HuggingFace](https://img.shields.io/badge/HuggingFace-Transformers-yellow?style=flat-square)
![PromptEng](https://img.shields.io/badge/Technique-Prompt_Engineering-green?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)

---

## 📌 Objective

Automatically classify customer support tickets into predefined categories using three LLM-based approaches — zero-shot, few-shot, and fine-tuned — and output the **top-3 most probable tags** per ticket.

---

## 🏷️ Tag Categories

| Tag | Example Ticket |
|-----|----------------|
| `Billing` | "I was charged twice this month" |
| `Technical Issue` | "App crashes when I open settings" |
| `Account Access` | "Password reset email never arrived" |
| `Feature Request` | "Please add dark mode" |
| `Bug Report` | "Save button deletes data instead of saving" |
| `Shipping/Delivery` | "My package hasn't arrived after 10 days" |
| `Refund` | "I want my money back for the damaged item" |
| `Security` | "I see logins from a country I've never visited" |

---

## 🧠 Methodology / Approach

### Approach 1 — Zero-Shot (BART-MNLI)
```
Ticket Text
    │
    ▼
facebook/bart-large-mnli
    │  (NLI: ticket as premise, each tag as hypothesis)
    ▼
Ranked probabilities → Top-3 tags
```
- No training data required
- Uses natural language inference to score each candidate label

### Approach 2 — Few-Shot (Flan-T5 Prompt Engineering)
```
[System prompt + 8 labeled examples (1 per class)]
    +
Ticket Text
    │
    ▼
google/flan-t5-base  (beam search, num_beams=4)
    │
    ▼
Generated tag string → matched to canonical tag
```
- 8 carefully chosen examples cover all categories
- No gradient updates — pure prompt engineering

### Approach 3 — Fine-Tuned Classification (DistilBERT)
```
Labeled Ticket Dataset
    │
    ▼
distilbert-base-uncased + Classification Head (8 classes)
    │
    ▼
Fine-tune  (5 epochs · lr=3e-5 · AdamW)
    │
    ▼
Softmax probabilities → Top-3 tags with confidence scores
```
- Best accuracy of the three approaches
- 40% faster than BERT-base with comparable results

---

## 📊 Performance Comparison

| Approach | Accuracy | F1-Macro | Training Data Needed |
|----------|----------|----------|---------------------|
| Zero-Shot (BART-MNLI) | ~55–65% | ~0.50–0.60 | None |
| Few-Shot (Flan-T5) | ~65–75% | ~0.60–0.70 | 8 examples total |
| **Fine-Tuned (DistilBERT)** | **~85–95%** | **~0.85–0.92** | ~32 per class |

---

## 🎯 Sample Top-3 Output

```
Ticket: "I was double charged and also need a refund for the extra payment"

  Rank 1 → Billing          76.3%  ████████████████░░░░
  Rank 2 → Refund           21.4%  ████░░░░░░░░░░░░░░░░
  Rank 3 → Account Access    1.8%  ░░░░░░░░░░░░░░░░░░░░
```

---

## 🔍 Observations

1. **Zero-shot** handles well-separated categories well (Security, Feature Request) but confuses overlapping ones (Billing vs Refund)
2. **Few-shot** gains ~10% F1 over zero-shot with only 8 examples — prompt quality and example diversity are critical
3. **Fine-tuning** delivers the strongest results; DistilBERT learns task-specific representations quickly even on small data
4. **Billing ↔ Refund** is the hardest confusion pair — context phrases like "charged extra" vs "get my money back" resolve most cases
5. **Top-3 tags** are more actionable in production than top-1 alone — borderline tickets often have two valid categories

---

## 🗂️ Project Structure

```
support-ticket-auto-tagger/
├── task5_support_ticket_tagging.ipynb   ← Main notebook
├── ticket_tagger/                        ← Fine-tuned DistilBERT weights
│   ├── config.json
│   └── pytorch_model.bin
├── outputs/
│   ├── task5_eda.png
│   └── task5_comparison.png
├── requirements.txt
└── README.md
```

---

## ⚙️ Setup & Run

```bash
# 1. Clone the repo
git clone https://github.com/engineermuhammadtalha/support-ticket-auto-tagger
cd support-ticket-auto-tagger

# 2. Install dependencies
pip install -r requirements.txt

# 3. Run the notebook
jupyter notebook task5_support_ticket_tagging.ipynb
```

---

## 🛠️ Tech Stack

`Python` · `PyTorch` · `Hugging Face Transformers` · `Datasets` · `DistilBERT` · `Flan-T5` · `BART-MNLI` · `scikit-learn` · `Matplotlib` · `Seaborn`
