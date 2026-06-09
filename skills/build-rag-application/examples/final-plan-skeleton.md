# Example: Final Plan Skeleton

## Recommendation

Build a local-first RAG prototype with a separate ingestion pipeline and a small chat UI. Start with 10 representative documents, preserve page metadata, and evaluate retrieval before adding advanced agent workflows.

## Architecture

- Ingestion: parse PDFs with native extraction, then OCR fallback for scanned pages.
- Metadata: JSONL or SQLite records for sources, chunks, page numbers, content type, and hashes.
- Index: FAISS for first prototype; Qdrant or pgvector if filtered multi-user retrieval becomes required.
- Retrieval: top-30 dense retrieval, optional keyword boost, rerank to top-6.
- Generation: strict source-grounded prompt with citations and refusal behavior.
- UI: chat plus source list and page preview.
- Evaluation: 30 golden questions covering direct lookup, synthesis, no-answer, and multilingual paraphrases.

## Next Tasks

1. Create sample corpus folder and manifest.
2. Implement extraction smoke test.
3. Implement chunk schema and chunk writer.
4. Build baseline index.
5. Add retrieval debug command.
6. Add answer generation with citation IDs.
7. Add no-answer guardrail test.
