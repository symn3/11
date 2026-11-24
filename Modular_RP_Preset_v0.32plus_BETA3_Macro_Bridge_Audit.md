# MRP v0.32plus Beta — FF5.4 Macro Bridge Addendum

Date: 2026-11-24  
Repository: https://github.com/symn3/11  
Target preset: `Modular_RP_Preset_v0.32plus_BETA.json`

## Purpose

This update adapts the useful architecture behind Freaky Frankenstein 5.4's main-prompt variable system to the existing Modular RP (MRP) design. It does **not** transplant FF5.4's whole main prompt, its forced reasoning protocol, its turn-counter relationship logic, or its original state rules.

The design principle is: the shared bootstrap declares an empty set of local variables; each enabled MRP tracker registers only its own output template and, where useful, a short update helper; a late master prompt assembles the registered templates into one state panel; a separate scheduler invokes only helpers that are non-empty.

## FF5.4 design principle adapted

The pinned FF5.4 source inspected for this work is:

- https://github.com/ddkhan24/hordestudio/blob/653329e22f315ec87d928204f8155d4548d0d6c1/presets.js
- Source preset object: `freaky_frankenstein_5_4`
- Source release: FF5.4 Internal States
- Source has 63 prompt entries. Its main prompt initializes 16 template/helper variables. Enabled tracker modules then populate template variables, and the Internal States master reads those variables using `getvar`.

MRP keeps its own prompt IDs, tag grammar, roles, state fields, relationship semantics, random-roll rules, and profile logic. Only the useful set/get/assemble/update-helper pattern is adapted.

SillyTavern's documented variable macros are local-chat `setvar` and `getvar`; the current docs distinguish local variables from global variables and state that `setvar` emits no text while `getvar` inserts the stored value:
- https://docs.sillytavern.app/usage/core-concepts/macros/
- https://docs.sillytavern.app/usage/st-script/

## New prompt entries

### A0 — `a0-macro-bootstrap`

- Relative system prompt, order 90, enabled in both profiles.
- Initializes 24 `mrp32_*` local variables to empty strings on each request.
- This prevents a state template or helper from a previously enabled tracker being reused after the tracker is disabled.
- Variables are chat-local, not global.

### F0b — `f0-macro-master`

- In-chat system prompt, depth 0, order 320.
- Enabled in the Immersive profile only.
- Assembles the templates with `getvar` into the MRP state wrapper:
  `<GFX><details> ... </details></GFX>`.
- Uses the existing MRP state label and output conventions. It does not expose FF5.4's `<internal_states>` wrapper.
- The legacy F0 prompt is retained unchanged as a rollback/compatibility option, but is disabled in both profiles to avoid duplicate state panels.

### F16 — `f16-state-macro-scheduler`

- In-chat system prompt, depth 0, order 330, immediately after F0b and before the selected reasoning module.
- Enabled in the Immersive profile only.
- Reads the non-empty state-update helpers in a fixed sequence and asks the model to apply them silently.
- Does not require a visible checklist, forced monologue, `<think>` section, or generic turn counter.

## Variables

### Output-template variables (15)

| Variable | Owning module |
|---|---|
| `mrp32_npcAgendasTpl` | F1 NPC Agendas |
| `mrp32_npcLocationsTpl` | F1 NPC Locations |
| `mrp32_factionsTpl` | F2 Factions |
| `mrp32_bondsTpl` | F3 Relationships |
| `mrp32_questsTpl` | F4 Quests |
| `mrp32_inventoryTpl` | F5 Inventory / Skills |
| `mrp32_chekhovTpl` | F6 Chekhov's Gun |
| `mrp32_thoughtsTpl` | F7 NPC Thoughts |
| `mrp32_gmNotebookTpl` | F8 GM Notebook |
| `mrp32_dndTpl` | F9 DnD Task Sim |
| `mrp32_worldSimTpl` | F10 World Simulation |
| `mrp32_physicsTpl` | F11 Physics / World Notes |
| `mrp32_pendingEventsTpl` | F13 Pending Events |
| `mrp32_reputationTpl` | F14 Reputation |
| `mrp32_achievementsTpl` | F15 Achievements |

