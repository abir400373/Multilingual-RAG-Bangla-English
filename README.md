# Multilingual Retrieval-Augmented Generation (RAG) System

A simple RAG pipeline capable of handling both **English and Bangla** queries to retrieve and answer questions from a Bangla literature PDF (HSC26 Bangla 1st Paper). Built for AI Engineer (Level-1) Technical Assessment.

---
## 🚀 Features
- Accepts Bangla and English queries
- Retrieves answers from vectorized Bangla literature PDF
- Preprocessing and chunking for accurate retrieval
---

## 📚 Dataset
- Source: HSC Bangla 1st Paper (Class 11–12)
- Format: PDF → text extracted using PyMuPDF and Tesseract OCR
---

## 🛠️ Tools and Libraries
| Task                          | Tool / Library Used                                                                 |
| ----------------------------- | ----------------------------------------------------------------------------------- |
| **Text Extraction**           | `PyMuPDF (fitz)` for PDF text<br>`pytesseract` (Tesseract OCR) for image-based text |
| **OCR Language Support**      | `ben.traineddata` for Bangla OCR (Tesseract)                                        |
| **Chunking Strategy**         | Sentence-based chunking for semantic clarity                                        |
| **Text Embedding Model**      | `sentence-transformers/all-MiniLM-L6-v2`                                            |
| **Vector Storage & Search**   | `FAISS` for fast vector similarity search                                           |
| **Language Handling**         | UTF-8 Bangla + English                                                              |
| **Similarity Evaluation**     | Cosine similarity + manually verified examples                                      |
| **Answer Selection**          | Closest retrieved chunk used directly as the answer (no LLM used)                   |
| **Interface**                 | Jupyter Notebook (Interactive development)                                          |

---

## ⚙️ Setup Guide

```bash
# Clone the repo
git clone https://github.com/YOUR_USERNAME/Multilingual-RAG-Bangla-English.git
cd Multilingual-RAG-Bangla-English

# Install dependencies
pip install -r requirements.txt
```

###  🧾 Tesseract OCR Setup for Bangla (ben)
To enable Bangla OCR support for PDF/image text extraction:
1st Step: Download and install Tesseract OCR from the official UB Mannheim Windows installer:
👉 https://github.com/UB-Mannheim/tesseract/wiki

2nd Step: Download Bangla Language Data
Go to: https://github.com/tesseract-ocr/tessdata
Download the file: ben.traineddata
Copy it to the Tesseract tessdata directory: "C:\Program Files\Tesseract-OCR\tessdata\"

3rd Step:  Set the Tesseract Path in Code
In your Python script or notebook, configure the Tesseract path: (if Path Changes)
```bash
pytesseract.pytesseract.tesseract_cmd = r'C:\Program Files\Tesseract-OCR\tesseract.exe'  # Update path if differ
```


## 🧠 Questions & Answers
### 1. What method or library did you use to extract the text, and why? Did you face any formatting challenges with the PDF content?
I used PyMuPDF (fitz) for initial PDF text extraction due to its speed and support for Unicode. However, I encountered formatting issues where text wasn't read properly because of font encoding or scanned pages. To overcome this, I added OCR support using pytesseract with the Bengali trained data. This hybrid approach ensured accurate text extraction even when direct parsing failed.

### 2. What chunking strategy did you choose (e.g., paragraph-based, sentence-based, character limit)? Why do you think it works well for semantic retrieval?
I implemented sentence-based chunking, which works well for semantic search in Bangla literature. Since Bangla text often contains complete ideas in individual sentences, this strategy maintains the meaning of each chunk while keeping them small enough for accurate vector embedding.

### 3. What embedding model did you use? Why did you choose it? How does it capture the meaning of the text?
I used sentence-transformers/all-MiniLM-L6-v2 from Hugging Face. It's a lightweight, multilingual model that generates context-aware sentence embeddings. Although not fully optimized for Bangla, it provides decent performance. I tested several Hugging Face models; this one performed best locally. Using more powerful models (e.g., OpenAI embeddings) could further improve results but wasn’t feasible due to API usage limits.

### 4. How are you comparing the query with your stored chunks? Why did you choose this similarity method and storage setup?
I used FAISS for storing and searching document embeddings, and cosine similarity to compare user queries with stored chunks. This setup was chosen for its speed and effectiveness in semantic vector matching, especially in resource-constrained environments.

###  5. How do you ensure that the question and the document chunks are compared meaningfully? What would happen if the query is vague or missing context?
Both the question and document chunks are encoded using the same embedding model, ensuring alignment in the vector space. This makes the comparison meaningful. If the query is vague or lacks context, the system may retrieve less relevant results. This could be improved with:
1. Query reformulation
2. Re-ranking the top-k chunks
3. Using an LLM to reason over the retrieved content

### 6. Do the results seem relevant? If not, what might improve them (e.g., better chunking, better embedding model, larger document)?
For most direct and well-phrased questions, results were relevant. However, the system could be improved by:
1. Using Bangla-optimized embeddings
2. Incorporating larger language models
3. Applying more advanced chunking or context windows
4. Improving OCR accuracy with preprocessing
Due to local testing constraints and no paid API access, I used a small-scale model. Still, the framework is extendable for more powerful models and datasets.
