# 🤖 RAG Agent with n8n – Intelligent Q&A System on Documents

[![n8n](https://img.shields.io/badge/n8n-Workflow-FF6D6D?style=flat-square&logo=n8n)](https://n8n.io/)
[![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20DB-DC382C?style=flat-square&logo=qdrant)](https://qdrant.tech/)
[![OpenAI](https://img.shields.io/badge/OpenAI-GPT--4o%20mini-412991?style=flat-square&logo=openai)](https://openai.com/)
[![Node.js](https://img.shields.io/badge/Node.js-18+-339933?style=flat-square&logo=node.js)](https://nodejs.org/)

A complete RAG (Retrieval-Augmented Generation) system built with n8n to automatically index your documents and intelligently answer questions with source citations.

## 📚 Table of Contents

1. [Features](#-features)
2. [Architecture](#-architecture)
3. [Quick Installation](#-quick-installation)
4. [Configuration](#-configuration)
5. [Usage](#-usage)
6. [Project Structure](#-project-structure)
7. [Detailed Workflow](#-detailed-workflow)
8. [Customization](#-customization)
9. [Troubleshooting](#-troubleshooting)
10. [Metrics & Performance](#-metrics--performance)
11. [Contribution](#-contribution)
12. [License](#-license)
13. [Acknowledgments](#-acknowledgments)
14. [Support](#-support)


## 🎯 Features

- **Automatic ingestion** of documents (PDF, TXT, DOCX, MD, Java, XML)
- **Semantic search** using a Qdrant vector database
- **Smart chat** with automatic source citations
- **Built-in conversational interface**
- **Conversation memory** for persistent context
- **Multi-document analysis** with cross-referencing

## 🏗️ Architecture


```
📁 Local Documents
    ↓
🔄 n8n Ingestion Workflow
    ↓
🗃️ Qdrant Vector Store
    ↓
💬 Chat Interface
    ↓
🤖 RAG Agent + OpenAI GPT-4o mini
```


## 🚀 Quick Installation

### Prerequisites

- Node.js 18+ ([Download](https://nodejs.org/))
- [Qdrant Cloud](https://cloud.qdrant.io/) account (free)
- [OpenAI API Key](https://platform.openai.com/api-keys)

### Installation Steps

1. **Install n8n**
   ```bash
   npm install -g n8n
   ```

2. **Clone this repository**
   ```bash
   git clone https://github.com/your-username/rag-agent-n8n.git
   cd rag-agent-n8n
   ```

3. **Start n8n**
   ```bash
   n8n
   ```
   Then type `o` to open in the browser (http://localhost:5678)

4. **Import the workflow**
   - Go to Workflows → + New Workflow
   - Click on "Import from File"
   - Select `rag_agent.json`
   - Save

## ⚙️ Configuration

### 1. Configure Qdrant

1. Create an account on [Qdrant Cloud](https://cloud.qdrant.io/)
2. Generate an API key
3. Create a collection with:
   - **Name**: `test_rag` (or any name you prefer)
   - **Dimensions**: `1536`
   - **Metric**: `cosine`

### 2. Configure credentials in n8n

**OpenAI API:**
- Name: `OpenAi account`
- API Key: Your OpenAI key

**Qdrant API:**
- Name: `QdrantApi account`
- API Key: Your Qdrant key
- URL: Your Qdrant cluster URL

### 3. Customize document paths

In the "Read/Write Files from Disk" node, change:
```
D:/Stage_Talan_2025/fist-tast-documentation-master/**/*.*
```
To your own document folder:
```
/path/to/your/documents/**/.
```


## 📖 Usage

### 1. Index your documents

1. Place your documents in the configured folder
2. Click "Execute Workflow" in the ingestion workflow
3. Wait for indexing to finish

### 2. Use the chat

1. Activate the main workflow
2. Open the chat interface (generated webhook)
3. Ask your questions!

### Example Conversation

```
🧑 Question : "Comment configurer l'API Qdrant ?"

🤖 Réponse : Pour configurer l'API Qdrant, vous devez :

1. **Create an API Key**
   Log in to your Qdrant account and go to the API Keys section.

2. **Create a collection**
   - Name: according to your project
   - Dimensions: 1536 (OpenAI compatible)
   - Metric: cosine

**Sources :**
- File: rag.pdf | Chunk: chunk_123 | Score: 0.95
```

## 📁 Project Structure

```
rag-agent-n8n/
├── README.md # This file
├── rag_agent.json # Main n8n workflow
├── guide_rag_agent/ # Detailed guide
├── LICENSE/
└── .gitignore
```


## 🛠️ Detailed Workflow

### Part 1: Document Ingestion
- **Read Files** → Recursively reads documents
- **Switch** → Filters by file type
- **Extract** → Extracts text content
- **Token Splitter** → Splits into chunks
- **Embeddings** → Converts to vectors
- **Qdrant Store** → Stores vectors in database

### Part 2: Chat and Responses
- **Chat Trigger** → Receives chat messages
- **AI Agent** → Smart orchestration
- **Vector Search** → Semantic search
- **OpenAI Model** → Generates answers
- **Memory** → Maintains conversation context

## 🎨 Customization

### Modify the system prompt

In the "AI Agent" node, you can customize the system message:
```
You are an AI assistant specialized in [YOUR DOMAIN]...
```


### Add new file types

In the "Switch" node, add new conditions for other extensions.

## 🔧 Troubleshooting

### Common Issues

**❌ File read error**
- Check absolute paths (use `/` instead of `\`)
- Ensure file access permissions

**❌ Qdrant connection failed**
- Check your API key
- Confirm the collection exists
- Test network connectivity

**❌ No chat response**
- Ensure indexing is complete
- Check n8n logs for errors
- Confirm OpenAI API is working

## 📊 Metrics & Performance

- **Chunk size**: 800 tokens (customizable)
- **Overlap**: 100 tokens
- **Result limit**: 4 documents per query
- **Model**: GPT-4o mini (cost-effective)

## 🤝 Contribution

Contributions are welcome! Here's how to participate:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to your branch (`git push origin feature/new-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [n8n](https://n8n.io/) for the automation platform
- [Qdrant](https://qdrant.tech/) for the vector database
- [OpenAI](https://openai.com/) for the language models

## 📞 Support

If you encounter issues:

1. Refer to the [complete guide](rag_agent_guide.pdf)
---

⭐ **Don't forget to give a star if this project helps you!**
