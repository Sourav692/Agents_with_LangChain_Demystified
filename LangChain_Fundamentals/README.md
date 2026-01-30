# LangChain Fundamentals - Course Directory

This directory contains a comprehensive, progressively organized curriculum for learning LangChain and its applications in Generative AI.

## 📚 Learning Path

### 01. Getting Started
Introduction to LangChain with commercial and open-source LLMs.
- Using Commercial LLMs (OpenAI, etc.) natively and with LangChain
- Working with Open Source LLMs (HuggingFace, Groq Cloud)
- OpenAI API basics

### 02. Inputs, Outputs & Prompts
Understanding input/output mechanisms and prompt engineering.
- LangChain inputs and outputs
- Prompt templates and best practices
- LLM vs ChatModel comparison
- Output parsers

### 03. LangChain Expression Language (LCEL)
Mastering LCEL and the Runnable interface.
- LCEL fundamentals and deep dive
- Runnables and composition
- Chain migrations to LCEL

### 04. Chains
Building and managing chains in LangChain.
- Chain basics and output parsers
- Advanced chain patterns
- Branching, routing, and merging chains

### 05. Memory
Implementing memory in conversational AI.
- Chat message memory types
- Conversation chains with LCEL
- Multi-user conversations (in-memory and SQL persistent)
- ConversationQA patterns

### 06. Tools and Functions
Working with tools and function calling.
- Tool basics and function calling
- LangChain tool calling patterns
- Building tool-calling agents
- OpenAI function integration

### 07. RAG (Retrieval Augmented Generation)
Deep dive into RAG implementations.
- RAG fundamentals and patterns
- Hybrid search strategies
- Indexing API usage

### 08. Text Summarization
Summarization techniques with LangChain.
- Summarization strategies and patterns

### 09. Advanced Features
Production-ready LangChain features.
- LLM cost monitoring
- Caching strategies
- Streaming responses
- Chain moderation
- Callbacks and hooks

### 10. Agents
Building autonomous agents.
- Agent fundamentals and patterns

### 11. LangSmith
Observability and evaluation tools.
- Tracing, datasets, and evaluation

### 12. MicroServices
Production deployment patterns.
- Microservice architecture for LLM applications

---

## 📁 Folder Structure

```
LangChain_Fundamentals/
├── 01_Getting_Started/       # 8 notebooks
├── 02_Inputs_Outputs_Prompts/# 6 notebooks
├── 03_LCEL/                  # 7 notebooks
├── 04_Chains/                # 4 notebooks
├── 05_Memory/                # 9 notebooks
├── 06_Tools_and_Functions/   # 4 notebooks
├── 07_RAG/                   # 4 notebooks + resources
├── 08_Summarization/         # 2 notebooks + resources
├── 09_Advanced_Features/     # 6 notebooks
├── 10_Agents/                # 1 notebook + resources
├── 11_LangSmith/             # 1 notebook + resources
├── 12_MicroServices/         # Production templates
├── _Archive/                 # Deprecated & duplicate files
└── images/                   # Documentation images
```

---

## 🚀 Getting Started

1. Clone the repository
2. Rename `.env.example` to `.env` and add your API keys
3. Start with `01_Getting_Started` and progress through the numbered folders
4. Each folder contains notebooks numbered in recommended learning order

### Cleanup Notebook Output

**Linux:**
```bash
find . -name "*.ipynb" -exec jupyter nbconvert --ClearOutputPreprocessor.enabled=True --inplace {} \;
```

**Windows:**
```powershell
for /r %i in (*.ipynb) do jupyter nbconvert --to notebook --ClearOutputPreprocessor.enabled=True --inplace "%i"
```
