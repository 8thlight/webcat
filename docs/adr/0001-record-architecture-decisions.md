# ADR-0001 — Record architecture decisions

Status: **Accepted** · 2026-11-20 · written by hydraflow init

## Context

A decision that shapes this repository is made once and read many times, by people and by the agents that work on it. Read from the code alone, its reasons are lost.

## Decision

Each such decision is kept as a short record in docs/adr, numbered in order and never renumbered: its context, the decision, the alternatives it beat, and what follows from it. A decision changed later gets a new record that names the one it replaces.

## Consequence

- ADR-0002 records the architecture as hydraflow init found it. The next decision is ADR-0003.
- The standards this line is held to, and the count each started at, are in docs/standards/README.md.

## Enforcement-exempt

- `docs/adr` — keeping a record of each decision is a practice of the people who make them: once adr_enforcement is switched on a check holds each record's shape, and no check can hold that a decision was written down.
