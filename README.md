# FinOps Copilot

An AI-powered FinOps assistant that uses Retrieval-Augmented Generation (RAG) to help teams understand, optimize, and control their cloud spending.

## Overview

FinOps Copilot ingests your cloud cost data, billing reports, and infrastructure documentation, and exposes them through a conversational interface. Instead of digging through dashboards and CSVs, you can ask questions like:

- *"Which services drove the largest cost increase last month?"*
- *"Summarize the anomalies in our AWS bill for the last 7 days."*
- *"What are the top 5 recommendations to reduce our GCP spend?"*
- *"Show me the cost trend for the `prod-data` project since the last release."*

The system grounds every answer in your own data, so responses cite the source documents and stay accurate to your environment.

## Core Features

- **Conversational Q&A** — natural language interface over cloud cost and usage data.
- **RAG pipeline** — retrieval over indexed billing reports, cost explorer exports, IaC docs, and runbooks.
- **Anomaly detection** — surface unexpected spikes and deviations in cost trends.
- **Multi-cloud aware** — designed to work with AWS, Azure, and GCP data sources.
- **Source citations** — every answer links back to the underlying document or report.
- **Extensible connectors** — pluggable loaders for new data sources.

## Architecture

```
          ┌────────────────┐
          │   User Query   │
          └──────┬─────────┘
                 ▼
        ┌────────────────┐
        │  LLM (answer)  │ ◄── prompt + retrieved context
        └──────┬─────────┘
               ▲
        ┌──────┴─────────┐
        │ Retriever (RAG)│
        └──────┬─────────┘
               ▲
        ┌──────┴─────────┐
        │  Vector Store  │
        └──────┬─────────┘
               ▲
   ┌───────────┴────────────┐
   │ Cloud cost + FinOps    │
   │ docs, reports, runbooks │
   └────────────────────────┘
```

Typical components:

1. **Ingestion** — load billing exports, CSVs, PDFs, and docs.
2. **Chunking & Embedding** — split documents and embed them into a vector store.
3. **Retrieval** — fetch the most relevant chunks for a query.
4. **Generation** — combine the retrieved context with a prompt to an LLM.
5. **UI / API** — chat interface and programmatic access.

## Getting Started

### Prerequisites

- Python 3.10+
- An LLM provider API key (e.g., OpenAI, Anthropic, or a local model)
- Cloud billing data exported as CSV/JSON, or read access to a cost API

### Installation

```bash
git clone https://github.com/Source-C0de/FinOps-Copilot.git
cd FinOps-Copilot
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
```

### Configuration

Copy the example environment file and add your keys:

```bash
cp .env.example .env
```

Then set:

```env
LLM_API_KEY=your-key-here
VECTOR_STORE=faiss   # or chroma, qdrant, pinecone
EMBEDDING_MODEL=text-embedding-3-small
```

### Run

```bash
python -m finops_copilot
```

## Project Structure

```
FinOps-Copilot/
├── src/                  # application source code
├── data/                 # sample billing data and docs
├── notebooks/            # exploration and evaluation
├── tests/                # unit and integration tests
├── requirements.txt
├── .env.example
└── README.md
```

## Roadmap

- [ ] Initial ingestion pipeline for AWS Cost & Usage Reports
- [ ] Support for Azure and GCP billing exports
- [ ] Anomaly detection module
- [ ] Cost recommendation engine
- [ ] Web UI for chat-based interaction
- [ ] Evaluation harness for answer quality

## Contributing

Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License

This project is licensed under the MIT License. See the [LICENSE](./LICENSE) file for details.
