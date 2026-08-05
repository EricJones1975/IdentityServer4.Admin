---
name: structuring-offer-ladders
description: |
  Frames plan tiers, value ladders, and upgrade logic. Use when: Marketing work needs frames plan tiers, value ladders, and upgrade logic.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Structuring Offer Ladders

Advisory marketing skill for Founder/Pro operators. Use when: frames plan tiers, value ladders, and upgrade logic.

## Module

- Operating layer: Marketing
- Focus: Frames plan tiers, value ladders, and upgrade logic.

## When To Use

- Frames plan tiers, value ladders, and upgrade logic.
- Pair the recommendation with the repository's real marketing surfaces before editing; do not invent flows that the code does not support.

## How To Work

1. Read the nearest relevant files for the surface you are changing and reuse existing patterns.
2. Keep the change scoped to the smallest slice that delivers value.
3. Tie any claim (tracking, lifecycle, ranking, adoption) to a code path that actually performs it.

## Context7 Pointer

- For the tooling behind this work, fetch live docs with Context7 instead of relying on memory.
- Topic: conversion tracking, lifecycle email, and pixel/CAPI tooling (e.g. PostHog, Resend, Meta Conversions API).
- Workflow: `npx ctx7@latest library "<official name>" "<task query>"` then `npx ctx7@latest docs <libraryId> "<task query>"`.

## Boundary

- This skill is advisory marketing strategy grounded in the repo, not generic library documentation.
- If Context7 docs and local code disagree, preserve local behavior unless the task is an explicit migration.
