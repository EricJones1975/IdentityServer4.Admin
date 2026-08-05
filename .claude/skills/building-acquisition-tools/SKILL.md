---
name: building-acquisition-tools
description: |
  Designs lead magnets or free tools for acquisition. Use when: Marketing work needs designs lead magnets or free tools for acquisition.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Building Acquisition Tools

Advisory marketing skill for Founder/Pro operators. Use when: designs lead magnets or free tools for acquisition.

## Module

- Operating layer: Marketing
- Focus: Designs lead magnets or free tools for acquisition.

## When To Use

- Designs lead magnets or free tools for acquisition.
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
