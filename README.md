# 📜 Constitutional RAG

A Retrieval-Augmented Generation (RAG) system specifically optimized for querying, analyzing, and retrieving information from constitutional law (e.g., the 1996 Constitution). 

Unlike standard RAG pipelines, this project is engineered for **strict legal accuracy**, utilizing metadata-aware chunking, hierarchical retrieval, and rigorous evaluation to prevent hallucinations and ensure precise citation of legal clauses.

## ✨ Features

- **Metadata-Aware Ingestion:** Parses document structure to attach granular metadata (Chapter, Section, Article) to every text chunk.
- **Hierarchical Retrieval:** Implements Parent-Child (Small-to-Big) chunking to ensure precise vector search while providing the LLM with full contextual clauses.
- **Metadata Filtering:** Allows users to restrict queries to specific parts of the constitution (e.g., "What does Chapter 2 say about...").
- **Strict Evaluation Pipeline:** Built-in evaluation framework using [RAGAS / TruLens] to measure faithfulness, context precision, and answer relevance.
- **Local Vector Persistence:** Saves embedded vectors locally to avoid re-processing the document on every run.

## 🛠️ Tech Stack

- **Language:** Python 3.10+
- **RAG Framework:** [LangChain / LlamaIndex]
- **Vector Database:** [ChromaDB / FAISS / Pinecone]
- **LLM / Embeddings:** [OpenAI (gpt-4o / text-embedding-3-small) / Local HuggingFace models]
- **Document Parsing:** [PyMuPDF / pdfplumber / LlamaParse]
- **UI (Optional):** [Streamlit / Gradio]

## 📂 Project Structure

```text
constitutional-rag/
├── .env                      # API keys and environment variables
├── .gitignore                
├── config.py                 # Centralized settings (chunk sizes, models, paths)
├── requirements.txt          
├── README.md
│
├── data/
│   ├── raw/                  # Original PDFs (e.g., constitution_1996.pdf)
│   └── processed/            # Saved chunks/metadata (JSON/Parquet)
│
├── vector_store/             # Persisted local Vector DB
│
├── notebooks/                # Jupyter notebooks for experimentation
│   ├── 01_experiment_chunking.ipynb
│   └── 02_experiment_prompts.ipynb
│
├── src/
│   ├── ingestion.py          # PDF parsing, text cleaning, chunking, embedding
│   ├── retriever.py          # Vector search, reranking, metadata filtering
│   ├── generator.py          # LLM prompting, response synthesis
│   └── utils.py              # Helper functions and logging setup
│
├── eval/                     
│   ├── eval_dataset.json     # Ground truth Q&A pairs for testing
│   └── run_evaluation.py     # Script to score retrieval & generation
│
├── tests/                    # Unit tests for pipeline components
│   ├── test_ingestion.py
│   └── test_retrieval.py
│
└── logs/                     # Application and LLM call logs
