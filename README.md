![Seraph Database](https://cdn.hbr.quest/webp/jp/ui/LoginBonus_Stamp.webp)

> This repo holds SeraphDB's localization files and the project's issue tracker, and nothing else.

## Files

| file | what it is |
|---|---|
| `translation.json` | the site's UI strings, per locale |
| `skill_templates.json` | the description template for each skill type, per locale |
| `mission_types.json` | the description template for each mission type, per locale |
| `role_abilities.json` | the ROLE ABILITY state panels, per locale |
| `expedition_cards.json` | English for the Endless Expedition enchant cards, beside a Japanese mirror of each |

## Editing `role_abilities.json`

The boxed panel the game shows beside a role ability: Demonic Rage, All-Out
Attack, Immersion, Void. Shape is `{locale: {RoleAbility.<label>: {...}}}`, and
the text fields are `Name` (panel title), `Desc` (body) and `Sub` (the ※
caveats). `Icon` names the panel's icon and is not text, so leave it as it is.

Three rules, in order of how much they matter.

**1. Delete `"_generated": true` when you edit an entry.** It marks the entry as
the pipeline's, and the pipeline REWRITES those on every build, so an edit
that leaves the marker in place will silently disappear on the next build.
Removing it hands the entry to you permanently and nothing will touch it again.

**2. Keep the `{keywords}` exactly as they are.** They are replaced with real
numbers (or element names) when the file is published:

```
"- Independent Mind Eye effect: increases weakness damage dealt by {reinforcedModeSTezukaMindEyePercent}%"
                                                          published as -> 120%
```

Move them around the sentence freely, translate everything around them, but do
not replace one with the number it currently prints: that number is balance
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

As of 2026-11-05. An entry is curated when it has no `_generated` marker, and
is not in its locale's own words yet when it carries `_fallback`.

| locale | curated | still generated | of those, showing another locale's text |
|---|---|---|---|
| `ja_JP` | 0 | 6 | 0 |
| `en_US` | 6 | 0 | 0 |
| `zh_CN` | 0 | 6 | 2 (from `zh_TW`: Immersion and Void) |
| `zh_TW` | 0 | 6 | 0 |
| `ko_KR` | 0 | 6 | 0 |

The generated entries are the game's own official text, so they are correct,
just wordier than the site's house style. `en_US` has been rewritten to that
style and is the reference for what a curated entry looks like.

## Editing `expedition_cards.json`

One line of English per card, in the `en_US` block, keyed
`endlessExpedition.enchantCard.<n>`. The `ja_JP` block beside it is a mirror of
each card's Japanese text that the build keeps current, so leave it alone. When
a commit changes a card's `ja_JP` line, the game reworded that card: check the
`en_US` line under the same key. A card the file does not have yet arrives with
an empty `en_US` entry, which is yours to fill in. The build never touches
`en_US` text.
