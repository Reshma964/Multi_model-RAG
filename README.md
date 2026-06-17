# Multi_model-RAG
# Multimodal RAG System

A Multimodal Retrieval-Augmented Generation (RAG) pipeline that extracts text and images from PDF documents, generates semantic summaries, stores them in a vector database, retrieves relevant information using embeddings and reranking, and generates accurate answers to user queries.

## Features

* PDF document ingestion
* Text extraction and chunking using Docling
* Image extraction from PDFs
* AI-powered text summarization
* AI-powered image understanding and description
* Vector storage using ChromaDB
* Semantic search with embeddings
* Reranking using CrossEncoder
* Context-aware question answering
* Support for multimodal retrieval (text + images)

---

## Architecture

```text
PDF Document
      │
      ▼
  Docling Parser
      │
 ┌────┴────┐
 ▼         ▼
Text     Images
 │          │
 ▼          ▼
Chunking  Image Captioning
 │          │
 ▼          ▼
Text Summaries
      │
      ▼
 LangChain Documents
      │
      ▼
 Embedding Model
      │
      ▼
   ChromaDB
      │
      ▼
 Retriever (MMR)
      │
      ▼
 CrossEncoder Reranker
      │
      ▼
 Context Builder
      │
      ▼
     LLM
      │
      ▼
 Final Answer
```

---

## Tech Stack

### Document Processing

* Docling
* HybridChunker

### Embeddings

* MixedBread Embeddings

  * `mixedbread-ai/mxbai-embed-large-v1`

### Vector Database

* ChromaDB

### Reranking

* BAAI Cross Encoder

  * `BAAI/bge-reranker-large`

### Vision Model

* Gemini 2.5 Flash

### LLM

* Ollama (Llama 3)
* Custom API-based text generation endpoint

### Frameworks

* LangChain
* Hugging Face Transformers

---

## Installation

Clone the repository:

```bash
git clone https://github.com/yourusername/multimodal-rag.git
cd multimodal-rag
```

Install dependencies:

```bash
pip install google-generativeai
pip install pillow
pip install langchain-chroma
pip install langchain-core
pip install langchain-huggingface
pip install langchain-text-splitters
pip install sentence-transformers
pip install transformers
pip install docling
pip install chromadb
pip install ollama
```

---

## Workflow

### 1. Parse PDF

The PDF is processed using Docling.

```python
converter = DocumentConverter(...)
doc = converter.convert("document.pdf")
```

### 2. Extract Content

* Text blocks
* Images

### 3. Generate Summaries

Text chunks are summarized using an LLM.

```python
summary = summarize_chunk(chunk.text)
```

Images are converted into rich semantic descriptions.

```python
summary = summarize_image(image)
```

### 4. Create Documents

Summaries are stored as LangChain documents.

```python
Document(
    page_content=summary,
    metadata={"type": "text"}
)
```

### 5. Generate Embeddings

```python
embeddings = HuggingFaceEmbeddings(
    model_name="mixedbread-ai/mxbai-embed-large-v1"
)
```

### 6. Store in ChromaDB

```python
vectorstore.add_documents(documents)
```

### 7. Retrieve Relevant Content

```python
retriever = vectorstore.as_retriever(
    search_type="mmr"
)
```

### 8. Rerank Results

```python
reranker = CrossEncoder(
    "BAAI/bge-reranker-large"
)
```

### 9. Build Context

```python
context = build_context(query)
```

### 10. Generate Final Answer

```python
answer = ask("Your question")
```

---

## Example Query

```python
answer = ask(
    "What is the problem statement?"
)

print(answer)
```

---

## Project Structure

```text
multimodal-rag/
│
├── notebooks/
│   └── Multimodal_RAG.ipynb
│
├── chroma_mragdb/
│   └── Vector Database
│
├── data/
│   └── PDF Documents
│
├── README.md
│
└── requirements.txt
```

---

## Future Improvements

* OCR support for scanned PDFs
* Multi-PDF retrieval
* Source citation generation
* Streaming responses
* Hybrid keyword + vector search
* Evaluation pipeline
* Web UI using Streamlit or Gradio
* Support for audio and video documents

---

## Use Cases

* Research paper search
* Enterprise knowledge bases
* Technical documentation assistants
* Educational content retrieval
* Legal and compliance document search
* Multimodal document question answering

---

## License

This project is released under the MIT License.

---

## Author

Developed as a Multimodal RAG pipeline using Docling, LangChain, ChromaDB, Gemini, and Ollama.
