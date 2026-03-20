---
description: Review a RAG pipeline for chunking quality, retrieval accuracy, re-ranking, and prompt design
---

Review the RAG pipeline in $ARGUMENTS (code, config, or description).

**Step 1** — Read the pipeline code/config and trace the flow from document ingestion to LLM response.

**Document Processing & Chunking**
- Chunk size appropriate for the embedding model context window
- Chunk overlap configured to preserve context across boundaries
- Chunking strategy matches content type (paragraph for prose, section for docs, row for tables)
- Metadata attached to chunks (source, page, section, date) for filtering and citation
- Preprocessing removes noise (headers/footers, boilerplate, encoding artifacts)

**Embedding**
- Embedding model matches retrieval use case (asymmetric for Q&A, symmetric for similarity)
- Embeddings re-generated when source documents change
- Embedding dimensions and model version consistent between indexing and query time
- Batch embedding used for efficiency, not one-by-one API calls

**Vector Store & Retrieval**
- Index type appropriate for dataset size (HNSW for large, flat for small)
- Top-K value calibrated (too low misses relevant chunks, too high adds noise)
- Hybrid search (vector + keyword/BM25) considered for factual queries
- Metadata filters applied before vector search to reduce search space
- Retrieved chunks re-ranked before passing to LLM (cross-encoder or LLM reranker)

**Prompt Design**
- Retrieved context clearly delimited in the prompt
- LLM instructed to answer only from provided context
- Citation format requested so answers are traceable to source chunks
- Fallback instruction when no relevant context is found ("I don't know" not hallucination)
- Context window not exceeded — chunk count x chunk size + prompt + max_tokens < model limit

**Evaluation**
- Retrieval quality measured (recall@K, MRR)
- Answer quality measured (faithfulness, relevance, groundedness)
- Failure cases logged (no retrieval, wrong retrieval, hallucination despite context)

Output findings as a prioritized list: **Critical > Major > Minor**. Include specific recommendations.
