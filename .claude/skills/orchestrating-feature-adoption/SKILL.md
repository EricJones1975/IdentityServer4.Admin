---
name: orchestrating-feature-adoption
description: |
  Plans feature discovery, nudges, and adoption flows. Use when: Product work needs plans feature discovery, nudges, and adoption flows.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Orchestrating Feature Adoption

Advisory product skill for Founder/Pro operators. Use when: plans feature discovery, nudges, and adoption flows.

## Module

- Operating layer: Product
- Focus: Plans feature discovery, nudges, and adoption flows.

## When To Use

- Plans feature discovery, nudges, and adoption flows.
- Pair the recommendation with the repository's real product surfaces before editing; do not invent flows that the code does not support.

## How To Work

1. Read the nearest relevant files for the surface you are changing and reuse existing patterns.
2. Keep the change scoped to the smallest slice that delivers value.
3. Tie any claim (tracking, lifecycle, ranking, adoption) to a code path that actually performs it.

## Context7 Pointer

- For the tooling behind this work, fetch live docs with Context7 instead of relying on memory.
- Topic: product analytics, feature flags, and experiment tooling (e.g. PostHog).
- Workflow: `npx ctx7@latest library "<official name>" "<task query>"` then `npx ctx7@latest docs <libraryId> "<task query>"`.

## Boundary

- This skill is advisory product strategy grounded in the repo, not generic library documentation.
- If Context7 docs and local code disagree, preserve local behavior unless the task is an explicit migration.
