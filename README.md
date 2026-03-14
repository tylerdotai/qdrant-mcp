# Qdrant MCP Server

An MCP (Model Context Protocol) server for Qdrant vector database. Enables AI agents to perform semantic search against your private knowledge base.

## Features

- Query Qdrant collections via natural language
- List available collections
- Get collection info
- Semantic similarity search using Ollama embeddings

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
export OLLAMA_HOST="192.168.0.247"
export OLLAMA_PORT="11434"
```

## Prerequisites

### Start Ollama on Titan (for embeddings)

```bash
ssh root@192.168.0.247
systemctl start ollama
```

Make sure Ollama is listening on all interfaces (edit `/etc/systemd/system/ollama.service.d/override.conf`):

```ini
[Service]
Environment=OLLAMA_HOST=0.0.0.0:11434
Environment=OLLAMA_MODELS=/mnt/filestore/ollama_models
```

## Running the MCP Server

```bash
python server.py
```

## Using the Skill

The skill is in `skills/qdrant-query/`:

```bash
# Search the knowledge base
python skills/qdrant-query/query.py search "your query here"

# List collections
python skills/qdrant-query/query.py list

# Get collection info
python skills/qdrant-query/query.py info hydra-rag
```

## MCP Tools

| Tool | Description |
|------|-------------|
| `search` | Semantic search query |
| `list_collections` | List all collections |
| `collection_info` | Get collection details |

## Available Collections

- `strixhalo-wiki` - Strix Halo documentation
- `hydra-rag` - General RAG/knowledge base
- `ai-news` - AI news articles
- `mesh-docs` - Mesh network docs
- `agent-handoffs` - Agent handoff records
- `conversations` - Conversation history
- `system_states` - System state snapshots
- `screenshots` - Screenshot metadata
- `openclaw-config` - OpenClaw configuration
- `workspace-memory` - Workspace memory
- `documentation` - General docs
- `personal` - Personal notes
- `web-intel` - Web intelligence

## Usage with Claude/OpenClaw

Add to your mcporter config or use directly via the server.
