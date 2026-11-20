# ADR-0002 — The architecture as found

Status: **Accepted** · 2026-11-20 · written by hydraflow init

## Context

hydraflow init read this repository when it set the line up, before it changed anything. Each fact below is one it detected, stated as found.

## As found

- **Top-level folders git tracks**: .github, .vscode, customgpt, docker.

## To be written

- What each folder is for, and which way dependencies between them run.
- Which languages the tree is written in: no manifest init reads named one.
- Its entry points: none of the manifests init reads names one.
- How its tests are run: init found no test command it recognises.
- The decisions that shaped the tree, each as its own ADR from ADR-0003.

## Decision

The architecture is recorded as found and changed only by a later ADR that names what it changes.

## Consequence

- Until each fact above has its reason recorded, an agent reads what the tree is and not why; each later ADR adds one reason and names what it changes here.

## Enforcement-exempt

- `.hydraflow/layout.yaml` — this record describes the tree as hydraflow init found it, and a description is not a rule a check can hold; the roots it names are declared in that file, which hydraflow line-layout check holds.
