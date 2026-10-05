# Faithfulness Evaluation in Agentic GraphRAG Systems via Multi-LLM Judging Frameworks

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/chandrashekh215/Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks/blob/main/Faithfulness_eval_with_LLMs.ipynb)
![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![Haystack](https://img.shields.io/badge/Framework-Haystack-00b4ab)
![Neo4j](https://img.shields.io/badge/GraphDB-Neo4j-008CC1)
![License](https://img.shields.io/badge/License-MIT-green)

A modular, multi-pipeline engineering framework for evaluating statement-level faithfulness, hallucination patterns, and output redundancy across standard RAG, GraphRAG, and multi-agent architectures.

---

## Overview

As Large Language Models (LLMs) are deployed in high-stakes enterprise applications, ensuring factual grounding and source traceability becomes critical. Traditional single-source RAG evaluation frameworks struggle to isolate where hallucinations originate when multiple retrieval tools (vector search, knowledge graphs, and live web APIs) are orchestrated together by autonomous agents.

This project provides an end-to-end evaluation and benchmarking framework built on **Haystack** and **Neo4j**. It combines symbolic graph retrieval (**GraphRAG**), semantic search (**vector embeddings**), and real-time **web retrieval** with custom statement extraction and multi-LLM judging pipelines. Supporting **GPT-4**, **Claude**, and **Gemini** as evaluators, the system audits generated responses at the atomic statement level and verifies knowledge graph triples against source context.

---

## Key Features

- **Embeddings Pipeline:** Semantic vector retrieval using Neo4j document embedding stores.
- **Neo4j GraphRAG Pipeline:** Custom `KnowledgeGraphRetriever` component that parses queries, extracts entity-relation search terms, and traverses Neo4j graph subgraphs to retrieve contextually connected knowledge triples.
- **Web Search Augmentation:** Real-time web retrieval via SerperDev API, document conversion, and neural reranking using `TransformersSimilarityRanker` (`intfloat/simlm-msmarco-reranker`).
- **Agentic Workflows:** Multi-agent reasoning leveraging tools from standard pipelines with source-aware tool attribution tracking.
- **Statement-Level Faithfulness Auditing:** `StatementsExtractor` and modular evaluation components (`CustomFaithfulnessEvaluator`, `CustomAgentFaithfulnessEvaluator`) that parse LLM answers into verifiable atomic statements and evaluate statement-level faithfulness using LLM judges (GPT, Claude, Gemini).
- **Knowledge Graph Triples Audit:** Automated extraction and verification of LLM-generated `(Subject, Predicate, Object)` triples against source documentation before indexing.

---

## Tech Stack

* **Orchestration Framework:** [Haystack](https://github.com/deepset-ai/haystack) (2.x)
* **Graph Database:** Neo4j (Cypher querying & document graph indexing)
* **Retrieval & Reranking:** OpenAI Embeddings, HuggingFace Transformers (`simlm-msmarco-reranker`), SerperDev Web Search API
* **LLM Judges & Generators:** OpenAI (GPT-4 / GPT-4.1), Anthropic (Claude), Google (Gemini)
* **Environment:** Python 3.10+, Jupyter Notebook, Google Colab

---

## Getting Started

### Running in Google Colab
Launch the evaluation pipeline directly in Google Colab without local configuration:

1. Click the **Open In Colab** badge at the top of this README (or [open directly](https://colab.research.google.com/github/chandrashekh215/Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks/blob/main/Faithfulness_eval_with_LLMs.ipynb)).
2. Set your environment variables in Colab Secrets or notebook setup cells:
   ```python
   import os
   os.environ["OPENAI_API_KEY"] = "your-openai-api-key"
   os.environ["SERPERDEV_API_KEY"] = "your-serper-api-key"
   os.environ["NEO4J_URI"] = "neo4j+s://your-instance.databases.neo4j.io"
   os.environ["NEO4J_USER"] = "neo4j"
   os.environ["NEO4J_PASS"] = "your-neo4j-password"
   ```
3. Run the notebook cells sequentially to initialize pipelines, build vector/graph indexes, and execute multi-LLM faithfulness evaluations.

### Local Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/chandrashekh215/Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks.git
   cd Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks
   ```

2. **Install dependencies:**
   ```bash
   pip install haystack-ai neo4j-haystack transformers openai tiktoken serper-dev
   ```

3. **Start Jupyter & Open Notebook:**
   ```bash
   jupyter notebook Faithfulness_eval_with_LLMs.ipynb
   ```

---

## Repository Structure

```
.
├── Faithfulness_eval_with_LLMs.ipynb   # Jupyter Notebook containing full pipeline code & evaluation logic
└── README.md                            # Project documentation
```

---

## Author

**Chandra Shekhar**
- **GitHub:** [@chandrashekh215](https://github.com/chandrashekh215)
- **Repository:** [Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks](https://github.com/chandrashekh215/Faithfulness-Evaluation-in-Agentic-GraphRAG-Systems-via-Multi-LLM-Judging-Frameworks)

---

## License

This project is open-source and available under the [MIT License](LICENSE).
