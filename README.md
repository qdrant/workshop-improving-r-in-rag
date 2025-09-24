# Workshop: Improving R in RAG

This workshop focuses on enhancing the **R**etrieval component in Retrieval Augmented Generation (RAG) systems using 
Qdrant vector database. Through hands-on Jupyter notebooks, you'll learn advanced techniques for vector search, multiple 
embedding models, hybrid retrieval strategies, and practical optimizations to improve RAG system performance.

## Prerequisites

- **Python 3.12 or higher**
- **[uv](https://docs.astral.sh/uv/)** - Ultra-fast Python package manager
- **[Docker](https://www.docker.com/)** (optional) - For running Qdrant locally
- **LLM API access** - Anthropic, OpenAI, or Hugging Face account

> [!TIP]
> **🎉 Free LLM Access Available!**
> HuggingFace offers a generous free tier for their Inference API with access to thousands of specialized models across multiple AI tasks. Perfect for experimenting with this workshop without upfront costs!

## Installation

### Clone the repository

```bash
git clone <repository-url>
cd workshop-improving-r-in-rag
```

### Install uv

**On macOS and Linux:**

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

**On Windows:**
```powershell
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
```

**Alternative (using pip):**

```bash
pip install uv
```

### Install dependencies

```bash
uv sync
```

## Qdrant Setup

You can use either a local Qdrant instance or Qdrant Cloud's free tier.

### Option 1: Local Docker Container

```bash
docker run -p "6333:6333" -p "6334:6334" -v "$(pwd)/qdrant_storage:/qdrant/storage:z" "qdrant/qdrant:v1.15.4"
```

### Option 2: Qdrant Cloud Free Tier

Sign up for [Qdrant Cloud](https://cloud.qdrant.io/login) and use the free 1GB cluster.

## Environment Configuration

Create a `.env` file in the `notebooks/` directory with your API credentials:

### Option 1: HuggingFace (Free Tier Recommended) 🆓

```env
# LLM provider settings
LLM_PROVIDER="huggingface"
HF_TOKEN="your-huggingface-token"

# Qdrant settings
QDRANT_URL="http://localhost:6333"
# QDRANT_API_KEY="your-cloud-api-key" # Only needed for Qdrant Cloud
```

**To get your HuggingFace token:**
1. Create a free account at [huggingface.co](https://huggingface.co)
2. Go to [Token Settings](https://huggingface.co/settings/tokens)
3. Create a new token with "Read" permissions
4. Copy the token to your `.env` file

### Option 2: Other Providers

```env
# For Anthropic
LLM_PROVIDER="anthropic"
ANTHROPIC_API_KEY="your-api-key-here"

# For OpenAI
LLM_PROVIDER="openai"
OPENAI_API_KEY="your-api-key-here"

# Qdrant settings
QDRANT_URL="http://localhost:6333"
# QDRANT_API_KEY="your-cloud-api-key" # Only needed for Qdrant Cloud
```

**All Supported LLM providers:**
- **🆓 Hugging Face** (Recommended): Generous free tier with thousands of models - Set `LLM_PROVIDER="huggingface"` and `HF_TOKEN`
- **Anthropic**: Set `LLM_PROVIDER="anthropic"` and `ANTHROPIC_API_KEY`
- **OpenAI**: Set `LLM_PROVIDER="openai"` and `OPENAI_API_KEY`

## Workshop Structure

This workshop consists of 4 progressive notebooks:

### 📓 [00-set-up-environment.ipynb](notebooks/00-set-up-environment.ipynb)
- Environment setup and dependency installation
- Qdrant connectivity testing
- Introduction to the tech stack (Qdrant, FastEmbed, any-llm-sdk)

### 📓 [01-initial-data-load.ipynb](notebooks/01-initial-data-load.ipynb)
- Loading HackerNews dataset into Qdrant
- Building a basic RAG pipeline with dense vectors
- Implementing payload-based filtering
- Testing retrieval quality and LLM integration

### 📓 [02-different-representation-models.ipynb](notebooks/02-different-representation-models.ipynb)
- Setting up multiple vector representations per document
- Implementing sparse vectors (BM25) for keyword matching
- Multi-vector embeddings with ColBERT
- Hybrid search strategies: retrieval + reranking, and fusion methods

### 📓 [03-low-hanging-fruits.ipynb](notebooks/03-low-hanging-fruits.ipynb)
- Search result diversification using Maximal Marginal Relevance
- Applying business rules and constraints
- Additional optimization techniques for production RAG systems

## Running the Workshop

Start Jupyter Lab:

```bash
uv run jupyter lab
```

Or Jupyter Notebook:

```bash
uv run jupyter notebook
```

Then navigate through the notebooks in order, starting with `00-set-up-environment.ipynb`.

## Technical Stack

- **[Qdrant](https://qdrant.tech/)** - High-performance vector database for dense, sparse, and multi-vector retrieval
- **[FastEmbed](https://github.com/qdrant/fastembed)** - Efficient text-to-vector conversion with multiple embedding models
- **[any-llm-sdk](https://mozilla-ai.github.io/any-llm/)** - Unified interface for multiple LLM providers

## Dataset

The workshop uses a curated HackerNews submissions dataset containing tech discussions, startup ideas, and programming 
topics - perfect for demonstrating various retrieval challenges and solutions.

## Learning Outcomes

By completing this workshop, you'll understand:

- How to set up and configure Qdrant for production RAG systems
- Different embedding models and when to use each approach
- Hybrid retrieval strategies combining dense and sparse vectors
- Advanced reranking and fusion techniques
- Practical optimizations for improving retrieval relevance
- How to handle real-world RAG challenges like search diversity and business constraints
