# Agentic RAG - Retrieval Augmented Generation with Agents

A Jupyter Notebook implementation of **Agentic RAG** — an advanced pattern where AI agents autonomously decide when and how to retrieve information, making RAG systems more intelligent and adaptive than traditional pipelines.

## What is Agentic RAG?

Traditional RAG (Retrieval Augmented Generation) follows a fixed pipeline:
`Query → Retrieve → Generate`

**Agentic RAG** adds intelligence to this process — the agent can:
- Decide **whether** retrieval is even needed
- Choose **which** retrieval strategy to use
- **Refine** queries if initial results are insufficient
- **Iterate** retrieval multiple times to gather enough context
- **Combine** multiple sources of information

## Architecture

```
User Query
    ↓
[Agent Router] ─── Is retrieval needed? ──→ Direct LLM Answer
    ↓ Yes
[Query Analyzer] ─── Decompose complex queries
    ↓
[Vector Retriever] ─── Semantic similarity search
    ↓
[Relevance Checker] ─── Are results good enough?
    ↓ No → [Query Refiner] → retry
    ↓ Yes
[Response Generator] ─── LLM synthesis with context
    ↓
Final Answer
```

## Key Concepts

### Agent Decision Making
The agent evaluates whether retrieved documents are relevant before generating a response. If not relevant, it:
1. Reformulates the query
2. Searches different knowledge bases
3. Falls back to the base LLM if no relevant docs found

### Self-RAG Pattern
The notebook demonstrates **Self-RAG** — the model generates a retrieval token to decide:
- `[Retrieve]` — fetch external documents
- `[No Retrieve]` — answer from parametric knowledge

## Notebook Contents

```
1_agenticrag.ipynb
```

| Section | Description |
|---------|-------------|
| Setup | Install dependencies, configure API keys |
| Document Loading | Load and chunk source documents |
| Vector Store | Build FAISS index with embeddings |
| Basic RAG | Traditional retrieval pipeline baseline |
| Agentic RAG | Agent-controlled retrieval with decision logic |
| Evaluation | Compare answer quality: basic vs agentic |

## Tech Stack

| Tool | Purpose |
|------|---------|
| LangChain | Agent orchestration and RAG chains |
| FAISS | Fast vector similarity search |
| OpenAI / Gemini | LLM for reasoning and generation |
| HuggingFace | Embedding models |
| Python / Jupyter | Development environment |

## Getting Started

```bash
git clone https://github.com/sanikacentric/AgenticRAG.git
cd AgenticRAG
pip install langchain faiss-cpu openai jupyter
jupyter notebook
```

Set your API keys:
```bash
export OPENAI_API_KEY="your-key-here"
```

## When to Use Agentic RAG

- Complex, multi-hop questions requiring multiple retrievals
- Ambiguous queries that benefit from query decomposition
- Systems where retrieval quality directly impacts answer accuracy
- Production RAG systems that need graceful handling of missing context

## License

Open source — for educational and research purposes.
