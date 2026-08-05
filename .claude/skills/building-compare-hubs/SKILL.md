---
name: building-compare-hubs
description: |
  Creates comparison and alternative pages for discovery. Use when: SEO work needs creates comparison and alternative pages for discovery.
allowed-tools: Read, Edit, Write, Glob, Grep, Bash
---

# Building Compare Hubs

Advisory seo skill for Founder/Pro operators. Use when: creates comparison and alternative pages for discovery.

## Module

- Operating layer: SEO
- Focus: Creates comparison and alternative pages for discovery.

## When To Use

- Creates comparison and alternative pages for discovery.
- Pair the recommendation with the repository's real seo surfaces before editing; do not invent flows that the code does not support.

## How To Work

1. Read the nearest relevant files for the surface you are changing and reuse existing patterns.
2. Keep the change scoped to the smallest slice that delivers value.
3. Tie any claim (tracking, lifecycle, ranking, adoption) to a code path that actually performs it.

## Context7 Pointer

- For the tooling behind this work, fetch live docs with Context7 instead of relying on memory.
- Topic: metadata, structured data, sitemaps, and framework SEO primitives (e.g. Next.js Metadata API, schema.org).
- Workflow: `npx ctx7@latest library "<official name>" "<task query>"` then `npx ctx7@latest docs <libraryId> "<task query>"`.

## Boundary

- This skill is advisory seo strategy grounded in the repo, not generic library documentation.
- If Context7 docs and local code disagree, preserve local behavior unless the task is an explicit migration.
