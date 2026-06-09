<p align="center">
  <img src="assets/readme-banner.png" alt="Blindspot Skill - Make AI agents think through what they are about to miss" width="100%" />
</p>

# Blindspot Skill

<p align="center">
  <em>Make AI coding agents think through what they are about to miss.</em>
</p>

<p align="center">
  <img src="assets/blindspot-skill-logo.png" width="84" height="84" alt="Blindspot Skill" />
</p>

<p align="center">
  <a href="README.zh-CN.md"><img src="https://img.shields.io/badge/中文说明-README.zh--CN.md-22c55e?style=for-the-badge&labelColor=1e293b" alt="Chinese README"/></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-fbbf24?style=for-the-badge&labelColor=1e293b" alt="MIT License"/></a>
  <a href="#install"><img src="https://img.shields.io/badge/Tools-Codex%20%C2%B7%20Claude%20Code-111827?style=for-the-badge&labelColor=1e293b" alt="Supported agents"/></a>
</p>

Blindspot Skill is a pre-implementation skill for AI coding agents.

It was distilled from **376 real Codex and Claude Code mistakes** caught during product development: bugs that compiled, plans that sounded right, UI that looked cleaner, and agent answers that were technically plausible but still failed once a real human used the product.

The pattern was painfully consistent: AI agents are fast at code, but they miss the boring product reality around the code. They forget entry points. They trust local flags. They confuse empty data with failure. They call prompt text a guardrail. They ship UI copy that only engineers understand. They fix the screen in front of them and miss the release path users actually receive.

Blindspot Skill turns those mistakes into a repeatable pre-build pass. Before the agent writes code, it has to walk through the request like a real user and hunt for the hidden product, state, regression, source-of-truth, AI-context, visual, integration, and release-path blind spots it would normally skip.

## Who This Is For

Blindspot Skill is mainly for people using AI agents to build real products.

You do not need to be a professional engineer or a full-time product manager to use it. In fact, it is most useful when you have a product idea, screenshot, bug report, competitor reference, or "this feels wrong" instinct, but you do not know how to spell out every state, API, permission, edge case, regression, and release constraint before asking an agent to code.

Use it if you are:

- an indie builder, founder, designer, operator, creator, or domain expert building with Codex, Claude Code, or another coding agent
- a non-technical or semi-technical product owner who wants the agent to ask better questions before implementation
- a product manager who wants a fast pre-build pass over user flows, success states, copy, edge cases, and release risk
- an engineer who wants the agent to stop at the product boundary before jumping into code

The skill does not replace your judgment. It helps both you and the agent notice the things neither side had fully specified yet.

## What Human Corrections Revealed

| What 376 real mistakes exposed | Agent blind spot |
| --- | --- |
| The UI claimed something was connected, saved, or enabled when the system could not prove it | False success states |
| Empty external data was treated as failed permission or failed sync | No-data vs denied/unknown ambiguity |
| One entry point was fixed while onboarding, settings, modal, or detail page still used old logic | Entry-point drift |
| The final screen was correct, but the transition briefly flashed the wrong state | Transition-state blindness |
| A live update was expected to fix behavior that actually required native, backend, config, or review changes | Release-layer mismatch |
| AI output repeated outdated facts from old memory, summaries, examples, or prompt text | AI context leakage |
| Prompt instructions were described as hard guardrails even though the model could ignore them | Soft guardrails mistaken for deterministic enforcement |
| A required visual or structured response degraded into plain text | Structured-output omission |
| Copy was technically accurate but real users could not quickly understand what to do | User-language blindness |
| A read path was unified but write paths, caches, projections, or related surfaces stayed stale | Partial-chain fixes |

If you use AI coding agents to build real products, this skill is meant to catch the mistake before your users, reviewers, or teammates do.

## Why It Exists

Most AI coding failures do not start with syntax.

They start when the agent does not ask:

