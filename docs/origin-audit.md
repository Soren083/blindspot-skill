# Origin Audit

This is the public, privacy-preserving audit note for Blindspot Skill.

The goal is to explain where the skill came from without exposing the private products, product domains, implementation details, reviewer threads, or local session identifiers that were used during development.

## Public Claim

Blindspot Skill was distilled from real product-development corrections across two large product projects.

The public numbers used in the README are:

| Public metric | Count | Meaning |
| --- | ---: | --- |
| Local conversations / task records | 481 | Coding-agent work records and task conversations used to locate correction moments |
| Correction-style interaction signals | 1,132 | User corrections, follow-up fixes, review notes, rework requests, and plan-review comments |
| Traceable blindspot patterns | 69 | Reusable agent failure patterns extracted from the correction set |

These counts are used to support the origin story of the skill. They are not meant to expose the underlying products or reproduce private project history.

## What Was Audited

The underlying audit inspected local Codex, Claude Code, and related coding-agent records. The private source set included:

| Evidence class | Public description |
| --- | --- |
| Full coding-agent transcripts | Complete local task histories where the user, reviewer, or agent later corrected the implementation or plan |
| Session indexes and prompt history | Metadata and prompt traces used to locate likely correction threads |
| Supporting message, diff, and model-call stores | Lower-confidence supporting evidence used only to validate recurring patterns |
| Repository changes | Code and document changes that confirmed a correction became real product work |

The public repository intentionally does not list private session IDs, local filesystem paths, product names, feature names, reviewer screenshots, or implementation routes.

## Evidence Rule

A correction counted only when it showed a concrete mismatch between the agent's work and product reality.

Examples of counted evidence:

- A user or reviewer pointed out that a success state was not actually proven.
- A later fix showed that one entry point still used old logic after another entry point was changed.
- A plan treated a prompt instruction as a hard guarantee, but the product needed deterministic enforcement.
- A release or deployment step changed one layer while users or reviewers still received another layer.
- A UI or copy change was technically accurate but confusing to real users.

Examples that did not count by themselves:

- Pure brainstorming.
- A subjective taste preference with no product-state or implementation risk.
- A build or deployment command with no user-visible mismatch.
- A precise marketing number without a traceable ledger.

## Redaction Rule

The public docs intentionally avoid:

- Project names and product domains.
- Named third-party products unless needed to explain a generic class of issue.
- Private session IDs, local paths, screenshots, and raw logs.
- Exact feature flows that would reveal unreleased product behavior.
- Detailed reviewer or compliance history.
- Business-specific formulas, scoring rules, or proprietary architecture.

The public version keeps the reusable lesson and removes the private incident.

## Pattern Families

The 69 traceable patterns were grouped into reusable blindspot families:

| Pattern family | What the correction exposed | Skill behavior added |
| --- | --- | --- |
| Source-of-truth confusion | The agent trusted a local flag, callback, cached value, or empty result as proof | Require proof for connected, saved, enabled, synced, deleted, fixed, and deployed |
| Entry-point drift | One route was fixed while another route, modal, shortcut, or settings path stayed old | Force a multi-entry audit before implementation |
| Old-logic remnants | A prompt, hardcoded string, fallback, or legacy branch survived the change | Search deterministic copy, fallback paths, seeds, and inverse logic |
| Proxy-state ambiguity | No data, missing fields, delayed sync, and denied access looked the same | Treat ambiguous external states as first-class UI states |
| Soft constraint mistaken for guardrail | The agent wrote an instruction but not an enforcement layer | Separate prompt guidance from deterministic validation |
| AI context leakage | Old user facts survived through memory, summaries, examples, or tool results | Audit every AI input channel, not just structured context |
| Release-layer mismatch | A fix landed in one layer while users/reviewers saw another layer | Require evidence for the exact delivery path |
| Transition and async gaps | The final screen was right, but intermediate frames or stale async results were wrong | Check transitions, cancellation, stale results, and loading states |
| User-language mismatch | Copy was technically correct but not understandable or actionable | Rewrite from the real user's decision point |
| Derived-data blast radius | One formula, setting, or source field changed downstream numbers and UI | Trace derived values, caches, displays, and AI-facing context |
| Test-harness mismatch | The proposed test could not observe the promised behavior | Match tests to what the system can actually prove |
| Visual-reference drift | The final asset or UI matched the theme but not the chosen reference | Compare against the selected reference, not only the concept |

## Mapping To The Skill

The audit directly shaped these Blindspot Skill sections:

| Skill section | Evidence basis |
| --- | --- |
| Human User Walkthrough | Corrections where the implementation worked technically but failed real user understanding |
| Source-of-Truth Audit | Corrections where the UI claimed a state without real proof |
| Regression Contract | Corrections where old behavior survived in another path |
| Blindspot Scenario Pass | Corrections involving no-data, skipped setup, denied access, stale state, and unusual runtime environments |
| AI Context Audit | Corrections involving stale AI memory, soft prompt rules, missing deterministic checks, or wrong output structure |
| Release Evidence | Corrections involving mismatched deploy, build, config, or review-visible versions |

## Public Summary

Blindspot Skill is not a generic checklist invented from imagination. It is a compressed, redacted pattern library extracted from real correction work.

The public repository shows the method and the reusable patterns. The private product incidents stay private.
