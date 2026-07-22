# PRD Kit Quality Gate

Run this checklist before presenting the PRD.

## Fact Discipline

- No invented money, settlement, permission, account, launch, legal, production-write, or data semantics.
- Unresolved facts are marked `待确认`.
- Material unknowns are listed in `Open Questions` with owner, impact, and needed-by date when known.
- Assumptions are labeled as assumptions, not written as facts.

## Confirmed-Decision Closure

- Build an internal list of important confirmed decisions before drafting, with business-language wording, source, and PRD destination. Do not expose this list as a standalone PRD module.
- Classify every decision candidate as `已确认`, `待确认`, or `存在冲突`; use `待确认` only when no confirmed source exists, sources conflict, or the user explicitly leaves it unresolved.
- Complete a source-to-draft pass: every confirmed decision is present in the right PRD section and uses the confirmed business wording.
- Complete a pending-list repair pass: `当前待确认` and `待确认问题` contain no decision that an available source already confirms.
- Complete a draft-to-source pass: inspect every pending item in reverse; repair and reclassify it when a source resolves it, or surface the conflict when sources disagree.
- Repeat these passes after material revisions. Do not deliver a final PRD until important confirmed decisions have no pending or contradictory duplicate.
- Block delivery when a high-impact decision is both confirmed by an available source and listed as `待确认`, or when an unresolved source conflict is hidden.

## Business Language

- Write the distributed PRD in confirmed business language that operations, brand, marketing, partners, support, leadership, development, and QA can share.
- Translate implementation facts into their business meaning. Do not use database fields, enum values, API parameters, table names, code paths, internal component names, or technical stack names as the wording of a product rule.
- Reuse terminology from prior `grill-with-docs` output, the project glossary, ADRs, approved PRDs, or user-confirmed wording. Do not mock a new business term.
- When no canonical term exists or sources conflict, mark it `待确认` and resolve it with `grill-with-docs` before finalizing the rule.
- Do not create sections or descriptions named `技术栈`, `关联技术`, `技术方案`, or equivalent implementation-first wording for the distributed PRD. Describe the observable product capability, rule, boundary, and impact instead.
- Keep technical mappings out of the distributed PRD. Add a separate, minimal traceability note only when explicitly requested or required for an implementation handoff; it cannot be the only explanation of a product rule.
- Do not put external work-item carriers, branches, local implementation files, ticket formats, or repository workflow rules in `范围`, `不做什么`, product rules, or acceptance criteria. Keep them in internal delivery workflow unless the user explicitly asks for a handoff note and the detail changes a stakeholder decision.

## Publication State and External Work-Item Sync

- Before delivery, classify the PRD as `当前复核草案` or `同步外部父工作项`; do not infer synchronization from the existence of a work item.
- Default to `当前复核草案` unless the user explicitly requests synchronization, identifies the parent work item as canonical, or the active repo workflow requires it.
- Before updating a parent work item, read its current content and compare it with the PRD. Preserve valid decisions, links, and acceptance criteria; surface conflicts rather than overwrite them.
- Do not mark the document as synced until the external-work-item update actually succeeds. When the parent work item, carrier, access, or sync decision is missing, keep it as a review draft and report the blocker outside the PRD.

## Mode Discipline

- Mode 1 output is a framework brief until the user approves conversion into `to-spec`; do not pretend it is implementation-ready.
- Mode 1 records the grill-me decision trail: resolved decisions, recommended answers, unresolved branches, and what must be confirmed before development.
- Mode 2 uses grill-me only for high-impact missing decisions and does not re-interview for known facts.
- Mode 2 applies to-spec discipline before final PRD wording, including non-goals, source of truth, acceptance criteria, verification, and stop conditions.

## Cross-Functional Readability

- CEO / leadership can identify value, trade-offs, and decision needs within one minute from the summary and pending decisions.
- Operations, brand / marketing, partner teams, support, and development / QA can find their material action or constraint beside the affected requirement, rule, acceptance criterion, risk, or pending decision.
- Do not create standalone modules named `相关团队摘要`, `跨团队执行`, `研发交付`, or `验证方式`.

## Structure Fit

- Use Chinese section titles in generated documents.
- Use `轻量模式` for narrow changes; do not output the full complex PRD template.
- Use `标准模式` for ordinary cross-surface features.
- Use `复杂模式` for money, permissions, production writes, partner integration, compliance, cross-repo work, or launch campaigns.
- The chosen structure must still include facts, non-goals, acceptance criteria, and stop conditions when relevant. Put any needed verification detail inside its acceptance criterion rather than in a standalone module.

## Requirement Quality

- Replace vague words such as `快速`, `简单`, `易用`, `现代化`, `智能`, `稳定` with measurable or observable criteria.
- Each user story has acceptance criteria.
- Each important rule has a source, owner, or `待确认` marker.
- Non-goals explicitly protect scope from silent expansion.
- State, permission, empty, loading, error, retry, timeout, and rollback paths are covered when relevant.

## Delivery Quality

- Where verification detail is necessary, the related acceptance criterion includes the highest useful automated seam and required manual check.
- Cross-repo, API, Figma, data, and third-party dependencies are explicit.
- Stop conditions are actionable and narrow.
- The PRD can be split into implementation tickets without reinterpreting core business rules.
