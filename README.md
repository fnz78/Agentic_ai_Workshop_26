**📚 AI Exam Paper Generator using RAG**

(LangChain + FAISS + Groq LLM)

This project is a Retrieval-Augmented Generation (RAG) based AI system that:

• Loads a PDF textbook

• Splits it into meaningful chunks

• Creates semantic vector embeddings

• Stores them in a FAISS vector database

• Retrieves relevant context

• Uses an LLM (via Groq API) to generate exam-style multiple-choice questions

• Built during a hands-on AI workshop using modern LLM tooling.

##🚀 Features##

✅ PDF document loading

✅ Intelligent text chunking

✅ Semantic embeddings using HuggingFace

✅ Vector storage using FAISS

✅ Context-aware question generation

✅ Multiple RetrievalQA chain types (stuff, map_reduce)

✅ Automatic MCQ generation with answers



##🛠️ Tech Stack##

• Python 3.12

• LangChain

• LangChain Community

• LangChain Text Splitters

• FAISS (Vector Database)

• Sentence Transformers

• Groq LLM (LLaMA models)

• PyPDF

• Google Colab

##📦 Installation##

Run the following in Google Colab or your local environment:



Bash

pip install -q langchain-groq

pip install langchain

pip install -U langchain langchain-core langchain-community langchain-text-splitters

pip install sentence-transformers

pip install faiss-cpu

pip install PyPDF

##🔐 API Setup##

Store your Groq API key in Google Colab Secrets.

Load it:


from google.colab import userdata

gkey = userdata.get('GAPI')


Set environment variable:


import os

os.environ["GROQ_API_KEY"] = gkey

📄 Step-by-Step Workflow

1️⃣ Load PDF


from langchain_community.document_loaders import PyPDFLoader

loader = PyPDFLoader("/content/kemh102.pdf")

docs = loader.load()

2️⃣ Split into Chunks


from langchain_text_splitters import RecursiveCharacterTextSplitter

splitter = RecursiveCharacterTextSplitter(

chunk_size=1000,

chunk_overlap=200

)

chunks = splitter.split_documents(docs)

3️⃣ Create Embeddings

from langchain_community.embeddings import HuggingFaceEmbeddings

emb = HuggingFaceEmbeddings(

model_name="sentence-transformers/all-MiniLM-L6-v2"

)

4️⃣ Create FAISS Vector Store


from langchain_community.vectorstores import FAISS

index = FAISS.from_documents(chunks, emb)

retriever = index.as_retriever(search_kwargs={"k": 5})

5️⃣ Similarity Search


results_with_scores = index.similarity_search_with_score(

"relations and functions",

k=5

)

6️⃣ LLM Integration (Groq)


from langchain_groq import ChatGroq

llm = ChatGroq(

model="llama-3.3-70b-versatile",

temperature=0

)

Available models used:

llama-3.3-70b-versatile

llama-3.1-8b-instant



7️⃣ MCQ Generation Prompt Format

The system generates 10 structured multiple-choice questions in strict format:


1. Question text

A. Option text

B. Option text

C. Option text

D. Option text

Answer: Correct option letter

8️⃣ RetrievalQA Chains

Using stuff chain:



from langchain_classic.chains import RetrievalQA

qa_stuff = RetrievalQA.from_chain_type(

llm=llm,

chain_type='stuff',

retriever=retriever

)

Using map_reduce chain:


qa_map_reduce = RetrievalQA.from_chain_type(

llm=llm,

chain_type='map_reduce',

retriever=retriever

)

##🧠 How It Works (RAG Pipeline)##



PDF → Documents

Documents → Text Chunks

Chunks → Embeddings

Embeddings → FAISS Vector Store

User Query → Retrieve Relevant Chunks

Retrieved Context → LLM

LLM → Generates Structured MCQs

This improves accuracy compared to plain prompting because the LLM uses textbook-based context during generation.


##📊 Example Use Cases##

• Generate exam questions from textbooks (e.g., NCERT)

• Create automated test banks

• Build AI-powered study assistants

• Develop EdTech question generation systems

##⚠️ Notes##

HuggingFace authentication is optional for public models.

FAISS runs locally in CPU mode.

Ensure Groq API key is configured properly.

Works best in Google Colab.

📌 Future Improvements

Add Streamlit frontend

Add PDF upload interface

Persist vector database storage

Add difficulty-level control

Generate answer explanations

Export questions to PDF/Docx

👨‍💻 Author

Nazim_fnz77

Created during an AI Workshop as a practical implementation of Retrieval-Augmented Generation using LangChai
