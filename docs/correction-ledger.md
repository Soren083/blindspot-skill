# Correction Ledger

Blindspot Skill is built from correction-led product work.

This public ledger does not reproduce private project history. It summarizes the types of corrections that shaped the skill while keeping product names, domains, session identifiers, local paths, screenshots, reviewer details, and proprietary implementation details out of the repository.

## Why Corrections Matter

The strongest evidence was not that an agent wrote code. The strongest evidence was what happened after the code, plan, copy, or UI met reality:

- A user tested the product and found the state was not true.
- A reviewer saw a different build, string, or behavior than the agent expected.
- A teammate or second agent found that the plan contradicted the actual code.
- A follow-up fix revealed that the previous implementation covered only one path.

Those correction moments are useful because they expose the agent's hidden assumption.

## Public Evidence Scope

The public README uses these redacted origin numbers:

| Public metric | Count | How it is used |
| --- | ---: | --- |
| Local conversations / task records | 481 | Used to locate correction-heavy product-development work |
| Correction-style interaction signals | 1,132 | Used to identify repeated correction themes |
| Traceable blindspot patterns | 69 | The reusable patterns distilled into the skill |

The private audit also used full local transcripts, prompt history, message parts, diffs, and repository changes. Those raw sources remain private.

## Evidence Tiers

| Tier | Meaning | Public use |
| --- | --- | --- |
| A | Full transcript or code-change evidence plus a concrete correction | Can support a pattern family |
| B | Prompt or metadata evidence with enough context to infer a recurring issue | Can support repeated themes |
| C | Diff-only, model-call, or partial local-agent evidence | Supporting signal only |

Public claims should refer to pattern families, not private incidents.

## Correction Families

The 69 traceable blindspots collapse into the following public families.

| # | Correction family | Typical agent assumption | What Blindspot Skill now forces the agent to check |
| ---: | --- | --- | --- |
| 1 | False success state | Returning from a system sheet, API call, or async task means success | What proves the state is actually true? |
| 2 | No-data ambiguity | Empty results mean the user denied access or the system failed | Could this also be no records, delayed sync, unsupported data, or partial setup? |
| 3 | Entry-point drift | Fixing the visible button fixes the feature | Which other buttons, routes, modals, settings pages, deep links, and shortcuts reach the same behavior? |
| 4 | Hidden legacy branch | New prompt, copy, or UI replaces the old behavior everywhere | Are there hardcoded strings, fallbacks, seeds, inverse formulas, cached fields, or server shortcuts still using the old model? |
| 5 | Source-of-truth confusion | Stored value, display value, computed value, and AI context can be independently updated | Which value is canonical, which is projection, and which is compatibility/cache? |
| 6 | Derived-data blast radius | Changing one field affects only that field | Which downstream numbers, labels, charts, recommendations, AI responses, and tests also change? |
| 7 | Prompt as guardrail | Telling the model "do not say X" is enough | Is there deterministic filtering, validation, or repair when the output must never be wrong? |
| 8 | AI context leakage | Structured context is the only thing the model sees | What stale facts can leak through memory, summaries, examples, tool results, previous messages, or shortcut handlers? |
| 9 | Wrong proxy metric | A convenient field is close enough to the real decision | What is the actual business or user-state switch? |
| 10 | Test illusion | A planned test proves the promised behavior | Can the test harness actually observe the behavior, or only the plan/input? |
| 11 | Release-layer mismatch | A live update, backend deploy, native build, migration, and config change are interchangeable | Which layer will the real user or reviewer actually receive? |
| 12 | Transition blindness | The final screen is correct, so the interaction is correct | What does the user see during loading, returning, cancellation, retry, and navigation? |
| 13 | Async stale write | Leaving a screen or starting a new action cancels old async work automatically | Are there cancellation tokens, request versions, and stale-result guards? |
| 14 | Permission denial dead end | If a permission is useful, denial can be treated as an error | What still works after denial, and how does the user recover later? |
| 15 | Runtime-environment assumption | Device category, screen width, account state, or platform capability is obvious from the hardware | What does the runtime actually report? |
| 16 | Localization surface gap | Updating the main string updates every language and native surface | Which locale files, generated native resources, screenshots, and store assets still carry old wording? |
| 17 | Technical copy | Accurate wording is enough | Does a normal user understand what happened and what to do next? |
| 18 | Overexplained optional state | Every caveat should be shown prominently | If the state is optional and harmless, can the UI lower its salience? |
| 19 | Visual-reference drift | Matching the theme is the same as matching the selected reference | Compare the result against the actual chosen reference and constraints. |
| 20 | Scope expansion | A better system is always better than the original requested change | What was the original product intent, and what should stay intentionally simple? |
| 21 | Audience mismatch | A globally broad option set is automatically better | Does the default order and wording fit the launch audience and real usage context? |
| 22 | Mixed mental models | One screen can ask several related preference questions | Are these actually different decisions that users answer differently? |
| 23 | Internal metric leakage | Formulas, coefficients, ranks, or hidden scores help explain the system | Does the user need that internal metric to choose, or does it add cognitive load? |
| 24 | Incomplete chain audit | The visible component contains the whole bug | Trace create, edit, delete, sync, aggregation, display, AI context, and release path. |
| 25 | Public claim without proof | A strong marketing number can be directionally true | Keep a redacted ledger or soften the claim. |

## How To Use This Ledger

When a user asks an agent to implement a feature, the skill should:

1. Turn the request into likely user states.
2. Identify the state source of truth for each state.
3. Check every entry point that can reach the behavior.
4. Search for old logic that could survive the change.
5. Separate what the prompt asks from what the system enforces.
6. Ask what the real user, reviewer, teammate, or future maintainer would observe.
7. Require release evidence for the layer that actually changed.

## What Stays Private

The public ledger intentionally excludes:

- Product names.
- Exact product domains and feature names.
- Private session IDs and local paths.
- Raw transcripts, screenshots, and reviewer messages.
- Proprietary formulas, prompts, routing details, and implementation files.
- Case-by-case incident narratives that could identify the products.

The skill keeps the lesson. The project details stay out of the repository.
