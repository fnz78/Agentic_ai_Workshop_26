

***

# 📚 AI Exam Paper Generator using RAG
### (LangChain + FAISS + Groq LLM)

This project is a **Retrieval-Augmented Generation (RAG)** based AI system designed to automate the creation of exam papers. It processes PDF textbooks, indexes their content, and uses Large Language Models (LLMs) to generate context-aware multiple-choice questions (MCQs).

Built during a hands-on AI workshop (Agentic_ai_Workshop_26), this tool demonstrates a full RAG pipeline using modern LLM orchestration.

---

## 🚀 Features

- ✅ **PDF Document Loading:** Extracts text from educational materials.
- ✅ **Intelligent Text Chunking:** Breaks down long chapters into manageable segments.
- ✅ **Semantic Embeddings:** Uses HuggingFace transformers for high-quality vector representations.
- ✅ **Vector Storage:** Efficient similarity search using FAISS.
- ✅ **Context-Aware Generation:** Ensures questions are grounded in the provided textbook.
- ✅ **Advanced RAG Chains:** Supports both `stuff` and `map_reduce` retrieval chains.
- ✅ **Structured Output:** Automatically generates 10 MCQs with correct answer keys.

---

## 🛠️ Tech Stack

- **Language:** Python 3.12
- **Framework:** [LangChain](https://www.langchain.com/)
- **LLM:** [Groq](https://groq.com/) (LLaMA 3.3-70b & 3.1-8b)
- **Vector Database:** FAISS (CPU)
- **Embeddings:** HuggingFace (`sentence-transformers/all-MiniLM-L6-v2`)
- **PDF Parsing:** PyPDF
- **Environment:** Google Colab

---

## 📦 Installation

Run the following commands to set up the environment:

```bash
pip install -q langchain-groq langchain langchain-core langchain-community langchain-text-splitters
pip install -q sentence-transformers faiss-cpu PyPDF
```

---

## 🔐 API Setup

This project uses the **Groq API** for high-speed inference. If using Google Colab, store your key in the "Secrets" tab.

```python
import os
from google.colab import userdata

# Load Groq API Key
os.environ["GROQ_API_KEY"] = userdata.get('GAPI')
```

---

## 📄 Step-by-Step Workflow

### 1. Load PDF & Split into Chunks
```python
from langchain_community.document_loaders import PyPDFLoader
from langchain_text_splitters import RecursiveCharacterTextSplitter

loader = PyPDFLoader("/content/kemh102.pdf")
docs = loader.load()

splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=200)
chunks = splitter.split_documents(docs)
```

### 2. Create Embeddings & FAISS Index
```python
from langchain_community.embeddings import HuggingFaceEmbeddings
from langchain_community.vectorstores import FAISS

emb = HuggingFaceEmbeddings(model_name="sentence-transformers/all-MiniLM-L6-v2")
index = FAISS.from_documents(chunks, emb)
retriever = index.as_retriever(search_kwargs={"k": 5})
```

### 3. LLM Integration (Groq)
```python
from langchain_groq import ChatGroq

llm = ChatGroq(model="llama-3.3-70b-versatile", temperature=0)
```

### 4. RetrievalQA Chains
```python
from langchain.chains import RetrievalQA

# Using the 'stuff' chain type
qa_chain = RetrievalQA.from_chain_type(llm=llm, chain_type='stuff', retriever=retriever)
```

---

## 🧠 How It Works (RAG Pipeline)

1. **Ingestion:** PDF is converted into Document objects.
2. **Chunking:** Documents are split to fit LLM context windows.
3. **Embedding:** Text is converted into mathematical vectors.
4. **Storage:** Vectors are stored in **FAISS** for fast retrieval.
5. **Retrieval:** The system finds the 5 most relevant chunks based on a user query.
6. **Generation:** The LLM uses the retrieved context to generate MCQs in a strict format:
   - Question
   - Options A, B, C, D
   - Correct Answer

---

## 📊 Example Use Cases

- **Automated Test Banks:** Create thousands of questions for EdTech platforms.
- **Study Assistant:** Generate self-assessment quizzes from personal notes.
- **NCERT/Textbook Processing:** Specifically tuned for academic textbook structures.

---

## 📌 Future Improvements

- [ ] **Frontend:** Add a Streamlit or Gradio interface for easy uploads.
- [ ] **Export:** Enable downloading generated questions as PDF or Docx.
- [ ] **Persistence:** Save FAISS indexes locally to avoid re-processing.
- [ ] **Complexity Control:** Add a toggle for Difficulty Level (Easy, Medium, Hard).
- [ ] **Explanations:** Generate a detailed rationale for why an answer is correct.

---

## 👨‍💻 Author

**Nazim_fnz77**  
Created as a practical implementation of Agentic RAG during the **Agentic AI Workshop 26**.

---
