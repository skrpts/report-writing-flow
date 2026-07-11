# Release Notes

## v1.1.25
GH#776 — fix advertised inputs reaching nothing (K-034). The four advertised inputs (`research_topic`, `research_questions`, `methodology`, `completed_draft_or_near`) were declared and bound nowhere, so every step ran on empty context. Adds a local `report-intake` skill + `report-brief` prompt that declares and collects the four inputs into a structured brief, which flows into the interpretation step via `{{steps.previous.output}}`; binds the previously-unbound `polish-language.source` to the interpretation via `from_step`. No shared-prompt edits. en-US copy. Also repins the `polish-language` dep v1.0.1 → v1.0.5 (same lineage `9b1771e0`), the version whose body declares `context_params.source` / references `{{step.context.source}}` — required for the new `source` binding to resolve (the stale v1.0.1 pin blocked the canonical publish scan).

## v1.1.24
GH#745 — declare per-step `output: {name, type}` on every execution step (interpretation/text, evidence_report/text, polished_report/text). Lights up the #744 rich flow-map. Content-only; no bindings or logic changes.

## v1.1.23
GH#645 Row 3b — migrate to K-037 dep-referenced schema. Strip 9 inline shared-content files and declare 9 hub-shared deps (UUID id + slug name + version + checksum from `gen-dep-checksums.mjs`). Closes pre-Step-3 inline-vendoring for this bundle.

## v1.1.22
Wave 2: re-signed with canonical engine signing pipeline.

## v1.1.21
Tags migrated inline into manifest (GH#586). tags.yaml retired.

## v1.1.20
Bundle re-signed with canonical engine signing pipeline (Wave 2 migration).

## v1.1.19
Signature fix — RELEASE_NOTES.md now included in integrity checksum.

## v1.1.18
Initial catalog release with full structural and content-quality validation. All scanner checks pass.
