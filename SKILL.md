---
name: prd-kit
description: "Manual-only workflow for creating business-readable, cross-functional PRDs through two modes. Invoke explicitly with $prd-kit to draft, review, or publish a PRD/spec for business stakeholders and developers."
---

# PRD Kit

## Invocation Guard

Run this skill only when the user explicitly invokes `$prd-kit`. Do not infer invocation from requests that mention PRDs, specifications, planning, product requirements, or this skill by name without `$prd-kit`.

Without an explicit `$prd-kit` invocation, do not start discovery, grilling, document generation, file writes, or external-work-item synchronization under this workflow.

## Operating Model

Use this skill as the wrapper for cross-functional PRD production. It coordinates:

- `grill-me` for resolving the product decision tree one question at a time.
- `grill-with-docs` for resolving terminology against the project's documented domain language.
- `to-spec` for local source-of-truth discipline, unresolved decisions, stop conditions, implementation boundaries, and ticket readiness.
- `prd` from `github/awesome-copilot` for discovery, executive summary, personas, user stories, acceptance criteria, risks, and roadmap quality.
- `prd-kit` rules for cross-functional readability across CEO, operations, brand, marketing, partner teams, support, development, and QA.

Before drafting, discover and read these companion skills by their installed names:

- `grill-me`
- `grill-with-docs`
- `to-spec`
- `prd`

If any companion skill is missing, continue with this skill and explicitly report which source was unavailable.

## Mode Selection

Default to Mode 1 when the user is still shaping a large framework, PRD strategy, business rule set, or cross-team launch plan. Use Mode 1 when the user says phrases like `先聊框架`, `先 grill`, `先定大方向`, `还没完全想清楚`, or `最后再进开发`.

Use Mode 2 when the user already has enough facts and wants a PRD/spec now, especially when the user says phrases like `直接出 PRD`, `基于当前讨论`, `进入开发`, `to-spec`, or `输出可执行 PRD`.

If the requested mode is unclear and choosing would materially change output, ask one concise question: `先用 Mode 1 聊清框架，还是用 Mode 2 直接产出 PRD？`

## Mode 1: Framework First

Use this for broad product planning before development.

1. Inspect the project's existing PRDs, `CONTEXT.md`, ADRs, and prior `grill-with-docs` outputs. Reuse their confirmed business terms verbatim.
2. When a required business term is new, ambiguous, or conflicts with those sources, run `grill-with-docs` before continuing. Do not invent a replacement term.
3. Run the `grill-me` interview: ask one question at a time, recommend an answer, and resolve the decision tree until the large framework is coherent.
4. Produce a `Framework Brief` instead of a final implementation PRD. It must include decisions, unresolved questions, non-goals, stakeholder impact, and risks.
5. Format the brief for cross-team review using `references/prd-template.md`, but do not force engineering details that are not ready.
6. Run `references/quality-gate.md`.
7. Run the confirmed-decision closure process before presenting the framework brief.
8. Only after the user confirms the framework, invoke `to-spec` discipline to convert the approved framework into an implementation-ready local PRD/spec.

Output names for Mode 1:

- `framework-brief.md`
- `open-questions.md`
- `cross-functional-review.md`
- later, after approval: `PRD.md` or repo-local `to-spec` location

## Mode 2: Direct PRD

Use this when the current context is already concrete enough for a PRD.

1. Gather source material from the conversation, repo docs, Figma/design links, tickets, APIs, schemas, product decisions, stakeholder notes, and prior `grill-with-docs` outputs.
2. Reuse the confirmed business terms in those sources verbatim. When a required term is new, ambiguous, or conflicts with the documented language, run `grill-with-docs` before drafting; do not mock a business term.
3. Use `grill-me` selectively for only the missing high-impact decisions; do not re-interview for known facts.
4. Apply `to-spec` discipline: do not invent money, data, permission, production-write, account, launch, or legal semantics. Mark unresolved decisions as `待确认`.
5. Apply `prd` discovery: identify the core problem, success metrics, constraints, user flow, non-goals, user stories, acceptance criteria, and risks.
6. Generate a cross-functional PRD using `references/prd-template.md`.
7. Run `references/quality-gate.md` before presenting the PRD.
8. Run the confirmed-decision closure process before presenting the PRD.
9. If facts are materially missing, lead with `Open Questions` before the draft and state what cannot be finalized.

## Output Policy

Produce Chinese Simplified by default unless the user asks otherwise.

All generated document section titles must be Chinese. Write business rules in confirmed domain language that a non-developer can understand. Translate implementation facts such as database fields, enum values, API parameters, table names, code paths, internal component names, and technical stack names into their business meaning; do not expose them in a cross-functional PRD merely for precision.

Use this precedence for business terms: confirmed `grill-with-docs` output, project glossary or ADR, approved PRD, then user-confirmed wording. If none exists, mark the term `待确认` and run `grill-with-docs`; never mock a plausible-sounding business term. Do not add a `技术栈`, `关联技术`, or similarly named product-description section. Keep technical mappings outside the distributed PRD by default. Include a weakly presented, separate traceability note only when the user explicitly asks for it or the downstream implementation handoff cannot proceed without it; it must not replace business wording or describe product value through implementation choices.

