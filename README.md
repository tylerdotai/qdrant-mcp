# Qdrant MCP Server

An MCP (Model Context Protocol) server for Qdrant vector database. Enables AI agents to perform semantic search against your private knowledge base.

## Features

- Query Qdrant collections via natural language
- List available collections
- Get collection info
- Semantic similarity search

## Installation

```bash
git clone https://codeberg.org/tylerdotai/qdrant-mcp.git
cd qdrant-mcp
pip install -r requirements.txt
```

## Configuration

Set environment variables:

```bash
export QDRANT_HOST="192.168.0.247"
export QDRANT_PORT="6333"
export QDRANT_API_KEY=""  # Optional
export QDRANT_COLLECTION="hydra-rag"
```

## Running

```bash
python server.py
```

## MCP Tools

| Tool | Description |
|------|-------------|
| `search` | Semantic search query |
| `list_collections` | List all collections |
| `collection_info` | Get collection details |

## Usage with Claude/OpenClaw

Add to your mcporter config or use directly via the server.
