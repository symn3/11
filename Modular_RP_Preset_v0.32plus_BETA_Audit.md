# Modular RP Preset v0.32+ Beta — Source Synthesis & Audit

Status: **Beta / additive only**  
Base: `Modular_RP_Preset_v0.32.json`  
Companion regex: `Modular_RP_Preset_v0.32_Regex.json` (unchanged)

## Non-negotiable preservation rule

This beta was forked from the current v0.32 JSON. Every pre-existing prompt object's `content` value was preserved byte-for-byte. No existing prompt text was rewritten, sanitized, shortened, translated, or otherwise altered. Only new prompt objects and their disabled entries in both existing `prompt_order` profiles were appended.

No existing regex script was changed. The new modules use native HTML `<details>` blocks and do not require regex transformations.

## Synthesis method

The source presets were compared by responsibility rather than by prompt name. Where multiple sources handled the same domain, the best coherent behavior was retained in the existing v0.32 module where already present. Source mechanisms that were complementary were represented as new, separately toggleable modules. Repeated state ownership and forced random events were avoided.

## New additive modules

| ID | Module | Source lineage | Why it is separate |
|---|---|---|---|
| C18 | Scene Pressure Cocktail | Pura 15.1 | Shapes tension, focus, social weather and pace without generating a second event |
| D20 | Random Genre Lens | Pura 15.1 | Adds a secondary tonal lens without replacing the established genre |
| D21 | Random Narrative Voice | Pura 15.1 / LFM v6.1 | Randomly selects a generic narrative voice; avoids author imitation and does not alter NPC dialogue |
| F13 | Pending Events Tracker | Pura 15.1 | Tracks promises, deadlines, appointments, threats and opportunities that are not ongoing quests |
| F14 | Reputation Tracker | Pura 15.1 | Tracks public perception, rumor provenance and conflicting reputations |
| F15 | Achievement Tracker | Pura 15.1 | Records earned milestones only; avoids duplicating F5 skills/titles |
| H9 | NPC Profile Sheets | Pura 15.1 + FF5.4 | Adds one-time concise profiles for recurring/plot-critical NPCs |
| H10 | Scene & Time Change Tracker | Pura 15.1 | Records meaningful scene cuts and time shifts without duplicating C7's recurring header |

## Source coverage already represented in the existing v0.32

| Source feature | Existing owner | Synthesis decision |
|---|---|---|
| Social friction / guarded NPCs | C3 + C16 | Preserve current modules; no duplicate Friction Mode |
| Geechan random scene interruption | C12 | Preserve current module |
| Grounded complication | C14 | Preserve current module |
| Scene-driving force | C15 | Preserve current module |
| Chaos Mode | C17 | Preserve current module |
| Ban phrases / anti-slop | D16 | Preserve current content exactly |
| Time continuity | C6 | Existing owner |
| Time/place header | C7 | Existing owner; H10 is event-marker only |
| NPC naming and identity | C10 | Existing owner; H9 only adds one-time profile display |
| NPC knowledge limits | C2 | Existing owner |
| Relationship tracking | F3 | Existing owner |
| Quests | F4 | Existing owner; F13 excludes ongoing quests |
| Inventory, skills and conditions | F5 | Existing owner; F15 excludes skill/title duplication |
| Chekhov seeds / secrets | F6 + C9 | Existing owners |
| NPC agendas and locations | F1 | Existing owner |
| Background world movement | F10 | Existing owner |
| Physics and durable world details | F11 | Existing owner |
| DND / skill checks | F9 + H8 | Existing owners |
| Internal States | F0-F12 | Existing owner system |
| X/social feed | H4 | Existing owner; FF's explicit/sexual audience archetypes were not imported |
| Image prompt comment | H3 | Existing owner; model/API-specific image-generation recipes were not imported |
| Randomized prose voice | New D21 | Added as a generic voice lens, not author imitation |

## Deliberately not imported

These were excluded from the additive beta because they are platform-specific, redundant, fragile, or likely to create poor narrative behavior:

- `{{Kimi-K3}}`, `{{maxContext}}`, and `{{maxResponse}}`: source-specific model/backend markers, not assumed to be portable SillyTavern macros.
- Force-first-two-sentences letter randomization: novelty mechanic with high risk of awkward prose and no meaningful RP-state benefit.
- FF's explicit X-feed archetypes and explicit auto-image-generation prompt recipe: platform/content-specific and not necessary for core RP.
- Pura's combined Director's Cut: duplicates several randomizer modules and encourages stacking incompatible scene engines.
- Pura's Parallel Off-Screen Tracker as an always-three-bullet output: existing F1/F10 already handle off-screen continuity; forcing three developments every scene can create invented events.
- Separate Pura item/status trackers: F5 already owns inventory, skills and conditions.
- Separate Pura secrets tracker: F6/C9 already own planted secrets and reveal pacing.
- Separate Pura relationship tracker: F3 already owns BOND/SPARKS/GRUDGE.
- Separate world-detail tracker: F11 already stores durable physics/environment facts.
- FF's `addvar` / `incvar` debug examples: advanced variable mutation is not required by the new modules and should not be copied without a tested state contract.

## Activation and conflict notes

All eight new modules are disabled in both prompt-order profiles by default.

- C18 is a scene-texture selector, not an event generator. Avoid combining it with C17.
- D20 keeps the established genre as canon; it is not a full genre swap.
- D21 is a generic narrative lens. Do not enable alongside a manually selected D17 voice.
- F13 excludes ongoing quests already tracked by F4.
- F14 distinguishes witnessed evidence from rumor.
- F15 awards at most one milestone per scene and does not duplicate F5 titles/skills.
- H9 is for recurring or plot-critical NPCs only; no profile for every extra.
- H10 marks meaningful transitions only. C6 remains the authority for elapsed time and C7 for a recurring time/place header.

## Validation performed

- Base prompt count: 109.
- Beta prompt count: 117.
- Existing prompt content fields changed: **0**.
- Duplicate prompt identifiers: **0**.
- Prompt-order profiles updated: **2**, new entries disabled in both.
- Existing regex scripts: **40**, unchanged.
- New regex dependencies: **none**.
