![Seraph Database](https://seraph.day/ui/LoginBonus_Stamp.webp)

> This repo is only meant for SeraphDB's localization file & the project's issue tracker

## Files

| file | what it is |
|---|---|
| `translation.json` | the site's UI strings, per locale |
| `skill_templates.json` | per-skill-type render templates |
| `mission_types.json` | per-mission-type description templates |
| `role_abilities.json` | the ROLE ABILITY state panels |
| `expedition_cards.json` | English for the Endless Expedition enchant cards |

## Editing `role_abilities.json`

The boxed panel the game shows beside a role ability — Demonic Rage, All-Out
Attack, Immersion, Void. Shape is `{locale: {RoleAbility.<label>: {...}}}`, and
the fields are `Name` (panel title), `Desc` (body) and `Sub` (the ※ caveats).

Three rules, in order of how much they matter.

**1. Delete `"_generated": true` when you edit an entry.** It marks the entry as
the pipeline's, and the pipeline REWRITES those on every build — so an edit
that leaves the marker in place will silently disappear on the next data
update. Removing it hands the entry to you permanently and nothing will touch
it again.

**2. Keep the `{keywords}` exactly as they are.** They are replaced with real
numbers when the file is published:

```
"- Independent Mind Eye effect: increases weakness damage dealt by {reinforcedModeSTezukaMindEyePercent}%"
                                                          published as -> 120%
```

Move them around the sentence freely, translate everything around them, but do
not replace one with the number it currently prints — that number is balance
data and changes when the game is rebalanced. This is not hypothetical: the
panels used to be hand-typed, and four of the five locales said Tezuka's Mind
Eye granted **12%** where the real figure is **120%**.

**3. `"_fallback": "<locale>"` means the entry is NOT in your language yet.** It
is showing another locale's text because the game has not shipped that panel in
yours. Those are the entries worth your time. Delete the marker along with
`_generated` when you replace the text.

Only touch your own locale's block. `ja_JP` is the original Japanese and is
best left generated.

### Current state

| locale | curated | still generated | showing another locale's text |
|---|---|---|---|
| `ja_JP` | – | 6 | – |
| `en_US` | 6 | – | – |
| `zh_CN` | – | 6 | 4 (from `zh_TW`) |
| `zh_TW` | – | 6 | – |
| `ko_KR` | – | 6 | – |

The generated entries are the game's own official text, so they are correct —
just wordier than the site's house style. `en_US` has been rewritten to that
style and is the reference for what a curated entry looks like.
