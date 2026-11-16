# Coding-agent handoff: Arc/Dia feature reconstruction

Use this prompt with the accompanying `arc-dia-rebuild-guide.md` and `feature-catalog.json`. The pack was researched on **7 November 2026**. It is a specification, not an implemented browser.

## Prompt

Build a real desktop browser implementing the selected Arc and Dia feature contracts in this pack. Read the architecture, product model, build sequence, and feature evidence policy before editing code.

Treat the feature IDs as stable requirements. The catalog contains 116 entries, including historical and unresolved items. Product evidence is separate from the independently proposed implementation. Do not claim that a proposed algorithm, schema, UI default, or acceptance test was recovered from Arc or Dia. Do not claim exact parity until the relevant behavior has been observed and compared in a stated build.

Start by inspecting the existing repository and its instructions. Reuse its engine and patterns when they can satisfy the requirements. If no codebase exists, document an engine decision before scaffolding. A prototype may use Electron with real `WebContentsView` surfaces; full Chrome Web Store compatibility requires a different level of engine support and cannot be promised from Electron’s partial extension APIs. Do not implement the product as a website containing arbitrary-site iframes or as a UI mock with simulated pages.

Use these default scope choices unless the user provides different ones:

- Combined Arc organization and Dia contextual AI, macOS desktop first.
- Add Windows through explicit platform adapters and capability checks.
- Treat mobile as a separate product phase.
- Preserve historical Arc features as optional modules.
- Keep retired Dia Memory disabled in current-parity mode.
- Leave A39 TypeTravel and M03 pinch-to-summarize as discovery tasks until there is evidence.

Before implementing a vertical slice, list its feature IDs, required dependencies, chosen behavior for open questions, and acceptance criteria. Work through the guide’s phases; do not attempt a single monolithic implementation of all 116 entries.

The first slice should include C01/C02/C03/C05/C06/C09/C13 and A01/A02/A04/A05:

1. Launch an actual browser window and load real test pages.
2. Create two isolated storage groups and three visual workspaces, two sharing one storage group.
3. Create, select, navigate, reorder, close, and restore ordinary tabs.
4. Pin a tab with an independent home URL and custom title.
5. Navigate away from the home URL, unload the live page, and preserve the saved pin.
6. Relaunch and restore tab organization; load only necessary page surfaces.
7. Verify separate test logins and no unintended cookie/history leakage.

Keep these design rules throughout the implementation:

- Workspace organization, browser storage identity, and AI permission scope are separate concepts.
- A saved tab is not a permanently loaded renderer.
- Close, unload, archive, remove, unpin, and delete are explicit commands with separate semantics.
- UI controls, shortcuts, and AI tab actions use the same validated command service.
- Native/browser privileges are inaccessible to arbitrary web content.
- Context extraction preserves source identity, document version, timestamps, and completeness.
- Source IDs and tool schemas are validated outside the model.
- Connected services are scoped to a provider account and workspace; browser login alone is not universal AI permission.
- External effects use concrete, revision-checked plans and idempotency keys.
- Stop/resume must report the actual outcome of in-flight tool operations.
- User-authored titles and edits win over late AI suggestions.
- Sync uses a deliberate conflict/deletion/key-recovery design and never transfers live renderers.

Create a feature ledger with these fields:

```json
{
  "feature_id": "A05",
  "target_platform": "macOS",
  "target_reference_version": null,
  "status": "not-started",
  "evidence_checked": [],
  "decisions": [],
  "implementation_files": [],
  "tests": [],
  "remaining_gaps": []
}
```

Allowed statuses: `not-started`, `discovery`, `in-progress`, `implemented`, `verified`, `unsupported`, and `deferred`. Record a reason for unsupported/deferred status. `verified` requires passing the relevant behavioral checks, not merely a compiling UI.

Use synthetic fixtures for forms, two-account authentication, redirected pins, nested folders, shadow DOM, frames, PDF/image extraction, very large pages, multiple media sources, tab restoration, connector failures, and prompt injection. Use an injectable clock for archive/meeting behavior and a deterministic model stub for AI orchestration tests; add provider integration tests only where needed.

Use REA only for concrete unresolved questions. First record the app version and binary hash, then perform bounded read-only inventory. Do not assume the apps are Electron applications. Keep observed facts, inferences, and implementation choices in separate evidence fields. Do not modify the user’s installed browser, inspect unrelated personal data, or copy proprietary assets into the new app.

At each completed slice, report:

- Feature IDs and working user behavior.
- Implementation decisions that differ from or fill gaps in the reference.
- Tests run, results, and platform coverage.
- Remaining known limitations.
- The next dependency-complete slice.

Continue until the user’s selected scope is implemented and verified. Do not present a prototype as full browser parity, and do not hide unsupported extension APIs, hosted-service dependencies, or unverified historical behavior.

## Research pack contents

- `arc-dia-rebuild-guide.md`: full human-readable guide, feature index, schemas, state transitions, build phases, acceptance suite, and REA protocol.
- `feature-catalog.json`: the same 116 feature entries in a machine-readable form, with dependencies and source registry.
- `local-evidence.json`: read-only installed-app metadata; it contains no browser-profile data.
- `coding-agent-handoff.md`: this prompt.

All acceptance tests in this pack are proposed tests. No browser implementation was created or tested as part of the research task.
