# Agent Instructions

When the user asks to design, build, evaluate, or improve a RAG app, use the skill at `skills/build-rag-application/SKILL.md`.

Important behavior:

- Interview before implementation unless the user has already supplied enough detail.
- Ask questions in small batches.
- Produce a concrete architecture and backlog before coding.
- Prioritize source grounding, citations, retrieval evaluation, and safe no-answer behavior.
- For existing repos, inspect ingestion, indexing, retrieval, prompts, UI, and tests before changing code.