- What would make this success state false?
- What does a first-time user believe after seeing this copy?
- Which other button, route, modal, job, or setting uses the same behavior?
- Can old data, cache, memory, or async responses overwrite the latest user action?
- Is this prompt rule actually enforceable?
- Will users and reviewers receive the matching frontend, backend, native, and config version?

Blindspot Skill makes the agent answer those questions before it writes code.

## Quick Demo

User:

```md
Make this permission flow simpler.
```

Without Blindspot Skill:

```md
The agent rewrites the copy and ships a cleaner screen.
```

With Blindspot Skill:

```md
The agent first checks:

1. What proves the permission is really enabled?
2. What should the UI say if the platform returns but the result is unknown?
3. Do onboarding, settings, and reconnect buttons use the same flow?
4. Can this ship through a live update, or does it need a native build?
5. What does an impatient first-time user understand from the title and button?
```

The second version prevents a cleaner-looking UI from lying to users.

## What It Catches

| Blind spot | What it prevents |
| --- | --- |
| False success state | UI says saved, connected, synced, or paid before there is proof |
| Preview vs final | Half-edited or preview data becomes real too early |
| Entry-point drift | Similar buttons behave differently across screens |
| Same data everywhere | Home, detail, export, notification, and AI summary disagree |
| External no-data ambiguity | Empty source data is mistaken for denial or failure |
| Old state overwrite | Slow requests, caches, jobs, or webhooks revert fresh user actions |
| Permission denial | Rejecting one permission blocks the whole product unnecessarily |
| AI context leakage | Old memory, summaries, prompt examples, or tool results leak stale facts |
| Soft guardrails | Prompt-only rules are mistaken for deterministic validation |
| Visual regression | Type checks pass while small screens, tablets, long text, or large font break |
| User-language blindness | Internal formulas and vague abstractions reach the user |
| Release mismatch | Users, reviewers, frontend, backend, native build, and config see different versions |

## Install

### Codex

Copy the skill directory into your Codex skills folder:

```bash
mkdir -p ~/.codex/skills
cp -R skills/codex/blindspot ~/.codex/skills/blindspot
```

Restart Codex or open a new session if the skill list does not refresh immediately.

### Claude Code

Copy the skill directory into your Claude skills folder:

```bash
mkdir -p ~/.claude/skills
cp -R skills/claude/blindspot ~/.claude/skills/blindspot
```

You can also import the packaged file:

```text
packages/blindspot.skill
```

## Use

```md
Use agent-blindspot before coding.

My request:
Build a customer import feature.
```

The skill should output:

- a blindspot read
- likely directions
- real-user walkthrough
- source-of-truth audit for success states
- existing behavior contract for regressions
- AI context audit when AI output is involved
- release evidence requirements
- at most 3 important questions
- after confirmation, a buildable development brief

## Examples

See:

- [Customer import](examples/customer-import.md)
- [Subscription paywall](examples/subscription-paywall.md)
- [Calendar event](examples/calendar-event.md)
- [Admin dashboard](examples/admin-dashboard.md)
- [AI summary feature](examples/ai-summary-feature.md)

Each example includes:

1. Original fuzzy request
2. Skill questions
3. Development brief outline

## Evaluation Ideas

This skill is not evaluated by whether it writes code. It is evaluated by whether it catches hidden product decisions before code is written.

A good response should:

- ask no more than 3 questions at a time
- avoid database/API/schema questions before product rules are clear
- include a not-doing section when scope is cut
- explain what could break if something is skipped
- catch hidden state, data, context, failure, permission, AI, visual, or release problems
- downgrade success states that do not have a verifiable source of truth
- include negative acceptance checks for high-risk requests
- produce a brief a coding agent can implement after the user confirms direction

See [eval prompts](evals/prompts.json).

## Project Structure

```text
blindspot-skill/
  README.md
  README.zh-CN.md
  assets/
  skills/
    codex/blindspot/SKILL.md
    claude/blindspot/SKILL.md
  packages/
    blindspot.skill
  docs/
    patterns.md
  examples/
  evals/
```

## License

MIT
