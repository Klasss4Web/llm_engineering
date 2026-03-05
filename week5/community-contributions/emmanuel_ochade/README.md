# Runbook RAG Chat

A **RAG (Retrieval-Augmented Generation) chat** over internal runbook / how-to documents. Ask questions in natural language and get answers grounded in the knowledge base. Built **without LangChain**: OpenAI embeddings, ChromaDB, and OpenAI chat only.

## What’s different

- **Topic:** Runbooks and ops how-tos (deploy, backup, restart services), not medical, legal, or travel.
- **Stack:** No LangChain. Direct use of `openai` and `chromadb` for ingest and retrieval, then OpenAI chat with injected context.
- **Single notebook:** Ingest, embed, store, and chat are all in `runbook_rag_chat.ipynb`.

## Requirements

- Python 3.10+
- `OPENROUTER_API_KEY` in `.env`
- Dependencies are installed in the notebook (first cell: `!pip install openai chromadb python-dotenv gradio`). No separate `requirements.txt` needed.

## Knowledge base

Place Markdown runbooks in `knowledge_base/`. The notebook loads all `*.md` files, chunks them, embeds with OpenAI, and stores in a local Chroma persistence directory.

## How to run

1. Add or edit `.md` files in `knowledge_base/`.
2. Open `runbook_rag_chat.ipynb` and run all cells (ingest + embed once, then use the Gradio chat).
3. Ask e.g. “How do I restart the API?” or “What’s the backup procedure?”

## Layout

- `knowledge_base/` – Markdown runbooks (included).
- `runbook_rag_chat.ipynb` – Load, chunk, embed, Chroma, RAG chat UI.
- `chroma_runbooks/` – Created by the notebook (Chroma persistence).
