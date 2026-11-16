# Knowledge e RAG

Retrieval-Augmented Generation, vector databases, embeddings, knowledge graphs e estrategias de chunking.

## RAG (Retrieval-Augmented Generation)

### O que e
- Combina retrieval com generation
- Context augmentation
- Reduz hallucinations
- Permite knowledge updates sem retraining

### Pipeline
1. **Indexing:** chunk documents, embed, store in vector DB
2. **Retrieval:** embed query, search vector DB, get top-k
3. **Augmentation:** add retrieved context to prompt
4. **Generation:** LLM generates response with context

### Frameworks
- **LangChain:** langchain.com
- **LlamaIndex:** llamaindex.ai
- **Haystack:** haystack.deepset.ai
- **Semantic Kernel:** github.com/microsoft/semantic-kernel

## Vector Databases

### Pinecone
- **Site:** pinecone.io
- Fully managed
- Serverless
- Metadata filtering

### Weaviate
- **Site:** weaviate.io
- Open-source
- Hybrid search (vector + keyword)
- GraphQL API

### Milvus
- **Site:** milvus.io
- Open-source
- Scalable
- Multiple index types

### Chroma
- **Site:** trychroma.com
- Open-source, embedded
- Easy to use
- Good for prototyping

### Qdrant
- **Site:** qdrant.tech
- Open-source
- High performance
- Rust-based

### pgvector
- **Repo:** github.com/pgvector/pgvector
- PostgreSQL extension
- Use existing Postgres
- Good for small-medium scale

## Embeddings

### OpenAI
- **text-embedding-3-small:** 1536 dims, $0.02/1M tokens
- **text-embedding-3-large:** 3072 dims, $0.13/1M tokens
- **text-embedding-ada-002:** 1536 dims (legacy)

### Open-Source
- **Sentence Transformers:** sentence-transformers.readthedocs.io
- **all-MiniLM-L6-v2:** small, fast
- **BGE:** github.com/FlagOpen/FlagEmbedding (BAAI)
- **E5:** github.com/microsoft/unilm/tree/master/e5

### Local Models
- **Ollama:** ollama.ai (run models locally)
- **llama.cpp:** github.com/ggerganov/llama.cpp
- **GPT4All:** gpt4all.io

## Chunking Strategies

### Fixed Size
- Split by character count
- Overlap between chunks
- Simple but naive

### Semantic
- Split by paragraphs, sections
- Respect document structure
- Better context preservation

### Recursive
- Start with large chunks
- Recursively split if too large
- LangChain: RecursiveCharacterTextSplitter

### Document-Specific
- **Code:** split by functions, classes
- **HTML:** split by headings, sections
- **PDF:** split by pages, paragraphs

### Best Practices
- Chunk size: 500-1000 tokens
- Overlap: 10-20%
- Preserve context (headers, metadata)
- Test different strategies

## Retrieval Techniques

### Dense Retrieval
- Vector similarity (cosine, dot product, L2)
- ANN (Approximate Nearest Neighbors)
- HNSW, IVF indexes

### Sparse Retrieval
- BM25 (TF-IDF based)
- Keyword matching
- Elasticsearch, Solr

### Hybrid
- Combine dense + sparse
- Reciprocal Rank Fusion (RRF)
- Better recall and precision

### Reranking
- **Cohere Rerank:** cohere.com
- **Cross-encoder:** sentence-transformers
- **ColBERT:** github.com/stanford-futuredata/ColBERT

## Advanced RAG

### Query Transformations
- **HyDE:** Hypothetical Document Embeddings
- **Multi-query:** generate multiple queries
- **Step-back prompting:** broader context

### Context Compression
- **LLMChainExtractor:** extract relevant parts
- **EmbeddingsRedundantFilter:** remove duplicates

### Parent Document Retriever
- Store parent-child relationships
- Retrieve full parent for context

### Ensemble Retrieval
- Multiple retrievers
- EnsembleRetriever (LangChain)

## Knowledge Graphs

### Neo4j
- **Site:** neo4j.com
- Property graph model
- Cypher query language
- GraphRAG integration

### GraphRAG
- **Repo:** github.com/microsoft/graphrag
- Microsoft research
- Combines graphs with RAG
- Better for complex queries

## Evaluation

### Metrics
- **Faithfulness:** is response grounded in context?
- **Answer Relevance:** does answer address query?
- **Context Relevance:** are retrieved docs relevant?

### Frameworks
- **RAGAS:** github.com/explodinggradients/ragas
- **DeepEval:** github.com/confident-ai/deepeval
- **TruLens:** trulens.org

## Resources
- LangChain documentation
- LlamaIndex documentation
- Pinecone learning center
- RAG papers and research