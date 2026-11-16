# Vector Databases & RAG

## Vector DBs
- Pinecone, Weaviate, Qdrant, Chroma, pgvector
- Armazenamento de embeddings de documentos e mensagens

## Embedding Models
- OpenAI text-embedding-3-small/large
- Sentence Transformers (local): all-MiniLM-L6-v2, BGE

## RAG Pipeline
1. Chunking: Dividir documento em partes de 500-1000 tokens com overlap
2. Embedding: Gerar vetores para cada chunk
3. Storage: Salvar no Vector DB com metadados
4. Retrieval: Busca por similaridade (cosine similarity) + re-ranking
5. Augmentation: Inserir chunks no prompt do LLM

## Otimizacoes
- Hybrid search (vector + keyword BM25)
- Metadata filtering para reduzir escopo de busca