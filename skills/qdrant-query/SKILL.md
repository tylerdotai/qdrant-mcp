# Qdrant Query Skill

Query your vector knowledge base (RAG) on Titan.

## Trigger Phrases
- "search my knowledge"
- "query qdrant"
- "search rag"
- "what's in my memory"
- "search my notes"

## Usage

### Search Knowledge Base
```
search my knowledge base for [query]
```

### List Collections
```
list qdrant collections
```

### Get Collection Info
```
qdrant collection info [collection_name]
```

## Configuration

Set these environment variables:
- `QDRANT_HOST` (default: 192.168.0.247)
- `QDRANT_PORT` (default: 6333)
- `QDRANT_COLLECTION` (default: hydra-rag)

## Example Queries

- "search my knowledge base for flume project updates"
- "search rag for tyler' preferences"
- "list qdrant collections"
