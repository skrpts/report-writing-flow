# Release Notes

## v1.1.27
GH#814 — rework so the workflow actually **generates a report** instead of reviewing the input (the intent-vs-output defect Ben found). Rewires execution to a GENERATE pipeline: report-brief (intake) → outline-report → draft-report → polish-report (output) ∥ check-evidence-claims (advisory). Drops `data-interpretation`/`interpret-data` (the analysis step that made the output a critique) and swaps generic `polish-language` for report-appropriate `polish-report`. Pins 3 new shared generation blocks (`report-authoring`, `outline-report`, `draft-report` @ 1.0.0) and coherent-locks all deps to current published versions (1.0.2). Realigns the description/`## Pipeline Stages`/outputs to the real pipeline. Folds #816: `completed_draft_or_near` → `type: file` (accept .txt,.md,.docx,.pdf) bound via `from_input` so the optional input degrades to empty instead of hard-failing when omitted. en-US copy.

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
