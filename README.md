*# 📚 AI Exam Paper Generator using RAG
### (LangChain + FAISS + Groq LLM)

This project is a **Retrieval-Augmented Generation (RAG)** based AI system designed to transform standard PDF textbooks into structured exam papers. It leverages semantic search to retrieve context and an LLM to formulate accurate Multiple Choice Questions (MCQs).



---

## 🚀 Features
* **PDF Document Loading:** Seamlessly ingest textbook content.
* **Intelligent Text Chunking:** Optimized splitting for better context retention.
* **Semantic Embeddings:** Powered by HuggingFace (`all-MiniLM-L6-v2`).
* **Vector Storage:** High-performance retrieval using **FAISS**.
* **Context-Aware Generation:** Uses Groq API (LLaMA 3.3/3.1) for hallucination-free questions.
* **Flexible QA Chains:** Supports `stuff` and `map_reduce` chain types.
* **Structured Output:** Automatic MCQ generation with answers.

---

## 🛠️ Tech Stack
* **Language:** Python 3.12
* **Orchestration:** LangChain
* **Vector DB:** FAISS (CPU)
* **LLM Gateway:** Groq Cloud
* **Models:** LLaMA-3.3-70b-versatile, LLaMA-3.1-8b-instant
* **Environment:** Google Colab / Local Python

---

## 📦 Installation

Run the following commands to set up your environment:

bash

pip install -q langchain-groq langchain langchain-core \
langchain-community langchain-text-splitters \
sentence-transformers faiss-cpu PyPDF


##🔐 API Setup

​This project requires a Groq API Key. 
If using Google Colab, store it in "Secrets" under the name GAPI.
