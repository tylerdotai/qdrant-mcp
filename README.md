# Qdrant MCP Server

An MCP (Model Context Protocol) server for Qdrant vector database. Enables AI agents to perform semantic search against your private knowledge base.

## Features

- Query Qdrant collections via natural language
- List available collections
- Get collection info
- Semantic similarity search using Ollama embeddings (CPU mode)

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

## Titan Setup

### llama-server (GPU) - Running on ports 8402/8403

The Strix Halo runs llama-server in a Docker container:

```bash
# In llama-box container:
llama-server -m /models/Qwen3.5-35B-A3B-Q4_K_M.gguf -c 8192 -ngl 999 -fa 1 --no-mmap --host 0.0.0.0 --port 8402
llama-server -m /models/Qwen3-14B-Q4_K_M.gguf -c 8192 -ngl 999 -fa 1 --no-mmap --host 0.0.0.0 --port 8403
```

**Important flags for Strix Halo:**
- `-fa 1` - Flash attention (required)
- `--no-mmap` - Avoids crashes/slowdowns
- `-ngl 999` - All layers on GPU

### Ollama (CPU) - For Embeddings

Ollama runs on the host (not in container) in CPU mode due to ROCm issues:

```bash
# On Titan (192.168.0.247):
# Edit /etc/systemd/system/ollama.service.d/override.conf:
[Service]
Environment=OLLAMA_MODELS=/mnt/filestore/ollama_models
Environment=OLLAMA_HOST=0.0.0.0:11434
Environment=CUDA_VISIBLE_DEVICES=-1  # CPU mode - ROCm has issues with embeddings

systemctl daemon-reload && systemctl restart ollama
```

**Note:** GPU mode crashes on ROCm due to a known llama.cpp bug with embedding models. CPU mode works but is slower. This is a llama.cpp/ROCm issue, not a setup issue.

### Qdrant

Qdrant runs on the host:

```bash
# On Titan:
qdrant --config-path /home/anon/qdrant/config/config.yaml
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

## Known Issues

- **Ollama embeddings on GPU**: llama.cpp embedding binary crashes on ROCm 7.x due to a compiler regression. Running in CPU mode (`CUDA_VISIBLE_DEVICES=-1`) works around this. See: https://github.com/kyuz0/amd-strix-halo-toolboxes/issues/45
