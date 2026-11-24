# Modular RP Preset v0.32+ Beta 2 — FF5.4 Graphics, X Feed & Macro Audit

## Preservation

This update is append-only. The original v0.32 preset, original v0.32 Regex companion, and the 117 pre-existing beta prompt objects were not rewritten.

- Original base preset: 109 prompts
- Previous beta: 117 prompts
- Updated beta: 119 prompts
- Inherited prompt content fields changed: **0**
- Duplicate prompt identifiers: **0**
- Existing regex scripts: 40
- New beta regex scripts: 44

The new modules preserve FF5.4's operational behavior and output contract, but their long authoring text is reworded for this modular preset rather than copied verbatim.

## FF5.4 provenance

Extracted from the pinned FF5.4 preset object embedded in `ddkhan24/hordestudio/presets.js`, revision `653329e22f315ec87d928204f8155d4548d0d6c1`. The embedded FF5.4 export contains 63 prompts and 25 regex scripts. The upstream third-party notice records SHA-256 `1a42fbbfebdf23ce3bc243dc340b6d400bbb713ba882e8f81d921e162ccb893a`.

- Archive: https://rentry.org/freaky-frankenstein-presets
- Upstream JSON: https://www.mediafire.com/file/9f70q840092j5lr/Freaky_Frankenstein_5.4_Internal_States_%25282%2529.json/file
- Pinned mirror: https://github.com/ddkhan24/hordestudio/blob/653329e22f315ec87d928204f8155d4548d0d6c1/presets.js

## H11 — Pop-in Graphics (FF5.4)

- Source identifier: `019f62e8-892f-701a-afd5-49222c79fdb6`
- Enabled by default in both beta profiles, matching FF5.4's source state.
- Trigger: characters receive, notice, view, open, or read a concrete in-world readable medium.
- Produces raw inline HTML wrapped in `<!-- GFX_START -->` / `<!-- GFX_END -->`; Markdown fences are forbidden.
- Media treatments: terminal/interface, paper/letter/sign/map, phone/messaging screen.
- Phone screens include time, battery percentage, caller/conversation identity and chat bubbles, but the prompt avoids inventing metadata the scene does not support.
- Graphics are placed beside their prose beat and the prose does not repeat the visual's full content.
- Existing H2 is untouched. **Do not enable H2 and H11 together**: H2 is the previous POPIN marker implementation; H11 is the FF5.4 GFX marker implementation.

## H12 — Twitter X Feed (FF5.4)

- Source identifier: `019f62e8-892f-7028-bad6-be1f427c3ae4`
- Disabled by default in both beta profiles, matching FF5.4.
- Appends a five-post fictional live-audience feed after the finished story.
- Posts must react to specific current-scene details; no off-topic memes or impossible audience knowledge.
- Five persona archetypes are selected using five SillyTavern `{{random::...}}` macros over five **disjoint pools**, guaranteeing the five archetypes are distinct.
- Renders one X / Trending-style raw HTML card wrapped in GFX_START/END. Markdown code fences are forbidden.
- Flirtatious archetypes are restricted to non-graphic comments about clearly adult fictional characters and consensual adult tension.
- Existing H4 is untouched. **Do not enable H4 and H12 together**: H4 provides a compact in-world social feed; H12 provides an external live-audience reaction feed.

## Regex companion

The 40 original regex scripts were cloned without modification. Four rules were appended:

1. `FF5 GFX · Opening fence repair`: removes a Markdown opening fence before GFX/POPIN markers.
2. `FF5 GFX · Closing fence repair`: removes a trailing Markdown fence after GFX/POPIN end markers.
3. `FF5 GFX / POPIN · Prompt history stripper`: strips GFX_START/END or POPIN_START/END blocks, and internal_states wrappers, from prompt-only history from depth 0.
4. `FF5 X Feed · Prompt history fallback cleanup`: strips an older `<x_feed>...</x_feed>` semantic wrapper from prompt-only history.

Local sample tests:
- openingFenceRemoved: **PASS**
- closingFenceRemoved: **PASS**
- gfxPromptBlockRemoved: **PASS**
- popinPromptBlockRemoved: **PASS**
- xFeedFallbackRemoved: **PASS**
- plainStateDoesNotMatchStripper: **PASS**

The new beta Regex file has 44 rules. The original 40-rule file is unchanged.

## FF5.4 macro audit

The source scan below is performed over prompt content after removing author-comment payloads.

