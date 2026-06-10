# Origin Audit

This document records how Blindspot Skill was checked against the local Codex and Claude Code conversations it came from.

The short version: the skill is genuinely grounded in real local product-development corrections, especially the KaloCam debugging and review work. The public README uses the "376 correction moments" line as a memorable origin claim, while this audit keeps the evidence tiers honest: the local corpus contains 300 Codex session bodies, 377 Claude local session identifiers, and supporting PieBox stores. The highest-signal correction threads are itemized in [correction-ledger.md](correction-ledger.md).

## Audit Scope

Local sources inspected during this audit:

| Source | Count | Notes |
| --- | ---: | --- |
| Codex session JSONL files | 300 | 296 active local `~/.codex/sessions` JSONL bodies plus 4 archived session JSONL bodies |
| Claude Code retained main transcript JSONL files | 23 | Local `~/.claude/projects`; complete message/tool transcript bodies currently retained |
| Claude Code retained subagent transcript JSONL files | 6 | Local `~/.claude/projects/**/subagents`; useful execution traces, not user-facing main sessions |
| Claude Desktop Code session indexes | 30 | Local `~/Library/Application Support/Claude/claude-code-sessions`; metadata/title/cwd/turn counts, not full message bodies |
| Claude Code standalone transcript exports | 2 | Local `~/.claude/transcripts`; complete transcript-style JSONL files |
| Claude Code usage event session IDs | 94 | Local `~/.claude/usage-insights/events.jsonl`; proves session activity, but usually no full message text |
| Claude Code prompt-history session IDs | 288 | Local `~/.claude/history.jsonl`; user prompt history only, not assistant replies or diffs |
| Unique Claude local session identifiers | 377 | Union of usage-event session IDs and prompt-history session IDs; 5 IDs overlap |
| Claude model API dumps | 2,983 | Local PieBox `llm-fetch-dumps/*claude*.json`; raw provider request/response dumps, classified separately from Claude Code sessions |
| PieBox local sessions | 7 | Local `~/.local/share/piebox/storage/session` |
| PieBox message files | 232 | Local `~/.local/share/piebox/storage/message`; paired with `part` files for user text |
| PieBox session diffs | 322 | Local `~/.local/share/piebox/storage/session_diff` |
| PieBox LLM fetch dumps | 4,858 | Local `~/.local/share/piebox/log/llm-fetch-dumps`; 2,983 Claude-named dumps |
| Primary Codex product thread | 1 | Session `019e8b8f-f84b-7e91-a439-2eb29deb93eb`, 296 user turns |
| Additional Codex product threads deeply inspected | 10+ | App Review/build thread `019e6736...`, App Review/Coach thread `019ea510...`, iPad thread `019e870b...`, Coach data mismatch thread `019db51e...`, plus meal history, fasting, exercise, notification, payment, and build/deploy threads |
| Claude Code review sessions deeply inspected | 8+ | Sessions `07dcd81a...`, `f4dffc8a...`, `bc98a5f6...`, `00123bd1...`, `59585b34...`, `377470df...`, and related Coach/payment/planner document-review sessions |
| KaloCam git fixes cross-checked | 30+ | Fix commits from June 3-9, 2026 |

This is not a claim that every Codex file, Claude local session identifier, or PieBox dump has been fully hand-labeled. The 23 Claude main transcript JSONLs and 6 subagent traces are the currently retained full Claude Code transcript bodies; the larger 377 figure is a local-history/index count. PieBox is included as supporting local agent evidence, but its retained user-facing sessions are much smaller than its raw LLM dump store. This is a public audit of the highest-signal sessions that directly shaped the skill.

## Claude Search Method

The Claude Code audit used several local stores because the current Claude Desktop and Claude Code installations keep different levels of detail in different places:

