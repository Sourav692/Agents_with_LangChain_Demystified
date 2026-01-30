<div align="center">

# 🔗 LangChain Demystified

### *A Comprehensive Guide to Mastering LangChain for AI Engineering*

[![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![LangChain](https://img.shields.io/badge/LangChain-0.3.x-1C3C3C?style=for-the-badge&logo=langchain&logoColor=white)](https://langchain.com)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-412991?style=for-the-badge&logo=openai&logoColor=white)](https://openai.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=for-the-badge)](https://opensource.org/licenses/MIT)

---

*From fundamental concepts to production-ready AI agents — everything you need to build intelligent LLM-powered applications.*

[Getting Started](#-getting-started) •
[Concepts](#-concepts) •
[Projects](#-real-world-projects) •
[AI Agents](#-building-ai-agents) •
[Contributing](#-contributing)

</div>

---

## 📖 Overview

**LangChain Demystified** is a comprehensive educational repository designed to take you from LangChain beginner to proficient AI engineer. This repository covers both basic and advanced concepts through hands-on Jupyter notebooks, real-world projects, and production-ready architectures.

Whether you're looking to understand prompt engineering, build conversational AI systems, implement RAG (Retrieval-Augmented Generation) pipelines, or deploy microservice-based LLM applications — this repository has you covered.

---

## ✨ Features

| Category | What You'll Learn |
|----------|------------------|
| 🎯 **Fundamentals** | LLM APIs, Prompt Templates, Chains, Memory Systems |
| 🧠 **Advanced Concepts** | LCEL, Runnables, Streaming, Caching, Callbacks |
| 🔍 **RAG & Search** | Vector Databases, Embeddings, Hybrid Search, Indexing APIs |
| 🤖 **AI Agents** | Tool Calling, ReAct Pattern, Multi-User Agents, Text-to-SQL |
| 🏗️ **Production** | Microservices, Kubernetes, LangSmith Tracing |
| 🛠️ **Projects** | 11+ Real-world Applications |

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10 or higher
- Jupyter Notebook or JupyterLab
- API keys for LLM providers (OpenAI, Google, Groq, HuggingFace)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/LangChain_Demystified.git
   cd LangChain_Demystified
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   OPENAI_API_KEY=your_openai_api_key
   GOOGLE_API_KEY=your_google_api_key
   GROQ_API_KEY=your_groq_api_key
   HUGGINGFACEHUB_API_TOKEN=your_hf_token
   LANGCHAIN_API_KEY=your_langsmith_api_key
   ```

5. **Launch Jupyter**
   ```bash
   jupyter notebook
   ```

---

## 📁 Repository Structure

```
LangChain_Demystified/
│
├── LangChain_Fundamentals/             # 📚 Core LangChain Curriculum (56 notebooks)
│   │
│   ├── 01_Getting_Started/             # Introduction & LLM Providers (8 notebooks)
│   │   ├── 1.0_LangChain_Introduction.ipynb
│   │   ├── 1.1_Commercial_LLMs_Natively.ipynb
│   │   ├── 1.2_Commercial_LLMs_with_LangChain.ipynb
│   │   ├── 1.3_Open_Source_LLMs_HF_Transformers.ipynb
│   │   ├── 1.4_Open_Source_LLMs_HF_Inference_Client.ipynb
│   │   ├── 1.5_Open_Source_LLMs_Groq_Cloud.ipynb
│   │   ├── 1.6_Open_Source_LLMs_with_LangChain.ipynb
│   │   └── 1.7_OpenAI_API_Basics.ipynb
│   │
│   ├── 02_Inputs_Outputs_Prompts/      # I/O & Prompt Engineering (6 notebooks)
│   │   ├── 2.1_LangChain_Inputs_and_Outputs.ipynb
│   │   ├── 2.2_Prompt_Templates.ipynb
│   │   ├── 2.3_LLM_vs_ChatModel.ipynb
│   │   ├── 2.4_PromptTemplate_with_LangChain.ipynb
│   │   ├── 2.5_Output_Parser.ipynb
│   │   └── 2.6_LangChain_LLM_Input_Output_Comprehensive.ipynb
│   │
│   ├── 03_LCEL/                        # LangChain Expression Language (7 notebooks)
│   │   ├── 3.0_LCEL_Essentials.ipynb
│   │   ├── 3.1_LCEL_Introduction.ipynb
│   │   ├── 3.2_Runnables.ipynb
│   │   ├── 3.3_LCEL_Deepdive.ipynb
│   │   ├── 3.4_LCEL_and_Runnables.ipynb
│   │   ├── 3.5_Chain_Migrations.ipynb
│   │   └── 3.6_Chain_Migration_Advanced.ipynb
│   │
│   ├── 04_Chains/                      # Chain Compositions (4 notebooks)
│   │   ├── 4.0_Basics_of_Chains.ipynb
│   │   ├── 4.1_Chains_Basics_and_OutputParsers.ipynb
│   │   ├── 4.2_Advanced_Chains.ipynb
│   │   └── 4.3_Branching_Routing_Merging_Chains.ipynb
│   │
│   ├── 05_Memory/                      # Conversation Memory Systems (9 notebooks)
│   │   ├── 5.0_Memory_Essentials.ipynb
│   │   ├── 5.1_Chat_Message_Memory.ipynb
│   │   ├── 5.2_Introduction_Conversation_Chain.ipynb
│   │   ├── 5.3_Conversation_Chains_Memory_LCEL.ipynb
│   │   ├── 5.4_Multi_User_InMemory_Storage.ipynb
│   │   ├── 5.5_Multi_User_SQL_Persistent_Storage.ipynb
│   │   ├── 5.6_ConversationQA.ipynb
│   │   ├── 5.7_Memory_Another_Example.ipynb
│   │   └── 5.8_Memory_Code.ipynb
│   │
│   ├── 06_Tools_and_Functions/         # Tool Calling (4 notebooks)
│   │   ├── 6.0_Tools_Functions_Essentials.ipynb
│   │   ├── 6.1_Tool_Calling_LangChain.ipynb
│   │   ├── 6.2_Tool_Calling_Agents.ipynb
│   │   └── 6.3_OpenAI_Tool_Calling.ipynb
│   │
│   ├── 07_RAG/                         # Retrieval-Augmented Generation (4 notebooks)
│   │   ├── 7.0_RAG_Essentials.ipynb
│   │   ├── 7.1_RAG_Comprehensive.ipynb
│   │   ├── 7.2_Filtered_Search.ipynb
│   │   └── 7.3_Indexing_API.ipynb
│   │
│   ├── 08_Summarization/               # Text Summarization (2 notebooks)
│   │   ├── 8.0_Summarization_Essentials.ipynb
│   │   └── 8.1_Text_Summarization.ipynb
│   │
│   ├── 09_Advanced_Features/           # Production Features (6 notebooks)
│   │   ├── 9.0_Advanced_LangChain.ipynb
│   │   ├── 9.1_LLM_Cost_Monitoring.ipynb
│   │   ├── 9.2_Caching.ipynb
│   │   ├── 9.3_Streaming.ipynb
│   │   ├── 9.4_Moderating_Chains.ipynb
│   │   └── 9.5_Callbacks.ipynb
│   │
│   ├── 10_Agents/                      # Building Agents (1 notebook)
│   │   └── 10.1_Agents.ipynb
│   │
│   ├── 11_LangSmith/                   # Tracing & Evaluation (1 notebook)
│   │   └── 11.1_LangSmith_Basics.ipynb
│   │
│   ├── 12_MicroServices/               # Production Deployment
│   │   └── (Docker, Kubernetes, FastAPI templates)
│   │
│   └── _Archive/                       # Deprecated/Duplicate files
│       ├── Deprecated/
│       ├── Duplicates/
│       └── Miscellaneous/
│
├── 3. Simple_Projects_with_LangChain/  # Real-world Applications (11+ projects)
│   ├── 1. Create a Review Analyst.ipynb
│   ├── 2. Create Research Paper Analyst.ipynb
│   ├── 3. Create Social Media Marketing Analyst.ipynb
│   ├── 4. IT Support Analyst.ipynb
│   ├── 5. Building a Customer Support Workflow.ipynb
│   ├── 6. Building a Report Generator.ipynb
│   ├── 7. Building a Customer Review Analyst.ipynb
│   ├── 8. Build a Multi-user Conversational Product Recommendation Agent.ipynb
│   ├── 9. Study Assistant for Quiz Question Generation.ipynb
│   ├── 10. chat_stream.py
│   └── 11. project_custom_chatgpt_with_langchain_from_scratch.ipynb
│
├── 4. AI_Agents_with_LangChain/        # Advanced Agent Development
│   ├── Module 1/                       # Agent Tools & Tool Calling
│   ├── Module 2/                       # Agentic AI Research Assistant
│   ├── Module 3/                       # Multi-User Conversational Agents
│   ├── Module 4/                       # Text-to-SQL AI Systems
│   ├── Module 5/                       # Financial Analyst ReAct Agent
│   └── Assignment/                     # Intelligent Travel Assistant
│
├── requirements.txt
├── LICENSE
└── README.md
```

---

## 📚 Concepts

### 🌟 Introduction to LLMs

Learn to work with various LLM providers in `LangChain_Fundamentals/01_Getting_Started/`:

| Provider | Integration Type | Notebook |
|----------|-----------------|----------|
| OpenAI | Native API + LangChain | `1.0-1.2, 1.7` |
| Google Gemini | LangChain | `langchain-google-genai` |
| HuggingFace | Transformers + Inference API | `1.3-1.4` |
| Groq | High-speed inference | `1.5` |
| Open Source Models | LangChain integration | `1.6` |

### 🔗 LangChain Expression Language (LCEL)

Master the modern way to compose LangChain components in `03_LCEL/`:

- **Runnables**: The building blocks of LCEL
- **Chaining**: Pipe operators for composable workflows
- **Parallel Execution**: Run multiple chains concurrently
- **Branching & Routing**: Conditional logic in chains
- **Chain Migrations**: Upgrade legacy chains to LCEL

### 💾 Memory Systems

Build stateful conversational applications in `05_Memory/`:

- **Buffer Memory**: Simple conversation history
- **Summary Memory**: Compressed conversation context
- **Entity Memory**: Track entities across conversations
- **SQL Persistence**: Multi-user conversation storage
- **LCEL Memory Integration**: Modern memory patterns

### 🔍 Retrieval-Augmented Generation (RAG)

Build production-ready RAG pipelines in `07_RAG/`:

- **Document Loading & Splitting**
- **Vector Embeddings** (OpenAI, HuggingFace)
- **Vector Stores** (FAISS, ChromaDB, PgVector)
- **Hybrid Search** (Semantic + Keyword)
- **Indexing API** for efficient updates

### 🤖 Agents & Tool Calling

Create autonomous AI systems in `06_Tools_and_Functions/` and `10_Agents/`:

- **OpenAI Function Calling**: Structured tool invocation
- **ReAct Pattern**: Reasoning + Acting framework
- **Custom Tools**: Build domain-specific tools
- **Multi-Agent Systems**: Collaborative AI workflows

### 📊 Advanced Features

Production-ready features in `09_Advanced_Features/`:

- **Cost Monitoring**: Track API usage and costs
- **Caching**: Reduce latency and costs
- **Streaming**: Real-time response generation
- **Callbacks**: Custom handlers and logging
- **LangSmith**: Tracing, debugging, and evaluation

---

## 🛠️ Real-World Projects

| # | Project | Description |
|---|---------|-------------|
| 1 | **Review Analyst** | Analyze and summarize customer reviews |
| 2 | **Research Paper Analyst** | Extract insights from academic papers |
| 3 | **Social Media Marketing Analyst** | Generate marketing content and insights |
| 4 | **IT Support Analyst** | Automated technical support assistant |
| 5 | **Customer Support Workflow** | End-to-end support automation |
| 6 | **Report Generator** | Automated report creation system |
| 7 | **Customer Review Analyst** | Deep analysis of customer feedback |
| 8 | **Product Recommendation Agent** | Multi-user conversational recommender |
| 9 | **Quiz Question Generator** | Study assistant for education |
| 10 | **Chat Stream** | Real-time streaming chat application |
| 11 | **Custom ChatGPT** | Build your own ChatGPT from scratch |

---

## 🤖 Building AI Agents

A complete course on building production-ready AI agents:

### Module 1: Agent Tools & Tool Calling
- Understanding LangChain tools
- Creating custom tools
- LLM tool calling mechanisms

### Module 2: Research Assistant Agent
- Web search integration
- Information extraction
- Multi-step reasoning

### Module 3: Multi-User Conversational Agents
- User session management
- Persistent conversations
- Context handling across users

### Module 4: Text-to-SQL AI Systems
- Natural language to SQL conversion
- Database interaction agents
- ReAct pattern for data queries

### Module 5: Financial Analyst Agent
- Complex reasoning chains
- Real-time data integration
- Multi-tool orchestration

### 🎓 Assignment: Intelligent Travel Assistant
Build a complete travel assistant that:
- Searches for local attractions
- Retrieves weather information
- Uses ReAct reasoning for intelligent responses

---

## 🏗️ Microservice Architecture

Deploy LLM applications at scale with the Restaurant Chatbot example:

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│   Frontend  │────▶│  Service 2  │────▶│  Service 3  │
│   (React)   │     │  (FastAPI)  │     │  (LangChain)│
└─────────────┘     └──────┬──────┘     └──────┬──────┘
                           │                    │
                    ┌──────▼──────┐      ┌──────▼──────┐
                    │    Redis    │      │  PostgreSQL │
                    │   (State)   │      │  (Vectors)  │
                    └─────────────┘      └─────────────┘
```

**Features:**
- Kubernetes deployment manifests
- Docker containerization
- Ingress configuration
- Secret management
- Scalable architecture

---

## 🛠️ Tech Stack

<div align="center">

| Core | Databases | Cloud & APIs | Frontend |
|------|-----------|--------------|----------|
| ![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white) | ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=flat&logo=postgresql&logoColor=white) | ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | ![React](https://img.shields.io/badge/React-61DAFB?style=flat&logo=react&logoColor=black) |
| ![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat&logoColor=white) | ![ChromaDB](https://img.shields.io/badge/ChromaDB-FF6B6B?style=flat&logoColor=white) | ![Google](https://img.shields.io/badge/Gemini-4285F4?style=flat&logo=google&logoColor=white) | ![Streamlit](https://img.shields.io/badge/Streamlit-FF4B4B?style=flat&logo=streamlit&logoColor=white) |
| ![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat&logo=fastapi&logoColor=white) | ![FAISS](https://img.shields.io/badge/FAISS-00ADD8?style=flat&logoColor=white) | ![HuggingFace](https://img.shields.io/badge/HuggingFace-FFD21E?style=flat&logo=huggingface&logoColor=black) | ![TailwindCSS](https://img.shields.io/badge/Tailwind-38B2AC?style=flat&logo=tailwind-css&logoColor=white) |
| ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=flat&logo=jupyter&logoColor=white) | ![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat&logo=redis&logoColor=white) | ![Groq](https://img.shields.io/badge/Groq-00D4AA?style=flat&logoColor=white) | |

</div>

---

## 📋 Key Dependencies

```
langchain>=0.3.21
langchain-openai>=0.3.10
langchain-google-genai>=2.0.6
langchain-community>=0.3.20
langchain-chroma>=0.2.2
langchain-postgres>=0.0.13
langchain-huggingface>=0.1.0
langchain-groq>=0.2.0
openai>=1.68.2
chromadb>=0.6.3
faiss-cpu>=1.10.0
streamlit>=1.43.2
fastapi>=0.115.12
transformers>=4.47.0
tiktoken>=0.9.0
```

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

1. **Fork** the repository
2. **Create** a feature branch (`git checkout -b feature/amazing-feature`)
3. **Commit** your changes (`git commit -m 'Add amazing feature'`)
4. **Push** to the branch (`git push origin feature/amazing-feature`)
5. **Open** a Pull Request

### Guidelines

- Follow existing code style and notebook formatting
- Add clear comments and documentation
- Test your notebooks before submitting
- Update the README if adding new content

---

## 📝 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

```
MIT License

Copyright (c) 2025 Sourav Banerjee

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 🙏 Acknowledgments

- [LangChain](https://langchain.com) - The framework powering this repository
- [OpenAI](https://openai.com) - For GPT models and APIs
- [Coding Crashkurse](https://github.com/Coding-Crashkurse/LangChain-Udemy-Course) - Course inspiration
- [Analytics Vidhya](https://courses.analyticsvidhya.com/courses/take/building-ai-agents-with-langchain/) - AI Agents course

---

## 📬 Contact

**Sourav Banerjee**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=flat&logo=github&logoColor=white)](https://github.com/yourusername)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=flat&logo=linkedin&logoColor=white)](https://linkedin.com/in/yourprofile)

---

<div align="center">

### ⭐ Star this repository if you find it helpful!

*Built with ❤️ for the AI Engineering community*

</div>