| FF5.4 macro head | Count |
|---|---:|
| `{{addvar}}` | 1 |
| `{{char}}` | 1 |
| `{{getvar}}` | 45 |
| `{{incvar}}` | 1 |
| `{{kimi-k3}}` | 1 |
| `{{maxcontext}}` | 1 |
| `{{maxresponse}}` | 1 |
| `{{roll}}` | 12 |
| `{{setvar}}` | 44 |
| `{{trim}}` | 53 |
| `{{user}}` | 40 |

### Main Prompt variable initialisers

The FF5.4 **Main Prompt** itself initializes 16 template/helper variables:

`bondsTemplate`, `invTemplate`, `chekhovTemplate`, `thoughtsTemplate`, `gmNotebookTemplate`, `dndTemplate`, `worldsimTemplate`, `bondCoT1`, `bondCoT2`, `agendaTrackerCoT`, `chekhovsGunCoT`, `gmNotebookCoT`, `dndSimCoT`, `dndSimCoTHQ1`, `DNDSimDCCoT`, `gmNotebookCoTGamestate`.

Across the **entire FF5.4 prompt set**, 27 distinct variable names are assigned with `setvar`, because later modules additionally initialise or update `worldsimCoT`, `bond_LS_US`, `bond_X_Y`, `sparks_X_Y`, `grudge_X_Y`, `chekhovActive`, `chekhovLocked`, `debug_mode`, `npcSeed`, `plotSeed`, and `rollD20`. This distinction matters: not all 27 are initialised in the Main Prompt.
### What was skipped, and why

- `setvar`, `getvar`, `addvar`, `incvar`, `roll`, `trim`, `user`, `char`, `maxContext`, and `maxResponse` are supported SillyTavern core macros. The last two also have the documented aliases `maxContextTokens` and `maxResponseTokens`.
- `{{roll:1d20}}` uses the legacy single-colon spelling; it is accepted by SillyTavern, but new authoring should use `{{roll::1d20}}`.
- `{{Kimi-K3}}` is not a standard core macro. It is a source-/backend-specific token marker, so copying it unchanged would not make the preset portable.
- `addvar` and `incvar` appear in FF5.4's optional Debug Engine for manual OOC state editing. They are not automatically needed by the ordinary turn loop.
- FF5.4 uses `getvar::name::fallback` in some positions. The inspected SillyTavern source registers `getvar` with exactly one argument, so the second segment is not a documented fallback parameter. Migration should use explicit fallback logic instead of assuming this syntax is valid.
- The earlier beta did not migrate FF5.4's variable framework because its F0 state block and F3 relationship output currently use a last-message state ledger and regex-facing numeric text rows. FF5.4's template state engine is a coupled dependency graph: 17 initialisers, module-level template setters, getvar consumers, CoT helpers, and optional Debug Engine commands. Copying only the Main Prompt initialisers would create blank/dead helpers. The earlier rationale was caution about incomplete dependency migration, not lack of SillyTavern macro support. Calling these core macros "non-portable" was incorrect; the complete variable framework simply had not been migrated.
- Current beta macro inventory remains native SillyTavern macros:

| Beta macro head | Count |
|---|---:|
| `{{char}}` | 3 |
| `{{charifnotgroup}}` | 1 |
| `{{lastmessageid}}` | 1 |
| `{{random}}` | 21 |
| `{{roll}}` | 7 |
| `{{trim}}` | 107 |
| `{{user}}` | 34 |

The new X Feed adds five native `random` calls. The current beta has seven `roll` calls written with the legacy single-colon separator; SillyTavern still accepts that legacy form, while double-colon is preferred for new authoring. Existing prompt text was not rewritten. No custom/backend macro was introduced.

## Activation and test checklist

- Use H11 for FF5.4-style readable media panels; leave H2 off.
- Use H12 for the five-comment live audience footer; leave H4 off.
- Expect additional output tokens from H12.
- In SillyTavern, test fenced GFX, fenced POPIN, ordinary F0 <GFX> state panels, X Feed output and an ordinary prose-only reply.
- Inspect Prompt Itemization and verify that the latest state block remains in context while older visual artifacts are removed at depth 0+.

## Validation

- FF5.4 source: 63 prompts / 25 regex scripts
- Base original: 109 prompts
- Previous beta: 117 prompts
- Updated beta: 119 prompts
- Inherited beta content changes: 0
- Duplicate prompt IDs: 0
- Beta regex rules: 44
- Regex smoke tests: 6/6 PASS

JSON parsing, identifier uniqueness, profile activation and local regex smoke tests passed. Actual import/rendering behavior must still be tested in the user's installed SillyTavern version.
