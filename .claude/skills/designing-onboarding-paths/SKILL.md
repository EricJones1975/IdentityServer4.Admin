---
name: designing-onboarding-paths
description: |
  Designs onboarding paths, checklists, and first-run UI. Use when: Product work needs designs onboarding paths, checklists, and first-run ui.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Designing Onboarding Paths

Advisory product skill for Founder/Pro operators. Use when: designs onboarding paths, checklists, and first-run ui.

## Module

- Operating layer: Product
- Focus: Designs onboarding paths, checklists, and first-run UI.

## When To Use

- Designs onboarding paths, checklists, and first-run UI.
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
