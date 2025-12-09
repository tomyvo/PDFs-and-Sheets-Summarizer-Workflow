# 📚 PDFs and Sheets Summarizer Workflow

Welcome to the **PDFs and Sheets Summarizer** workflow built in **n8n**! This workflow automates the extraction, embedding, and summarization of content from **PDF files** and **Excel spreadsheets** stored in Google Drive, and makes it searchable via a **Supabase Vector Database**. It also allows conversational queries through a **chat agent** integrated with Hugging Face embeddings and OpenRouter language models.

---

## 🌈 Workflow Overview

This workflow consists of the following main parts:

1. **Triggers**  
   - **Google Drive Trigger**: Monitors a specific folder for new PDFs or Excel files.
   - **Google Sheets Trigger**: Watches selected spreadsheets for changes.

2. **File Routing & Extraction**  
   - **Switch Node (`Route by File Type`)**: Directs files based on MIME type (`pdf` or `spreadsheet`).
   - **Extract from PDF**: Extracts text content from PDFs.
   - **Extract from Excel**: Extracts cell content from Excel sheets.

3. **Document Embeddings & Storage**  
   - **Embeddings HuggingFace Inference**: Generates vector embeddings using `sentence-transformers/all-MiniLM-L6-v2`.
   - **Vector Store for PDFs & Sheets**: Stores embeddings in Supabase for semantic search.
   - **Default Data Loader**: Prepares documents for the vector store.

4. **AI Agent & Chat Integration**  
   - **AI Agent**: Specialized in summarizing documents and answering queries.
   - **OpenRouter Chat Model**: Uses `meta-llama/llama-3.3-70b-instruct:free` for natural language understanding.
   - **Postgres Chat Memory**: Keeps conversational memory for context-aware responses.
   - **Supabase Vector Store**: Provides the AI agent with access to embedded documents for semantic search.

---

## 🚀 Features

- **Automatic Document Monitoring**: Continuously watches Google Drive and Sheets for new or updated files.
- **File Type Routing**: Differentiates between PDFs and Excel files for proper extraction.
- **AI-Powered Summarization**: Generates concise, structured summaries highlighting key points and tables.
- **Semantic Search**: Stores embeddings in Supabase to allow fast and intelligent retrieval of relevant content.
- **Conversational Querying**: Users can ask questions about documents via chat, and the AI agent retrieves relevant answers.

---

## 🛠️ Node Details

| Node Name | Purpose | Key Features |
|-----------|---------|-------------|
| **Google Drive Trigger** | Monitors folder for new files | Supports PDFs, Excel (.xls/.xlsx) |
| **Route by File Type** | Switches files to proper extraction | Detects PDF vs spreadsheet |
| **Extract from PDF** | Extracts textual content | Handles multiple pages |
| **Extract from Excel** | Extracts spreadsheet data | Reads all sheets, maintains structure |
| **Embeddings HuggingFace Inference** | Generates vector embeddings | Uses `all-MiniLM-L6-v2` |
| **Supabase Vector Store** | Stores document embeddings | Used by AI agent for semantic search |
| **AI Agent** | Summarizes & answers questions | System prompt ensures professional and concise output |
| **OpenRouter Chat Model** | Handles natural language queries | Uses `LLaMA 3.3-70b instruct` |
| **Postgres Chat Memory** | Keeps conversation context | Allows multi-turn interactions |

---

## 💡 System Prompt for AI Agent

> You are an AI agent specialized in processing and summarizing documents. Your task is to read PDF files and Excel spreadsheets from the connected Google Drive folder, extract their contents, and generate clear, concise summaries. Always structure your output in a way that is easy to understand, highlighting key information, tables, or data points when relevant. Do not include unnecessary details, and do not guess when information is missing or unclear — instead, politely indicate that the content could not be fully interpreted. Keep your tone professional yet approachable, suitable for business or academic contexts.

---

## 📊 Supabase Vector Database

- Stores embeddings of all PDFs and Sheets.
- **AI agent must use this database** for all semantic search and retrieval.
- Each entry corresponds to a section, table, or key content from the original document.
- Encoded in vector form to support fast and contextual queries.

---

## ⚡ Setup Instructions

1. **Connect Google Drive & Sheets**:  
   - Provide OAuth2 credentials in n8n for access.

2. **Supabase Setup**:  
   - Create a `documents` table with `pgvector` extension.
   - Ensure vector dimensions match Hugging Face model (384 for `all-MiniLM-L6-v2`).

3. **Hugging Face Integration**:  
   - Add Hugging Face API credentials in n8n.
   - Select `all-MiniLM-L6-v2` as the embeddings model.

4. **OpenRouter Model**:  
   - Configure OpenRouter API credentials.
   - Model: `meta-llama/llama-3.3-70b-instruct:free`.

5. **Enable Workflow**:  
   - Activate workflow in n8n to start monitoring and processing files.

---

## 🎨 Notes

- Optimized for **fast semantic search and summarization**.
- Scales for multiple PDFs and large spreadsheets.
- Conversational interface allows querying past documents effortlessly.
- Fully compatible with n8n nodes for LangChain, Hugging Face, OpenRouter, and Supabase.

---

## 📌 References

- [n8n Docs](https://docs.n8n.io/)  
- [Hugging Face Models](https://huggingface.co/models)  
- [Supabase Vector Database](https://supabase.com/docs/guides/database/vectors)  
- [OpenRouter AI Models](https://openrouter.ai/)  

---

## 🌟 License

MIT License – free to use and adapt for personal or commercial workflows.
