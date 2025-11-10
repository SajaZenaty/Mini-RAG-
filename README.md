#Building RAG system - HW2
---

### 🏗️ Overview

When working with **Question Answering (QA)** systems 🤖, a common challenge arises when the model encounters questions it has **not seen during training**. In such cases, the model may produce:

- ❌ **Hallucinated answers** — fabricated or incorrect responses
    
- ⏳ **Outdated answers** — information that was true during training but is no longer accurate
    

To address this issue, we can use **RAG (Retrieval-Augmented Generation)** — a hybrid approach that combines **information retrieval** and **language generation**.

---

### 🔎 What is RAG?

**RAG (Retrieval-Augmented Generation)** enables a model to **search for and retrieve relevant knowledge** from external sources — such as **Wikipedia, custom databases, or document collections** — before generating an answer.

This allows the model to answer **unseen, knowledge-intensive questions** more accurately and transparently.

RAG consists of two main components:

---

### 1️⃣ Retriever Component 🔍

The **Retriever** is responsible for finding the most relevant documents related to the user’s query.

**How it works:**

- Converts both the **question** and the **documents** into **vector embeddings** (numerical representations).
    
- Measures **semantic similarity** between these embeddings using **cosine similarity**.
    
- Returns the **Top-K most relevant documents** as context for the Generator.
    

**Model Used:**  
👉 `sentence-transformers/all-MiniLM-L6-v2`  
This is a lightweight and efficient transformer model optimized for **semantic similarity** and **retrieval tasks**.

---

### 2️⃣ Generator Component ✍️

The **Generator** uses the retrieved context to **produce a natural-language answer** that is accurate and coherent.

**How it works:**

- Takes the **question** and the **retrieved documents** as input.
    
- Generates a **context-aware answer** using a fine-tuned QA model.
    

**Model Used:**  
👉 `distilbert-base-cased-distilled-squad`  
This is a distilled version of BERT fine-tuned on the **SQuAD dataset** for **extractive question answering**, making it efficient yet powerful.

---

### ⚙️ Implementation Steps

#### Step 1: Load Models and Knowledge Base

- Load the **Retriever model** (`all-MiniLM-L6-v2`) to embed questions and documents.
    
- Load the **Generator model** (`distilbert-base-cased-distilled-squad`) for answer generation.
    
- Prepare the **knowledge base** — a collection of text documents that the retriever will search.
    

#### Step 2: Encode the Knowledge Base

    
- Use the retriever model to **encode** knowledge Base into vector embeddings.
    
    

#### Step 3: Query Processing

- When a user asks a question:
    
    1. Encode the question using the **Retriever model**.
        
    2. Compare it with the stored embeddings using **cosine similarity**.
        
    3. Select the **Top-K most similar documents**.
        

#### Step 4: Generate the Answer

- Pass both the **question** and the **retrieved text** to the **Generator model**.
    
- The generator produces a **contextually grounded answer**, minimizing hallucination.
    

---


