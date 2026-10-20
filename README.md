# repo-docs-system

A Claude Code plugin that builds and maintains a structured **Chinese knowledge base** (`docs/` system) for any code repository.

## What it does

- Generates `AGENTS.md` — a context map for AI agents to understand your project
- Creates `ARCHITECTURE.md` — architecture overview and domain breakdown
- Scaffolds `docs/` — design docs, product specs, exec plans, quality scores
- Maintains and updates existing docs without deleting existing content
- Scores documentation coverage with `docs/QUALITY_SCORE.md`

## Installation

```bash
/plugin install repo-docs-system@github:baiyue11111/repo-docs-system
```

## Usage

Trigger the skill by asking Claude to:

- "帮我初始化这个项目的 docs"
- "生成 AGENTS.md"
- "创建 ARCHITECTURE.md"
- "build a docs system for this repo"
- "generate a knowledge base"

## Output structure

```
project/
├── AGENTS.md                          # Agent context map (most important)
├── ARCHITECTURE.md                    # Architecture overview
└── docs/
    ├── QUALITY_SCORE.md               # Coverage score with history
    ├── design-docs/
    │   ├── index.md
    │   └── core-beliefs.md
    ├── product-specs/
    │   └── index.md
    └── exec-plans/
        └── tech-debt-tracker.md
```

## License

MIT
