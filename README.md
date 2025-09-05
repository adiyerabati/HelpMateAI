# 🚀 HelpMateAI – Building an Effective Generative Search System (RAG)

This project demonstrates how to build an **effective generative search system** using **Retrieval-Augmented Generation (RAG)**. The system is designed to interpret and answer queries from a **comprehensive life insurance policy document**.

---

## 📌 1. Project Overview
The project focuses on **designing a robust RAG-based search pipeline** capable of:
- Understanding large and complex documents (insurance policies).
- Accurately retrieving relevant content.
- Generating **clear, contextual, and reliable answers**.

---

## 🎯 2. Objective
The primary goal is to create a **search + generation system** that:
- Interprets user queries in natural language.  
- Retrieves the **most relevant sections** from the policy.  
- Produces **well-structured, cited answers**.  

---

## 📑 3. Reference Document
We use the following policy file for this implementation:  
📄 **[Principal-Sample-Life-Insurance-Policy.pdf]**

---

## 🛠️ 4. Methodology
The solution is structured into **three core layers**, each optimized for performance and accuracy.

### 🔹 a. Embedding Layer
- **Preprocessing & Cleaning:** Extract and normalize text from PDFs.  
- **Chunking Strategy:**  
  - Fixed-size chunking (baseline).  
  - Explore semantic or sliding-window chunking for improved retrieval.  
- **Embedding Models:**  
  - [`all-MiniLM-L6-v2`](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2) (SentenceTransformers).  
  - OpenAI Embeddings as an alternative.  

### 🔹 b. Search Layer
- **Query Embedding:** Convert user queries into embedding space.  
- **Vector Store:** Store embeddings in **ChromaDB** for fast similarity search.  
- **Query Efficiency:** Add a **caching mechanism** to speed up repeated queries.  
- **Re-ranking:** Apply a **cross-encoder model** to ensure top results are **highly relevant**.  

### 🔹 c. Generation Layer
- **Prompt Engineering:**  
  - Construct prompts that include **retrieved context**.  
  - Define clear system instructions for structured answers.  
- **Few-Shot Examples (Optional):** Add examples to improve consistency.  
- **LLM Integration:** Use **GPT-3.5 (or higher)** for final answer generation.  
- **Citations:** Provide answers with **document references** for transparency.  

---

## 🏗️ 5. System Components
- 📖 **PDF Processing:** Use `pdfplumber` to extract text, tables, and structured data.  
- ✂️ **Document Chunking:** Fixed-size (baseline) + explore smarter chunking strategies.  
- 🔎 **Embedding Generation:** SentenceTransformers (`all-MiniLM-L6-v2`).  
- 📦 **ChromaDB Storage:** Efficient embedding storage & retrieval.  
- ⚡ **Semantic Search + Cache:** Faster query responses with caching.  
- 🎯 **Re-Ranking:** Cross-encoder model for precise results.  
- 🤖 **RAG Pipeline:** GPT-3.5 + structured prompt + retrieved context.  

---

## 🏛️ 6. System Architecture
```mermaid
flowchart TD
    A[📄 Insurance Policy PDF] --> B[📖 PDF Processing (pdfplumber)]
    B --> C[✂️ Document Chunking]
    C --> D[🔎 Embedding Generation (SentenceTransformers)]
    D --> E[📦 ChromaDB Vector Store]

    Q[❓ User Query] --> Q1[🔎 Query Embedding]
    Q1 --> E
    E --> F[📂 Retrieved Chunks]
    F --> R[🎯 Re-Ranking (Cross-Encoder)]

    R --> G[📝 Prompt Construction]
    G --> H[🤖 GPT-3.5 Generation]
    H --> A1[✅ Final Answer w/ Citations]
