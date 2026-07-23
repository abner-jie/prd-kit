# PRD Kit

[中文](README.zh-CN.md)

Create business-readable PRDs for cross-functional teams. PRD Kit helps product, operations, marketing, partners, and engineering align on confirmed business rules, scope, acceptance criteria, risks, and open decisions.

## Modes

- **Mode 1 - Framework first:** use guided questions to settle a larger product framework before turning it into an implementation-ready PRD.
- **Mode 2 - Direct PRD:** turn available facts into a review-ready PRD and ask only for missing high-impact decisions.

## Use

Install the skill under your Codex skills directory, then invoke it explicitly with `$prd-kit`. PRD Kit does not run automatically for general PRD or planning requests. By default, generated resources are written to `<current-working-directory>/<project-slug>/`; specify an output directory in the request to override it.

PRD Kit creates a review draft by default. It synchronizes an external parent work item only when explicitly requested.
