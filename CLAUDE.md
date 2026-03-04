# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Repository Is

This is a **documentation-only** repository — a diagnostic and remediation framework (the "Triage & Improvement Playbook") for interpreting AI agent eval results, diagnosing why test cases fail, and mapping failures to specific fixes. There is no source code, build system, or test suite.

## Repository Structure

The playbook is organized in four layers, each answering a different question:

| File | Layer | Purpose |
|---|---|---|
| `README.md` | Layer 1: Score Interpretation | Interpret pass rates, set thresholds, assess ship-readiness |
| `triage-decision-tree.md` | Layer 2: Failure Triage | Classify each failure's root cause and owner |
| `remediation-mapping.md` | Layer 3: Remediation | Map diagnosed root causes to specific config changes |
| `pattern-analysis.md` | Layer 4: Pattern Analysis | Identify systemic issues across failures |
| `worked-examples.md` | Worked Examples | Three end-to-end journeys demonstrating the full flow |
| `templates/failure-log-template.md` | Template | Lightweight and detailed failure logging formats |
| `templates/failure-log-template.csv` | Template | CSV version of the failure log |

The parent directory (`../`) contains the **scenario library** that defines quality signals and eval scenarios. The playbook references but does not duplicate the library.

## Key Concepts

Every eval failure is classified into one of **three root cause types** that determine who acts:

1. **Eval Setup Issue** — the test/grader is wrong; eval author fixes it
2. **Agent Configuration Issue** — the agent is genuinely wrong; agent builder fixes it
3. **Platform Limitation** — underlying platform behavior; platform team acts

## Core Design Principles

- Always verify the eval setup before investigating the agent (eliminate wrong work first)
- Every diagnostic path ends with: root cause -> owner -> specific action
- After any remediation, re-run the eval to verify; if failure persists, re-triage
- Compound causes are real — a single failure can have multiple root cause types
- Non-determinism is expected; establish baselines with 3+ runs

## Editing Guidelines

- The playbook uses a layered cross-referencing structure. When editing any file, preserve internal links (e.g., `[Layer 2](triage-decision-tree.md)`, anchor links like `#grader-validation`).
- Diagnostic questions in `triage-decision-tree.md` are numbered (1.1-1.5, 2.1-2.26, M.1-M.4). Worked examples reference these numbers — keep them in sync.
- `remediation-mapping.md` tables follow the pattern: **Failure Sub-Type | Remediation Action | Verification**. Maintain this structure for new entries.
- Score thresholds in `README.md` are explicitly labeled as example calibrations, not universal standards. Do not present them as fixed requirements.
- The `<!-- Internal Planning Notes -->` HTML comment block at the bottom of `README.md` contains non-public design decisions and open questions. Do not surface this content in user-facing edits.
