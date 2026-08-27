---
name: andrej-karpathy-skills
description: Karpathy-derived coding behavior rules for LLMs.
version: 0.1.0
author: Andrej Karpathy (multica-ai), Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [coding, discipline, llm-behavior, karpathy]
    related_skills: []
---

# Andrej Karpathy Skills

Behavioral guidelines to reduce common LLM coding mistakes, derived from Andrej Karpathy's observations.

## When to Use

- Before coding: think first, surface assumptions and tradeoffs.
- Any coding task: check for over-engineering, choose minimal change.
- Editing existing code: surgical changes only, no adjacent refactoring.

## Rules

### 1. Think Before Coding
- Don't assume. Don't hide confusion. Surface tradeoffs.
- State assumptions explicitly before implementing.
- If multiple interpretations exist, present them all.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

### 2. Simplicity First
- Minimum code that solves the problem. Nothing speculative.
- No features beyond what was asked.
- No abstractions for single-use code.
- No "flexibility" or "configurability" that wasn't requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.
- Ask: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

### 3. Surgical Changes
- Touch only what you must. Clean up only your own mess.
- Don't "improve" adjacent code, comments, or formatting.
- Don't refactor things that aren't broken.
- Match existing style, even if you'd do it differently.
- If you notice unrelated dead code, mention it — don't delete it.
- When your changes create orphans, remove imports/variables/functions that YOUR changes made unused.
- Don't remove pre-existing dead code unless asked.

Test: Every changed line should trace directly to the user's request.

### 4. Goal-Driven Execution
- Define success criteria. Loop until verified.

Transform tasks into verifiable goals:
- "Add validation" → "Write tests for invalid inputs, then make them pass"
- "Fix the bug" → "Write a test that reproduces it, then make it pass"
- "Refactor X" → "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:
```
1. [Step] → verify: [check]
2. [Step] → verify: [check]
3. [Step] → verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require constant clarification.

## Verification

These guidelines are working if:
- Fewer unnecessary changes in diffs
- Fewer rewrites due to over-engineering
- Clarifying questions come before implementation, not after mistakes