- `~/.claude/projects`: retained full JSONL transcript bodies. This is the only Claude source counted as complete main-session transcript evidence.
- `~/.claude/projects/**/subagents`: retained JSONL traces from delegated subagents. These help explain agent behavior but are separated from user-facing main sessions.
- `~/Library/Application Support/Claude/claude-code-sessions`: desktop session metadata. These files include title, cwd, model, turn count, branch/worktree, and sometimes `cliSessionId`, but not full messages.
- `~/.claude/history.jsonl`: user prompt history. This proves prompts and session IDs existed, but does not contain assistant replies, tool outputs, or code diffs.
- `~/.claude/usage-insights/events.jsonl`: event history. This proves session starts, prompt submits, stops, and cwd values, but usually does not contain message text.
- `~/.claude/transcripts`: standalone transcript JSONL exports.
- `~/.local/share/piebox/log/llm-fetch-dumps/*claude*.json`: raw Claude provider request/response dumps. These were classified separately because they are model/API call logs, not Claude Code conversations.
- `~/.local/share/piebox/storage/message`, `part`, `session`, and `session_diff`: PieBox local session/message/diff stores. These were inspected separately because they are not Codex or Claude Code session bodies.

The 377 Claude number is the union of unique session identifiers in `history.jsonl` and `usage-insights/events.jsonl`; only five identifiers overlapped between those two stores during the audit. The inspectable full-transcript subset is much smaller, so public claims should avoid implying that all 377 identifiers have complete retained transcripts.

The correction-level evidence is itemized in [correction-ledger.md](correction-ledger.md). That ledger is the strongest evidence source for the actual Blindspot Skill rules.

## Counting Rule

A correction counts as evidence when at least one of these is true:

- A user or reviewer pointed out that the previous agent plan, code, UI, or explanation missed a real product state.
- A code-grounded review found a contradiction between the plan and the actual implementation.
- A later commit fixed a concrete issue that was caused by an earlier incomplete implementation or incomplete requirement.
- The agent confused a proxy signal with the real source of truth, a prompt instruction with a hard guardrail, or a release/update path with the layer users would actually receive.

These do not count as product-bug evidence by themselves:

- Pure brainstorming without a prior miss.
- Taste iteration with no underlying user-state or implementation error.
- Deployment/build commands unless the mismatch caused users or reviewers to see the wrong behavior.
- A numeric marketing claim that has no ledger.

## Audited Corrections