### Update-helper variables (9)

| Variable | Owning module | Purpose |
|---|---|---|
| `mrp32_agendaTrackerCoT` | F1 | Time-justified agenda/location updates |
| `mrp32_bondCoT1` | F3 | Grudge / negative relationship update |
| `mrp32_bondCoT2` | F3 | Sparks / positive relationship conversion |
| `mrp32_chekhovsGunCoT` | F6 | Seed age, lock, payoff and prune rules |
| `mrp32_gmNotebookCoT` | F8 | Notebook carry-forward, update and pruning |
| `mrp32_gmNotebookCoTGamestate` | F8 | Read previous notebook before updating |
| `mrp32_dndSimCoTHQ1` | F9 | Lock task DC before evaluating a roll |
| `mrp32_dndSimCoT` | F9 | Record the already-rolled task result |
| `mrp32_worldsimCoT` | F10 | Apply the existing world roll and event table |

All 24 variables are initialized, written by an owning module, and read by the master/scheduler. No `getvar::name::None` pseudo-fallback is used.

## Modules updated (append-only)

A macro bridge block was appended to each of:

- F1, F2, F3, F4, F5, F6, F7, F8, F9, F10, F11
- F13 Pending Events
- F14 Reputation
- F15 Achievements

The previous content of each prompt was retained as an exact prefix. The new blocks append `setvar` calls and short module-specific state/update contracts.

F13–F15 now direct their records into the single F0b state panel rather than creating separate top-level tracker panels. This avoids duplicate state containers.

## MRP semantics deliberately preserved

- **F1 agendas:** do not advance simply because a model reply happened. Progress requires plausible elapsed fictional time or an established process.
- **F3 relationships:** retain MRP's event-based BOND/SPARKS/GRUDGE rules. No FF-style fixed turn counter or automatic per-turn conversion was added.
- **F6 Chekhov:** no payoff before age 4 and no payoff without a natural scene opening. Seeds are not invented retroactively.
- **F9 DnD:** lock DC before using the pre-generated roll; skip trivial tasks; never reroll or alter the locked DC.
- **F10 World Sim:** use the existing roll and table; calm outcomes remain valid; off-screen events are shown only through a plausible trace or information path.
- **F8 Notebook:** does not duplicate facts owned by dedicated state trackers.

## Profile activation

| Profile | A0 | Legacy F0 | F0b | F16 |
|---|---:|---:|---:|---:|
| `100000` default | ON | OFF | OFF | OFF |
| `100001` Immersive | ON | OFF | ON | ON |

Existing F-module profile toggles were preserved. The Immersive profile's tracker activation state was not broadened automatically.

## Static validation

Validated after commit:

- Preset JSON parses successfully.
- 122 prompt entries; two prompt-order profiles.
- No duplicate prompt identifiers.
- Every prompt-order reference resolves to an existing prompt.
- 24 distinct `mrp32_*` variables are initialized.
- All 24 variables have an owning `setvar`.
- All 24 variables are retrieved by the master or scheduler.
- No getter refers to an uninitialized MRP32 variable.
- A0 is order 90; tracker modules are orders 210–315; F0b is order 320; F16 is order 330; reasoning modules begin at order 400.
- Regex companion remains at 44 scripts.
- Original v0.32 remains 109 prompts with SHA `4bf739491ab899d9ce0adde35049e1b4419703d6`.
- Original v0.32 regex remains 40 scripts with SHA `c8ac6fa246a46754864e2b4f719510930eb3c756`.

## Runtime caveat

This is a static JSON/macro wiring audit. The preset was not imported into a live SillyTavern UI during this change, so Prompt Itemization and an actual generation have not been runtime-verified here.

The master tells the model to omit the entire state wrapper if every template expands empty. That final all-empty omission is an instruction to the model, not a conditional preprocessor guarantee. In the shipped Immersive profile, several state templates are enabled, so the master has populated sections.

The regex companion was not modified because F0b retains MRP's existing outer `<GFX>` wrapper. Existing regex tests for that wrapper and the FF5 graphics blocks remain the applicable companion behavior.
