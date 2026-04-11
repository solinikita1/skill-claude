# CLAUDE.md

This file documents the repository structure, conventions, and development workflows for AI assistants working in this codebase.

## Repository Overview

This is a **Claude Code skill definition repository** for systemprompt.io. It contains Markdown-based skill specifications that define behaviors for Claude AI assistants — specifically how Claude should perform structured review tasks for the systemprompt brand.

**Not a traditional software project.** There is no build system, package manager, test framework, or compiled code. All artifacts are Markdown files.

## Repository Structure

```
skill-claude/
├── CLAUDE.md                        # This file
└── slill_soli_brand_review.md       # Brand review skill definition
```

> Note: `slill_soli_brand_review.md` contains a typo ("slill" instead of "skill") in the filename. This is the original uploaded filename — do not rename it without explicit instruction, as it may break external references.

## What Is a Skill File?

A skill file is a structured Markdown document that tells Claude:
- **When** to activate (trigger conditions)
- **What inputs** to expect from the user
- **How** to process those inputs (review checklists, rules, logic)
- **What output** to produce (format, sections, follow-up actions)

Skill files are loaded into Claude Code sessions and consumed as prompts/instructions. They are not executed as code.

## Current Skills

### `slill_soli_brand_review.md` — systemprompt.io Brand Review

Reviews marketing and technical content against systemprompt's brand identity and voice before publishing.

**Dependencies:** Requires the `identity` and `brand-voice` skills to be loaded first.

**Trigger:** User asks to review, check, or audit content before publishing.

**Inputs:**
- Content to review (pasted text, file, or URL)
- Channel: LinkedIn, Reddit, blog, email outreach, email nurture, documentation, or landing page
- Target audience: CTOs/enterprise, SaaS partners, or individual users

**Review categories:**
1. Identity Alignment — governance infrastructure positioning
2. Voice and Tone — four voice attributes + audience tone
3. Critical Rule Compliance — banned patterns, hashtags, em dashes, AI clichés, engagement bait
4. Messaging Hierarchy — core message reinforcement
5. Terminology — correct systemprompt and Anthropic terms
6. Channel-Specific Checks — per-channel formatting and content rules
7. AI Detection Risk — human-voice verification

**Output:** Alignment score summary, issues table (location/severity/fix), before/after revised sections, follow-up prompt.

## Skill File Conventions

When adding or editing skill files, follow these conventions:

### Structure

All skill files must include these sections in order:

```markdown
# [Skill Name]

[One-paragraph purpose description]

## Dependencies

[List prerequisite skills and what they provide]

## Trigger

[One sentence: when Claude should activate this skill]

## Inputs

- [input name] ([accepted formats or options])

## [Core Logic Section(s)]

[Checklists, rules, or processing instructions]

## Output

[Exact output format with section names, table structure, and follow-up prompt]
```

### Formatting Rules

- Use `##` for top-level sections, `###` for subsections, `####` for sub-subsections
- Use bullet lists (`-`) for checklist items and input definitions
- Use Markdown tables for structured output (issues found, comparisons)
- Use inline code (backticks) for flags, labels, or exact strings that must appear verbatim (e.g., `[UNVERIFIED]`)
- Do not use em dashes (`—`) in skill content — they violate the brand rules this repository enforces
- Do not use hashtags in skill content

### Naming

- Skill files: `skill_[scope]_[action].md` (snake_case, descriptive)
- Sections: Title case for H2/H3 headers

### Terminology to Use (per brand rules)

| Use | Avoid |
|-----|-------|
| AI governance infrastructure | persistence layer, memory tool, prompt library |
| the systemprompt platform | tool, app, marketplace |
| skill | plugin (Anthropic term distinction) |
| agent, connector, MCP server | generic "AI assistant" |
| Claude Cowork | generic product references |
| build-vs-buy | systemprompt vs. [competitor] framing |

### Banned Words/Patterns in Content

Any content reviewed or authored here must not include:
- `revolutionize`, `unlock`, `leverage`, `seamless`, `cutting-edge`
- Hashtags of any kind
- Em dashes (suggest restructured sentences instead)
- Engagement bait: "Comment YES", "Like for Part 2", "Tag someone"
- Formulaic AI openers: "In today's world", "Let's dive in", "Here's the thing"

## Git Workflow

### Branches

- `main` — stable, published skill definitions
- `claude/add-claude-documentation-KXOza` — active development branch (current)

All changes should be developed on the designated feature branch and pushed before creating a PR.

### Commit Style

Keep commit messages concise and descriptive:

```
Add brand review skill for systemprompt.io content
Update terminology checks in brand review skill
Fix channel-specific checklist for LinkedIn posts
```

### Pushing Changes

```bash
git add <file>
git commit -m "your message"
git push -u origin claude/add-claude-documentation-KXOza
```

## Adding a New Skill

1. Create a new Markdown file: `skill_[scope]_[action].md`
2. Follow the section structure above (Name, Dependencies, Trigger, Inputs, Logic, Output)
3. List any prerequisite skills under `## Dependencies`
4. Define clear, testable checklist items — prefer specific rules over vague guidance
5. Specify an exact output format so Claude produces consistent results
6. Commit and push to the feature branch

## Key Personas and Context

- **Edward** — the human author behind all published content. Skill output should sound like Edward, not a generic AI. Voice is authoritative, practical, sophisticated, infrastructure-minded.
- **Target audiences:** CTOs/enterprise (peer-to-peer tone), SaaS partners (opportunity framing), individual users (warmer tone)
- **Core message:** "systemprompt gives you control of Claude"
- **Competitive frame:** Build-vs-buy, not systemprompt vs. specific platforms

## What AI Assistants Should Know

- This repository contains skill *specifications*, not runnable code. Do not attempt to execute or import these files.
- When editing a skill file, preserve all section headers exactly — they are part of the skill's contract with Claude Code.
- Never introduce em dashes, hashtags, or banned terminology into skill content.
- The free tier is described as a "demonstration environment", not the core product — maintain this framing in any documentation.
- White-label capabilities should only be mentioned in bottom-of-funnel contexts, not top-of-funnel content.
- If adding channel-specific checks, follow the pattern in the existing `### Channel-Specific Checks` section and include a dedicated `####` subsection for each channel.