| Evidence | What the human correction exposed | General blindspot now covered |
| --- | --- | --- |
| Codex `019e8b8f...`: calorie migration review | Coach "set goal to 1800" still used the old BMR baseline, so changing only the display would silently overfeed the goal by the TDEE-BMR gap | Source-of-truth audit; read/write/projection consistency |
| Codex `019e8b8f...`: calorie migration review | A hardcoded Coach string still taught the old "exercise gives extra eating room" model even after prompt/i18n changes | Deterministic copy surfaces, not just prompts |
| Codex `019e8b8f...`: calorie migration review | Weight changes updated the input but not cached calorie targets, contradicting "instant update" | Cache/projection staleness; write-time vs read-time invariants |
| Codex `019e8b8f...`: calorie migration review | Safety calorie floors differed across paths, so "reuse existing behavior" was false | Cross-path rule unification |
| Codex `019e8b8f...`: food preference spec review | Two activeScore formulas coexisted; one double-penalized negative preferences and mishandled no-scene scoring | Old spec remnants; formula contradiction scan |
| Codex `019e8b8f...`: food preference spec review | Append-only snapshots were underspecified and could grow per chat turn | Lifecycle, retention, generation cadence |
| Codex `019e8b8f...`: food preference spec review | Deduplication keys could swallow legitimate repeated behavior events | Idempotency vs valid repeated events |
| Codex `019e8b8f...`: onboarding food preference redesign | The agent drifted from "replace country selection" into a complicated preference system | Preserve original product intent before expanding scope |
| Codex `019e8b8f...`: onboarding activity copy | The UI exposed activity multipliers and step ranges users may not know; the user corrected it toward workout frequency and plain descriptions | Real-user language; use what users can actually answer |
| Codex `019e8b8f...`: US launch meal options | US-first launch still surfaced Taiwan/China-heavy options too prominently | Audience and market-context pass |
| Codex `019e8b8f...`: Apple Health states | Allow, deny, skip, reconnect, and return-from-Health all needed different UI states; the earlier implementation blurred them | State truth table; every success/failure/unknown path |
| Codex `019e8b8f...`: Apple Health reconnect | Reconnect entry points did not match; onboarding and in-app flows behaved differently | Entry-point drift |
| Codex `019e8b8f...`: Apple Health skip | "Continue without Health" briefly flashed the wrong page before advancing | Transition-state blindness |
| Codex `019e8b8f...`: iPad HealthKit | No Health data on iPad was mistaken for no permission, and denial could be shown as connected | No-data vs denied vs unknown; proxy state warning |
| Codex `019e8b8f...`: HealthKit write probe | A write permission/probe was needed because read-only authorization cannot be reliably observed in that environment | True source-of-truth proof, not local intent |
| Codex `019e8b8f...`: OTA/native confusion | Several fixes were invisible until the correct deploy/OTA/native package was shipped | Release-layer evidence |
| Codex `019e8b8f...`: Coach meal review | "Analyze my meals" should produce visual cards, but the implementation degraded to text | Structured-output requirement |
| Codex `019e8b8f...`: Coach fasting leak | Fasting was closed in structured context but leaked from prompt text and old memory | AI context audit across prompt, memory, summary, examples, tools |
| Codex `019e8b8f...`: Coach copy | Abstract phrases like "more stable" were technically acceptable but not concrete enough for users | User-language blindness |
| Codex `019e6736...`: TestFlight/App Review build flow | An OTA after a TestFlight build caused reviewers to see an in-app update prompt after download | Release path must match reviewer-visible build |
| Codex `019e6736...`: Offline Coach screen | Offline startup caused severe screen flicker because AI-backed insight loading did not have a stable offline/empty state | Offline and loading-state acceptance |
| Codex `019e6736...`: Exercise backfill | Manually logging exercise for a past date still saved/displayed as today | Business date vs created date |
| Codex `019e6736...`: Multiple camera/logging entries | Photo logging had many entry points that needed the same save/display contract | Entry-point drift |
| Codex `019e6736...`: Speech recognition cancel | Leaving during recognition did not cancel the async result and later wrote stale text back into the UI | Old async overwrites new action |
| Codex `019e6736...`: Camera permission denial | Denying a native permission led to a dead-end screen with no working recovery or back path | Permission denial and partial usability |
| Codex `019e6736...`: HealthKit denial after native sheet | The app still showed connected after the user denied Apple Health | False success state; platform callback is not proof |
| Codex `019e6736...`: Review data-source evidence | Frontend claimed data sources, but source labels/help were incomplete or legally ambiguous | Public claim vs evidence surface |
| Codex `019e6736...`: Today request storm | Fast date switching and first-meal events could trigger repeated requests and stale UI behavior | Request dedupe, abort, and stale guards |
| Codex `019e870b...`: iPad compatibility | The plan assumed a 700pt tablet width, but iPhone-only apps on iPad report iPhone-width compatibility windows | Non-default environment; do not assume device category from hardware |
| Codex `019db51e...`: Home vs Coach goal mismatch | The home screen and Coach answer used different goal numbers | Same data everywhere; shared source of truth |
| Codex `019db51e...`: Coach answer verbosity | The user wanted chat plus lightweight visual analysis, not long text or cards without conversational context | Structured output with human conversation order |
| Codex `019ea510...`: App Review purpose strings | Only changing base config missed localized native strings, so the shipped binary still carried old sensitive wording | Native/i18n/config surfaces |
| Codex `019ea510...`: Coach medical/legal boundary | Legal feedback required evidence and boundaries without making every message feel like medical advice | Safety copy that matches product risk without harming UX |
| Codex `019ea510...`: Meal-diagnosis shortcut | Visual tool wiring on the AI main chain missed deterministic meal-diagnosis replies that returned earlier | Actual execution path audit |
| Claude `07dcd81a...`: Coach nutritionist review | The real fasting leak source was prompt/memory, not the structured fasting context | Root-cause check across all AI input channels |
| Claude `07dcd81a...`: Coach nutritionist review | `forbiddenClaims` were prompt text, not deterministic guardrails | Soft prompt vs hard enforcement |
| Claude `07dcd81a...`: Coach nutritionist review | The plan omitted the actual planner/risk/guardrails/critic layer wired into the main chain | Existing architecture scan before adding modules |
| Claude `07dcd81a...`: Coach nutritionist review | A proposed new card duplicated existing `today_checkin` intent and contradicted existing card types | Reuse existing mechanisms; avoid parallel concepts |
| Claude `07dcd81a...`: Coach nutritionist review | Fixtures could not verify LLM output text unless the issue became a deterministic guardrail | Test what the test harness can actually observe |
| Claude `07dcd81a...`: Coach nutritionist review | A guardrail depended on a missing `fastingActive` field and would infer false from absence | Missing first-class source-of-truth field |
| Claude `07dcd81a...`: Coach nutritionist review | Token scanning for fasting terms would block legitimate user questions and safe negations | Guardrails need semantic scope, not broad substring bans |
| Claude `07dcd81a...`: Coach nutritionist review | Card selection used meal count, while the real "avoid judgment" switch used `shouldAvoidDailyJudgment` | Wrong proxy metric |
| Claude `bc98a5f6...`: App Review/HealthKit review | Base purpose strings were fixed, but localized InfoPlist strings still shipped old "calibrate" wording | Native/i18n/config surfaces, not only one file |
| Claude `bc98a5f6...`: App Review/HealthKit review | The app-review plan missed a health consent gate and several native permission surfaces | Reviewer-environment and release-surface audit |
| Claude `00123bd1...`: Coach consistency review | A proposed `coach-reality` module would duplicate already-existing `coach-decision` and `coach-agent` infrastructure | Avoid parallel architecture when fixing consistency |
| Claude `00123bd1...`: Coach consistency review | The doc referenced non-existent modules and missed the real bypass path in meal diagnosis | Plan-code drift; inspect real routing before implementation |
| Claude `00123bd1...`: Coach visual tool review | The headline visual-card scenarios bypassed the planned AI wiring points | Trace the actual execution path, not the intended one |

