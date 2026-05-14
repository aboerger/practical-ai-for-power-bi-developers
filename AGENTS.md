# AGENTS.md

## Purpose

This repository is for demos and practical guidance on using generative AI and agents in Power BI and Microsoft Fabric workflows. Changes should improve how Power BI developers build, review, test, validate, and maintain semantic models, reports, and related assets in Git-enabled projects.

Prefer solutions that are:

- Easy to demonstrate live
- Easy for Power BI developers to understand and adopt
- Safe for source-controlled PBIP projects
- Minimal, targeted, and reversible

## Repository Shape

Most work happens in these areas:

- `analysis/`: One or more Power BI projects. Each project may include a `.pbip` file plus paired `.Report/` and `.SemanticModel/` folders.
- `analysis/<Project>/<Project>.Report/`: PBIR report definition, pages, visuals, bookmarks, themes, and custom visual metadata.
- `analysis/<Project>/<Project>.SemanticModel/`: Semantic model definition files, TMDL, DAX queries, and model-level assets.
- `resources/`: Reusable helper assets, including TMDL or script-based resources used across demos.
- `.github/agents/` and `.github/skills/`: Existing agent and skill customizations for repo-specific workflows.

Before editing, identify the owning surface and stay there:

- Report layout, themes, visuals, bookmarks, PBIR JSON: work in `.Report/`
- Measures, columns, relationships, model metadata, DAX tests, TMDL: work in `.SemanticModel/`
- Shared reusable assets or templates: work in `resources/`

## Working Style

- Treat this repo as a teaching repo, not just a delivery repo. Prefer changes that are clear and explainable.
- Preserve existing folder structure and file naming. Do not reorganize PBIP assets unless the task explicitly requires it.
- Do not overwrite or revert unrelated user changes.
- When a request spans report and model layers, make the dependency explicit and update both sides only when necessary.

## Power BI And Fabric Guidance

- Assume projects under `analysis/` may be opened as PBIP projects and should remain valid after edits.
- For semantic model work, prefer direct, deliberate edits to TMDL and related DAX artifacts over opaque bulk rewrites.
- For report work, preserve PBIR structure, page identity, visual identity, bookmarks, and custom visual references unless the user asks for structural changes.
- For Fabric or service-oriented tasks, be explicit about workspace, item, and environment assumptions. Do not guess publish targets.
- For Git-enabled workflow demos, favor steps that produce clean, reviewable diffs.

## Testing And Validation Expectations

- Validate the smallest relevant slice after making changes.
- For PBIR/report edits, prefer `pbir validate` or another report-scoped validation when available.
- For semantic model edits, use the narrowest available validation for TMDL, DAX, or model metadata.
- If working with DAX Query View tests or PQL.Assert, keep test assets inside the relevant `.SemanticModel/` project.
- Do not create model test files at the repo root.
- Treat BPA findings as guidance, not absolute truth. Confirm whether a flagged pattern is intentional before changing it.

## Repo-Specific Conventions

- A project may contain DAX test assets under `.SemanticModel/DAXQueries/`; keep those files colocated with the owning semantic model.
- Reusable assertion or helper functions may live in shared TMDL assets under `resources/` and in model definition files.
- Existing custom agents and skills in `.github/` should be reused when they clearly match the task, especially for Power Query, DAX testing, PBIP/PBIR work, Deneb, BPA, and semantic model review tasks.
- When working on Deneb or other custom visuals, preserve field bindings and report wiring unless the user explicitly requests a redesign.

## Preferred Agent Behavior

- Start from the nearest concrete artifact: a `.pbip`, `.Report/` file, `.SemanticModel/` file, TMDL table, DAX query, or visual definition.
- Make the smallest change that proves the intended behavior.
- Validate immediately after the first substantive edit.
- Surface assumptions clearly when environment-specific behavior matters, especially for DEV, TEST, and PROD workflows.
- When multiple implementations are possible, choose the one that best improves the workflow of Power BI developers.

## Avoid

- Broad repo-wide rewrites without a user request
- Moving files between projects casually
- Introducing undocumented conventions that differ from PBIP, PBIR, or TMDL norms
- Treating demos as throwaway work; example code here should still be credible and reviewable