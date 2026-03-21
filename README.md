# Qdrant MCP

MCP server for querying Qdrant vector databases from AI agents through semantic search and collection inspection tools.

[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat-square&logo=python)](#)
[![Qdrant](https://img.shields.io/badge/Qdrant-vector%20db-red?style=flat-square)](#)

## Live Demo

- Repository: `https://github.com/tylerdotai/qdrant-mcp`
- Main server entrypoint: `server.py`

## About

Qdrant MCP exposes a small set of Model Context Protocol tools for semantic retrieval against a Qdrant instance. It is designed for local or self-hosted agent setups that need collection introspection and text-based search over a private vector knowledge base.

## Tech Stack

| Layer | Technology |
|-------|------------|
| Runtime | Python |
| Protocol | MCP |
| Vector Store | Qdrant |
| Transport | stdio MCP server |

## Features

### MCP Tools
- Semantic search against a configured Qdrant collection
- List available collections
- Inspect collection metadata and counts

### Repo Surface
- MCP server implementation in `server.py`
- Example skill under `skills/qdrant-query/`
- Environment-based Qdrant configuration

## Project Structure

```text
server.py                    MCP server for Qdrant access
requirements.txt             Python dependencies
skills/qdrant-query/         Example related skill assets
README.md                    Repository overview
```

## Getting Started

### Prerequisites

- Python 3.10+
- A running Qdrant instance
- `pip`

### Installation

```bash
git clone https://github.com/tylerdotai/qdrant-mcp.git
cd qdrant-mcp
pip install -r requirements.txt
```

## Deployment

Qdrant MCP is designed for local or self-hosted agent environments.

- Repository: `https://github.com/tylerdotai/qdrant-mcp`

## Usage

```bash
python server.py
```

Configure with environment variables such as `QDRANT_HOST`, `QDRANT_PORT`, `QDRANT_API_KEY`, and `QDRANT_COLLECTION`.

## Current Limitations

- Tool surface is intentionally small today
- Query behavior assumes a Qdrant setup compatible with `query_text` search flow
- The repo is focused on MCP server logic rather than broader deployment packaging

## Roadmap

- Add more collection management and indexing tools
- Improve setup docs for common local agent environments
- Expand examples showing how agents should consume the MCP server

## License

No license has been added yet.
