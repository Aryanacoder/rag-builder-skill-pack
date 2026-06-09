# RAG Builder Skill Pack

A GitHub-ready agent skill for designing and building source-grounded RAG applications. It is meant for Claude Code, Cursor, Codex, and other agents that understand `SKILL.md`-style skills.

## What It Does

The main skill, `build-rag-application`, guides an AI agent through a granular RAG discovery interview, then produces a buildable architecture, ingestion plan, retrieval plan, evaluation plan, and implementation backlog.

It was informed by this workspace's local technical RAG application history: Chainlit UI, FAISS/Qdrant indexing, OCR fallbacks, multilingual query handling, source previews, reranking, offline knowledge packs, feedback logs, and retrieval debugging.

## Layout

```text
rag-builder-skill-pack/
  skills/
    build-rag-application/
      SKILL.md
      agents/openai.yaml
      references/
      examples/
  .claude-plugin/
  .cursor/rules/
  AGENTS.md
  CLAUDE.md
```

## Install Manually

Claude Code:

```bash
cp -r skills/build-rag-application ~/.claude/skills/build-rag-application
```

Codex:

```bash
mkdir -p .agents/skills
cp -r skills/build-rag-application .agents/skills/build-rag-application
```

Cursor:

```bash
mkdir -p .cursor/skills
cp -r skills/build-rag-application .cursor/skills/build-rag-application
```

For Cursor rule-based fallback, keep `.cursor/rules/build-rag-application.mdc` in the repo.

## Example Prompt

```text
Use the build-rag-application skill. Interview me step by step and design the best RAG app for my data, constraints, and first demo.
```

## Notes

- The skill intentionally asks questions before coding.
- It keeps the main `SKILL.md` focused and moves detailed checklists into `references/`.
- It does not require scripts or runtime dependencies.
