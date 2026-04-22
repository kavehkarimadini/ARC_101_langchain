# ARC 101: LangChain Learning Journey

## Overview

This repository documents a comprehensive learning progression through **LangChain**, a powerful framework for building applications with Large Language Models. The journey progresses from foundational concepts through advanced agent-based systems, all implemented using **local, open-source LLMs via Ollama** (including Mistral, Gemma3, and others). The work spans theoretical understanding, practical retrieval-augmented generation (RAG) applications, and sophisticated autonomous agents.

---

## The Learning Path

### **Phase 1: Foundations & RAG Concepts** 
**File**: `ARC_101_Langchain_01.ipynb`

The journey begins with establishing core LangChain concepts. This notebook introduces:

- **Open-source LLM landscape**: A roadmap for using free alternatives like Mistral 7B, Llama 2, and Zephyr running locally via Ollama
- **RAG (Retrieval-Augmented Generation)**: Understanding how to augment LLM responses with external knowledge bases
- **Practical RAG pipeline implementation**:
  - Loading documents from the web using `WebBaseLoader`
  - Intelligently chunking text with proper overlap to preserve context
  - Creating semantic embeddings using OllamaEmbeddings
  - Building a FAISS vector store for fast similarity search
  - Testing retrieval quality and embedding effectiveness

This foundation enables all subsequent work by demonstrating how to connect local LLMs with external knowledge sources—a critical pattern for real-world applications.

---

### **Phase 2: Advanced Retrieval Techniques**
**File**: `ARC_101_Langchain_02.ipynb`

Having understood basic RAG, this notebook explores **retrieval excellence**—how to significantly improve the quality of retrieved documents:

- **Multiple retriever strategies**: Comparing similarity search, Maximum Marginal Relevance (MMR), score thresholding, and top-k retrieval
- **Query enhancement with MultiQueryRetriever**: The LLM generates 5 different phrasings of user queries and combines results—a technique that dramatically improves retrieval coverage for ambiguous questions
- **Structured outputs**: Using Pydantic models to force LLMs into validated JSON structures, ensuring reliable, parseable responses
- **Real-world demonstration**: Answering questions about the State of the Union address, showing how different retrieval strategies affect answer quality

Key insight: Simply retrieving documents isn't enough—*how* you retrieve them and *how* you structure the response determines practical success.

---

### **Phase 3: Real-World RAG Application**
**File**: `RAG_LangChain.ipynb`

Theory meets practice with a sophisticated real-world application analyzing **Ausgrid electric vehicle survey responses**. This notebook demonstrates:

- **Complex document analysis at scale**: Processing customer survey data to extract behavioral insights
- **Multi-faceted analytical framework**: Implementing 10 different analysis prompts per survey question, including:
  - N-gram frequency analysis (unigrams, bigrams, trigrams)
  - Sentiment analysis on extracted topics
  - Identification of barriers and opportunities
  - Application of the **COM-B Behavioral Change Model** to understand psychological, physical, social, and motivational factors
- **RAG chains with source attribution**: `RetrievalQAWithSourcesChain` traces which original data passages support each analytical insight
- **Domain-specific application**: Deriving actionable recommendations for EV fleet adoption policy

This demonstrates that RAG systems can solve real business problems—in this case, understanding customer perspectives on electric vehicle transitions.

---

### **Phase 4: Simple Conversational Agents**
**File**: `Agent_01/Agent_Bot.py`

The work transitions from passive retrieval to **autonomous interaction** with the first agent implementation:

- **Stateful conversation**: The agent maintains message history across interactions
- **LangGraph framework**: Using state graphs to define agent behavior and message flow
- **Interactive loop**: A chatbot that responds to user input until they exit
- **Local LLM integration**: Running on Mistral via Ollama without external API calls

This simple agent is the foundation for understanding agent architecture—a stepping stone to more complex reasoning systems.

---

### **Phase 5: Advanced Agents with Reasoning & Tools**
**File**: `Agent_01/ReAct.py`

The final phase implements the **ReAct (Reasoning + Action) pattern**, creating agents that can reason about problems and decide when to use tools:

- **Tool integration**: Custom mathematical tools (add, subtract, multiply) with formal definitions and docstrings
- **Conditional branching**: The agent decides whether to call tools, execute them, or provide a direct answer
- **Complex planning**: Handles multi-step reasoning (e.g., "Add 40 + 12, then multiply by 6, then tell a joke")
- **Tool execution node**: Automatically routes selected tools and processes their results
- **Streaming output**: Real-time result display for interactive experiences

This represents the frontier of the learning journey—agents that can think through problems, decompose them into steps, and autonomously use available tools to reach conclusions.

---

## Data & Resources

### **state_of_the_union.txt**
A sample text corpus used throughout the notebooks for demonstrating document loading, retrieval testing, and Q&A capabilities. Serves as the universal test dataset for retrieval experiments.

---

## Technology Stack

The entire project leverages:

| Category | Technology |
|----------|-----------|
| **Language** | Python with Jupyter notebooks |
| **LLM Framework** | LangChain |
| **Agent Framework** | LangGraph |
| **Model Inference** | Ollama (local open-source models) |
| **Embeddings** | OllamaEmbeddings (Mistral-based) |
| **Vector Stores** | FAISS, Chroma |
| **Document Processing** | RecursiveCharacterTextSplitter, WebBaseLoader, TextLoader |
| **Output Validation** | Pydantic |
| **Tool Definition** | Python's @tool decorator |

---

## Key Concepts & Patterns

### **Retrieval-Augmented Generation (RAG)**
The core pattern underlying most notebooks: retrieve relevant documents from a knowledge base, then feed them into an LLM to generate contextual responses. This enables accurate answers without fine-tuning the model.

### **Tool Use**
Agents can be equipped with external tools (APIs, functions, databases) and autonomously decide when to use them. The ReAct agent demonstrates planning-based tool use.

### **Chain-of-Thought**
Agents and retrievers enhance reasoning by breaking problems into steps, generating intermediate reasoning, and transparently showing their work.

### **Structured Outputs**
Using Pydantic models to enforce schema on LLM outputs guarantees parseable, validated responses—critical for production systems.

---

## Progression & Interconnections

```
Foundations (Notebook 01)
    ↓
Advanced Retrieval (Notebook 02)
    ↓
Real-World RAG Application (RAG_LangChain.ipynb)

Simple Agent (Agent_Bot.py)
    ↓
Tool-Using ReAct Agent (ReAct.py)
```

Each notebook builds on skills from previous work. The RAG notebooks establish retrieval excellence used in the RAG_LangChain application. The agent files progress from simple conversation to sophisticated reasoning with tool use.

---

## Running This Work

Each Jupyter notebook can be run independently after configuring an Ollama instance with the required models (typically Mistral for LLMs and embeddings). The Python agent scripts in `Agent_01/` run directly from the terminal with any compatible OpenAI-style LLM provider.

---

## Summary

This repository represents a **complete educational journey** in modern LLM application development:
- **Understanding** foundational concepts (Notebooks 01-02)
- **Applying** RAG to real problems (RAG_LangChain.ipynb)
- **Advancing** to autonomous agent systems (Agent_01/)

All work uses **local, open-source models**, eliminating API dependencies and costs while demonstrating that sophisticated LLM applications don't require expensive commercial services. The progression demonstrates that mastering retrieval, reasoning, and tool use enables building powerful, practical AI systems.
