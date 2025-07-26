# Multilingual Retrieval-Augmented Generation (RAG) System

A simple RAG pipeline capable of handling both **English and Bangla** queries to retrieve and answer questions from a Bangla literature PDF (HSC26 Bangla 1st Paper). Built for AI Engineer (Level-1) Technical Assessment.

---
## 🚀 Features
- Accepts Bangla and English queries
- Retrieves answers from vectorized Bangla literature PDF
- Preprocessing and chunking for accurate retrieval
- Short-term (chat memory) & long-term (PDF knowledge base) context management
---

## 📚 Dataset
- Source: HSC Bangla 1st Paper (Class 11–12)
- Format: PDF → text extracted using PyMuPDF
---

## 🛠️ Tools and Libraries

| Task                    | Tool/Library Used             |
|-------------------------|-------------------------------|
| Text Extraction         | `PyMuPDF (fitz)`              |
| Chunking Strategy       | Sentence-based chunking       |
| Embedding Model         | `sentence-transformers/all-MiniLM-L6-v2` |
| Vector Storage          | `FAISS`                       |
| Language Handling       | UTF-8 Bangla + English        |
| Evaluation              | Cosine similarity + qualitative examples |
| Interface               | Jupyter Notebook              |

---

## ⚙️ Setup Guide

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/Multilingual-RAG-Bangla-English.git
cd Multilingual-RAG-Bangla-English

# Install dependencies
pip install -r requirements.txt