Keep delivery-process mechanics out of the distributed PRD: do not put external work-item carriers, branches, local implementation files, ticket formats, or repository workflow rules in `范围`, `不做什么`, product rules, or acceptance criteria. Apply those rules internally through `to-spec` and the active repo workflow. Mention them externally only when the user explicitly requests a handoff note and they materially affect a stakeholder decision.

For Mode 1, do not create implementation tickets or synchronize an external work item until the user approves the framework. For Mode 2, follow `to-spec` local source-of-truth rules for repo-local file location and external-work-item sync only when the user explicitly asks to publish or sync.

## Publication and External Work-Item Sync

Before presenting a new or materially revised PRD, decide its delivery state: `当前复核草案` or `同步外部父工作项`.

- Default to `当前复核草案` when the user has not explicitly requested publishing or synchronization. Set the document status to indicate it is a review draft; do not update an external system.
- Use `同步外部父工作项` only when the user explicitly requests synchronization, names a parent work item as the source of truth, or the active repo workflow requires it to carry the canonical PRD. The carrier can be GitLab, GitHub, Linear, Jira, or another user-specified system. Set the status to indicate that synchronization is pending until it actually succeeds.
- Before updating a parent work item, read its current content and compare it with the new PRD. Preserve still-valid acceptance, links, and decisions; surface conflicts instead of overwriting them. Synchronize only after confirmed-decision closure passes.
- After a successful update, set the PRD status to identify the synchronized parent work item and update the document time. If access, parent-work-item identity, carrier, or the synchronization decision is unavailable, keep the document as `当前复核草案` and state the blocker outside the PRD.

## Confirmed-Decision Closure

Before writing the draft, create an internal working list of important confirmed decisions. For each decision, record its business-language wording, source, and the PRD section where it belongs. Do not add this working list as a reader-facing PRD module.

Classify every decision candidate as exactly one of: `已确认`, `待确认`, or `存在冲突`. A decision may appear in `待确认问题` only when no confirmed source exists, sources conflict, or the user explicitly leaves it unresolved.

Run this loop before delivery and again after every material revision:

1. Source-to-draft: compare every `已确认` decision against the draft. Replace stale or vague wording with the confirmed business wording.
2. Pending-list repair: remove every confirmed decision from `当前待确认` and `待确认问题`; move it into the relevant requirement, rule, acceptance criterion, or risk.
3. Draft-to-source: inspect every `待确认` item in reverse. If a source already resolves it, repair the draft and reclassify it as `已确认`; if sources conflict, mark the conflict and do not choose silently.
4. Final review: confirm that each important confirmed decision has one unambiguous home in the PRD and no conflicting or pending duplicate. Repeat the loop until the check passes.

Block final delivery when a high-impact decision is both marked `待确认` and already resolved by an available source, or when conflicting sources have not been surfaced. State the exact unresolved decision, source conflict, owner, and required confirmation instead of presenting the PRD as final.

## Structure Depth

Match the output structure to actual complexity. Do not force the full PRD template when the request is small.

Use `轻量模式` for copy changes, display-only UI changes, narrow configuration, one-screen behavior, or a decision memo with no material cross-team dependency. Output only:

- `背景和目标`
- `范围`
- `不做什么`
- `规则和文案`
- `验收标准`
- `待确认`

Use `标准模式` for ordinary features touching two to three surfaces such as H5 plus backend, admin plus API, or an operational workflow with a few dependencies. Output:

- `一页摘要`
- `需求范围`
- `产品规则`
- `验收标准`
- `风险和待确认`

Use `复杂模式` for money, settlement, permissions, production writes, cross-repository work, partner integration, launch campaigns, compliance, or multiple stakeholder teams. Use the full `references/prd-template.md`.

If complexity is unclear, choose the smallest structure that still preserves facts, non-goals, acceptance criteria, verification, and stop conditions.

## Resource Directory

When generating user-facing PRD resources outside a repo-local `to-spec` path, use an explicit output directory from the user's request. Otherwise, default to `<当前工作目录>/<slug>`.

`<slug>` is a short lowercase feature or project slug derived from the PRD title, such as `invite-reward` or `kyc-callback`. Create one directory per PRD or framework package and put all generated resources for that package there. Report the resolved directory after generation, but do not write the local path into the distributed PRD.

For Mode 1, write `framework-brief.md`, `open-questions.md`, and `cross-functional-review.md` into the resolved directory. After user approval, a later `to-spec` conversion may create the repo-local PRD instead.

For Mode 2, write `PRD.md` and any companion files such as `open-questions.md`, `acceptance-checklist.md`, or `cross-functional-brief.md` into the resolved directory unless the user explicitly asks to use the repo-local `to-spec` location.

Always make clear:

- confirmed facts
- assumptions
- `待确认` decisions
- non-goals
- acceptance criteria
- stop conditions

## Cross-Functional Rules

Every important requirement must be understandable from at least two views, but do not create a separate department-based summary or execution section:

- Business view: why it matters, who owns it, and how success is judged.
- Delivery view: what changes, what must not change, how acceptance is judged, and what blocks delivery.

Place material operational actions, brand/marketing implications, partner dependencies, support/FAQ needs, and development/test constraints next to the rule, scope item, acceptance criterion, risk, or pending decision they affect. Do not repeat them as standalone modules.

## References

- Use `references/prd-template.md` for the document structure.
- Use `references/quality-gate.md` for final review.