## Mapping To Skill Rules

The audited corrections support these Blindspot Skill sections:

| Skill section | Evidence basis |
| --- | --- |
| Human User Walkthrough | Activity copy, food preference UI, HealthKit states, Coach language |
| Source-of-Truth Audit | HealthKit permission proof, calorie/TDEE projections, false connected states |
| Regression Contract | Multiple onboarding/settings/reconnect entry points, old hardcoded strings |
| Blindspot Scenario Pass | No-data ambiguity, transition flicker, release mismatch, AI context leakage |
| AI Context Audit | Fasting prompt/memory leak, visual-card tool requirement, soft guardrails |
| Release Evidence | OTA/native/build/App Review mismatches |

## Gaps Found In The Skill During This Audit

The skill covered the big categories, but the audit revealed four improvements that needed to be added:

- Public evidence claims need their own source-of-truth discipline. If a README says "N real mistakes", there must be a ledger or the claim should be softened.
- Proxy signals need stronger language. "No data", "missing field", "callback returned", or "old cache absent" are not proof of denial, success, or failure.
- Transition states deserve explicit review. The final screen can be correct while the user still sees a wrong intermediate frame.
- Existing architecture must be scanned before proposing new modules, especially for AI pipelines with planners, guardrails, critics, and deterministic short-circuits.
- Device and release assumptions must be checked against what the runtime actually reports: an iPad running an iPhone-only app is not the same as a tablet-width layout, and an OTA is not the same as a native App Review build.

These points are now folded back into the README, pattern library, and skill instructions.
