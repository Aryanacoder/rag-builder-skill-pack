---
name: build-rag-application
description: Design, build, or improve retrieval-augmented generation applications with source-grounded answers, document ingestion, chunking, embeddings, vector search, reranking, citations, evaluation, guardrails, multilingual support, OCR, or offline deployment. Use when the user asks to build a RAG app, knowledge assistant, document copilot, vector-search chatbot, local/offline assistant, or wants a structured interview that turns rough data and goals into a complete RAG implementation plan.
---

# Build RAG Application

## Core Rule

Do not start coding the RAG application until you have converted the user's situation into a clear RAG design. If the user asks for immediate implementation, ask only the missing high-risk questions, make explicit assumptions for the rest, then implement a narrow first slice.

This skill is an interview-driven RAG architect. It should make the user feel guided from fuzzy idea to buildable system.

## First Response

Start with a short framing sentence, then ask questions in batches. Do not ask the full questionnaire at once. Ask 5-8 questions per batch unless the user explicitly wants a long form.

Batch 1 must cover:

1. Goal: what should the RAG app help users decide, do, or understand?
2. Users: who will use it, and what mistakes would be costly?
3. Data: what file types, languages, volume, update frequency, and current storage?
4. Evidence: does every answer need citations, page previews, quotes, tables, images, or source downloads?
5. Runtime constraints: local/offline, cloud, privacy, latency, budget, hardware, model/API preferences?
6. Initial idea: what stack or workflow does the user already imagine?
7. Success: what would make the first demo obviously useful?

After each answer batch, summarize what you learned and ask the next most important batch. Stop questioning when the design risks are known enough to choose architecture.

## Interview Map

Use the full questionnaire in [references/question-bank.md](references/question-bank.md) when the request is broad, safety-sensitive, expensive, multilingual, multimodal, or unclear.

Keep the interview granular across these layers:

1. Product scope: jobs-to-be-done, users, answer types, refusal behavior.
2. Corpus: source systems, file types, languages, scans, tables, diagrams, images, permissions.
3. Ingestion: parsing, OCR, normalization, dedupe, metadata, manifests, incremental updates.
4. Indexing: chunking, embeddings, vector store, keyword/hybrid retrieval, asset storage.
5. Retrieval: query rewriting, filters, top-k, reranking, context assembly, citation mapping.
6. Generation: prompt policy, answer format, uncertainty, multilingual answer strategy.
7. UI/API: chat, source viewer, feedback, admin tools, batch jobs, observability.
8. Evaluation: golden questions, retrieval tests, answer faithfulness, latency, failure review.
9. Deployment: local/cloud/offline, packaging, model distribution, backups, migrations.
10. Operations: update cadence, human review, audit logs, privacy, incident response.

## Decision Flow

Use [references/architecture-playbook.md](references/architecture-playbook.md) after the initial interview.

Choose the simplest architecture that satisfies the user's constraints:

- Use a local FAISS/SQLite-style prototype when data is small, updates are manual, and speed matters.
- Use Qdrant, Weaviate, Milvus, OpenSearch, Postgres pgvector, or a managed vector database when metadata filtering, hybrid search, multi-user scale, operations, or updates matter.
- Use hybrid retrieval plus reranking when exact terms, part numbers, legal clauses, symptoms, or technical procedures matter.
- Use structured extraction and metadata when the app must cite pages, tables, diagrams, procedures, equipment, dates, customers, or permissions.
- Use OCR and visual extraction when PDFs are scanned or answers depend on diagrams, flowcharts, screenshots, handwriting, or page images.
- Use offline knowledge packs when indexing is heavy but runtime machines must be stable, private, or disconnected.

## Deliverables

When the design is ready, produce these artifacts before coding:

1. RAG brief: one-page goal, users, data, constraints, non-goals.
2. Architecture: ingestion, storage, retrieval, generation, UI/API, deployment.
3. Data contract: document metadata fields, chunk schema, citation schema, asset paths.
4. Pipeline plan: parse, clean, chunk, embed, index, package, verify.
5. Retrieval plan: query normalization, filters, hybrid search, reranking, context budget.
6. Prompt and answer policy: when to answer, cite, ask follow-up, or refuse.
7. Evaluation plan: golden set, retrieval metrics, faithfulness checks, latency targets.
8. Implementation backlog: small tasks with file paths, tests, and validation commands.

Use [references/output-templates.md](references/output-templates.md) for concise formats.

## Build Pattern

When implementing, work in vertical slices:

1. Ingest 3-10 representative documents.
2. Preserve metadata and source locations before optimizing embeddings.
3. Build retrieval with visible debug output.
4. Add citations and source previews before polishing generation.
5. Add reranking and query rewriting only after baseline retrieval is measured.
6. Add feedback and evaluation review loops before scaling the corpus.
7. Add incremental updates, permissions, and deployment packaging last unless they are core requirements.

For existing codebases, inspect current ingestion, index, retrieval, prompt, UI, and tests first. Preserve local patterns unless they block correctness.

## Guardrails

For high-stakes domains, make unsupported answers boring and explicit:

- Answer only from retrieved evidence.
- Cite every operational, legal, financial, medical, safety, or technical claim.
- Say what evidence is missing.
- Prefer asking a follow-up over inventing missing procedure steps, numeric values, or policy exceptions.
- Keep agentic background workflows supervised. They may analyze logs or draft improvements, but they must not silently alter live retrieval, prompts, indexes, or answer policy.

## Repo Lessons To Reuse

This skill was shaped by a local technical RAG app with these proven patterns:

- Heavy document processing on a developer machine; lightweight runtime on target machines.
- Full replacement knowledge packs with manifests and checksums for offline deployment.
- Docling/PyMuPDF/OCR fallback extraction so scanned and native PDFs both survive.
- Step-aware chunking, content-type metadata, page numbers, image assets, and procedure tags.
- FAISS as a simple local primary index; optional Qdrant for future hybrid/filtering paths.
- Multilingual query handling through language detection, cached translation, and source-grounded answers.
- Local reranking to improve precision after broad initial retrieval.
- Source preview and PDF download for verification before users act.
- Feedback logs and debug retrieval traces for improvement without mutating live answers.

## Quality Bar

Before declaring the RAG design or implementation done, verify:

- A representative question retrieves the expected source before generation.
- Each final answer can be traced to chunk metadata and source document location.
- Bad or out-of-corpus questions produce a safe refusal or clarification.
- The update path is defined: rebuild, incremental sync, or full replacement.
- The evaluation set includes easy, hard, ambiguous, multilingual, and no-answer questions.
- The user can inspect why a retrieved source was chosen.
