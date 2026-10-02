# AI Ready Design System

**AI Readiness Check for Figma Design Systems**

A Claude plugin that audits your Figma design system for AI-powered code generation readiness. Get a scored report with specific, actionable recommendations — then re-run after changes to track improvement.

All 28 checks are deterministic and rule-based.

## What it checks

| Category | Weight | Checks |
|----------|--------|--------|
| **Token Architecture** | 25% | Variable collections, semantic naming, hierarchy depth, descriptions, type diversity, modes, aliasing |
| **Component Contracts** | 25% | Component count, descriptions, variant coverage, property definitions, naming consistency, state completeness |
| **Design-Code Parity** | 15% | Code Connect existence, mapping coverage, naming alignment |
| **Accessibility** | 15% | Semantic color tokens, state indicators beyond color, contrast token pairs, focus state tokens |
| **Documentation Quality** | 10% | File organization, component descriptions, variable descriptions, usage guidelines |
| **Governance** | 10% | Deprecation signals, naming taxonomy, component organization, system completeness |

## How it works

The plugin reads structured data from your Figma file using Figma MCP tools (`get_metadata`, `get_variable_defs`, `get_design_context`, `get_code_connect_map`) and runs pattern matching, counting, and structural analysis. Every check is rule-based — results are reproducible and deterministic.

## Install

### From the Claude Plugin Directory

Search for **AI Ready Design System** in the Discover tab under Customize > Plugins.

### Manual install

Download the `.plugin` file from [Releases](../../releases) and drop it into a Claude chat, or:

```
claude plugin install ds-ai-check.plugin
```

## Usage

```
/ds-ai-check
```

Provide your Figma file URL when prompted. You'll get:

- An **overall AI Readiness Score** (0–100) with a letter grade (A through F)
- **Per-category scores** with pass/partial/fail on each of the 28 checks
- **Exact counts** — "14 of 23 components have descriptions (61%)"
- **Top 5 priority actions** ranked by score improvement potential
- **Specific Figma-level recommendations** for every failing check

## Scoring

| Grade | Score | Label | Meaning |
|-------|-------|-------|---------|
| A | 90–100 | AI-Ready | DS can be confidently used by AI agents for code generation |
| B | 75–89 | Mostly Ready | Strong foundation with some gaps to close |
| C | 55–74 | Partially Ready | Key areas need work before AI can reliably consume the DS |
| D | 35–54 | Early Stage | Significant structural improvements needed |
| F | 0–34 | Not AI-Ready | Fundamental DS structure missing for AI consumption |

## Requirements

- **Figma MCP** must be connected in your Claude setup
- A Figma file URL for the design system you want to audit

## Re-running

Run `/ds-ai-check` again after making improvements. The deterministic scoring means your progress is measurable and comparable across runs — diff your reports to see exactly what improved.

## Example output

Tested against the [shadcn/ui community design system](https://www.figma.com/community/file/1203061493325953101):

- **Overall:** 38/100 — Grade D (Early Stage)
- **Strongest:** Component Contracts (62/100) — excellent variant coverage and typed properties
- **Weakest:** Design-Code Parity (0/100) — no Code Connect mappings
- **Key finding:** Token layer is all raw primitives (`slate/900`) with no semantic abstraction, no descriptions, no light/dark modes

## Author

**Yeshika Senadeera** — [yeshikasenadeera@gmail.com](mailto:yeshikasenadeera@gmail.com)

## License

MIT
