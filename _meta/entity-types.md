---
type: meta
purpose: entity-types
---

# Entity Types

## Entity Type Hierarchy

```text
person (abstract)
├── player
├── game_master
└── character (abstract)
    ├── pc
    └── npc

agent (abstract) — can act, decide, exert influence
├── character (see above)
├── creature
│   ├── beast
│   ├── undead
│   ├── construct
│   ├── spirit
│   ├── deity
│   └── aberration
├── faction
└── organization
    ├── government
    ├── corporation
    ├── cult
    ├── guild
    ├── military
    └── criminal

place (abstract)
└── location  (nests via part_of)

artifact (abstract)
├── item
│   ├── weapon
│   ├── armor
│   ├── vehicle
│   ├── treasure
│   ├── relic
│   ├── tool
│   └── consumable
├── document
│   ├── spell
│   ├── map
│   ├── letter
│   ├── prophecy
│   ├── contract
│   └── journal
└── prop

narrative (abstract)
├── event
│   ├── battle
│   ├── ritual
│   ├── disaster
│   ├── discovery
│   ├── betrayal_event
│   └── celebration
├── clue
├── plan
├── adventure-brief
└── campaign_overview

world (abstract)
├── heritage
├── world_domain
└── world_flags
```

Abstract types are never assigned to entities; they exist for
constraint inheritance in the relationship ontology.

## Frontmatter Schemas

### Fields by Type

`gma schema-rules show <type>` prints one type's required and optional fields, the
values its enumerated fields take, its template, folder and
relationship rules; `show` alone lists the types and the fields any
type takes. It reads the schema checks' own rules and the templates.

Write the recommended fields (`aliases`, `tags`, `source_document`,
`campaign`, `first_appearance`) anyway: `gma vault-check <vault> names` reads
`aliases`, and campaign-qa's audits lean on the rest.

`gm_aliases` (optional list) holds names only the GM should know, such
as a disguised NPC's true name. They resolve `[[links]]` like `aliases`,
but publish-site and mobrpg never show them: both rewrite a GM alias to
the owning page's title before publishing or pushing. Obsidian only
resolves links through `aliases`, so to make such a link work in
Obsidian, list the name under both fields. It still stays off the site.

`withheld` (optional boolean, absent means false) marks a note whose
own name is a secret: an NPC the players must not hear of yet. Its file
name, title and `aliases` are then looked for in everything the site
publishes, and an unlabelled `[[link]]` to it prints a neutral
placeholder in place of the name. `gm_aliases` rewrites a secret name;
`withheld` finds one. Write `true` or `false`; the build also reads
`yes`, `on` and `1` as true, as it does for `gm_only`. It is a note's
own flag and is never published. Wrap-up step 5c lifts it when the
GM confirms the note came out in play.

`companion` (optional boolean on an NPC or creature, absent means
false) marks the NPC who travels with the party: a GURPS Ally, a D&D
companion, follower or familiar, a Blades cohort. The site's Story
pages never picture a companion, as they never picture a PC.

### Relationships Block

```yaml
relationships:
  - target: "[[Target Entity Name]]"
    type: member_of       # From _meta/relationship-types.md
    tone: respectful      # one listed word; see Tones below
    strength: 7           # 1-10 (1-2 weak, 9-10 defining)
    bidirectional: false
    description: "Serves as lieutenant"
    gm_only: false        # optional; true hides the edge from a published
                          # site (page, Connections, search index)
```

Every relationship on a non-PC entity also appears in the body,
readable (a PC's body follows `shared/pc-body-structure.md`): under
`## Related` (grouped People, Places, Groups, Things, one line per
tie), or under `### Hidden Ties` in GM Notes when `gm_only: true`.
Write, change or remove both together.

Extraction defaults: `tone: neutral` and `strength: 5` when the
source is ambiguous; `bidirectional: false` unless inherently
symmetric; a `description` traceable to source text; `gm_only`
omitted unless the edge's *existence* is the secret.

**Tones.** `tone` is always one of: positive, friendly, warm, loving,
romantic, loyal, devoted, protective, trusting, respectful (positive);
negative, hostile, fearful, distrustful, contemptuous, tense, cold,
resentful, predatory, ominous (negative); neutral, unknown,
complicated, cautious, transactional, formal, professional (neutral).
The nuance goes in `description`. The list is
`shared/gm-apprentice-ontology.json`'s `tones`.

### Publish control fields

Optional, on any entity — how a frontmatter secret or a whole
GM-facing file stays off a player site (`<!-- gm-only -->` has no
meaning in frontmatter).

| Field | Type | Meaning |
|-------|------|---------|
| `publish` | `false` or `stub` | `false` — no page in any mode; links to it render as plain text. `stub` — page emitted for navigation, keeping only `publish_include_sections`. |
| `publish_exclude_fields` | array | Fields hidden on **this file only**, merged over the vault's `player_site.hide.fields`. Not re-admitted by `player_site.hide.field_exceptions`. |
| `publish_include_sections` | array | With `publish: stub` only. Headings to keep; default none. |

Absent, or an unrecognized `publish:` value, means normal
publication.

**PC `live_key`** (optional string, a slug; machine-written). The key the
site stores a PC's live stats under (current HP/SAN, loadouts, party board).
Absent means the slug of the filename, as always. `gma relink` writes it when
it renames a PC, so the stats stay with the character; nothing else sets it
and templates do not carry it.

## Type-Specific Fields

Mirrored into each vault's `_meta/entity-types.md`; migrations diff
the mirror against these entries.

**NPC:** `companion` (true: travels with the party (an Ally, follower,
familiar, cohort); never pictured on Story pages), `occupation`,
`age`, `gender`, `nationality`, `status` (alive/dead/missing/unknown),
`location` (wiki-link: where they can usually be found), `portrait`,
`voice` (set only when the GM gives this NPC their own story; how they
are told and speak; never published)

**PC:** `player_name`, `occupation`, `age`, `gender`, `nationality`,
`status` (alive/dead/missing/retired/unknown), `key_traits`,
`portrait`, `display_meta` (optional array: ordered field names for
the site meta row; when omitted, the setting
`player_site.sheets.header_facts` decides), `voice` (how this PC is
told and how they speak, a few sentences; the GM approves it; never
published), `sheet_source` (optional string: where the sheet is kept
when not in this file, e.g. `"D&D Beyond"` or `"paper, with the
player"`; not shown by default; see `shared/pc-body-structure.md`),
`hook` (optional string, any system: one line under the name and on
cards; blank means the backstory's first sentence), `dndbeyond`
(optional string, D&D only: a D&D Beyond character link or id; `gma
dnd-ddb` syncs the note from it), `gravity` (optional number, GURPS
only: local gravity in G, e.g. `1.2`; the sheet and party board work
encumbrance out by B350 and show the value, the sheet opens with the
DX penalty and jump and throw notice, and the to-hit calculator
applies the penalty; absent means 1G), `home_gravity` (optional
number, GURPS only: the gravity the PC was raised in, in G; sets the
DX penalty for gravity (B350); absent means 1G)

**Character Story:** `character` (wiki-link to the PC), plus universal
fields only. Body is append-only session sections; see the Story
Companion Convention in `shared/pc-body-structure.md`.

**Location:** `location_type` (city, district, building, room,
wilderness, ship), `parent_location` (wiki-link; groups the published
Locations listing, fallback `location_type`), `atmosphere` (a few
words, shown as a badge: "damp, candlelit, watchful"), `portrait`
(establishing shot)

**Faction/Organization:** `faction_type` (cult, guild, military, etc.;
groups the Factions listing), `goals` (a list), `resources`,
`leadership` (wiki-link), `territory` (wiki-link), `tier`,
`currentPlan`, `planProgress`, `alliances`, `recentActions`, `status`
(active/weakened/destroyed/allied/dormant), `part_of` (wiki-link to
the parent body, optional), `portrait` (logo, seal or headquarters)

**Item:** `item_type` (weapon, armor, vehicle, treasure, relic, tool,
consumable), `current_holder` (wiki-link: who has it now), `origin`
(wiki-link: where or who it came from), `portrait`

**Event:** `event_type` (battle, ritual, disaster, discovery,
betrayal, meeting, celebration), `in_game_date` (the in-game date, as
the story tells it ("Day 2", "May 1814")), `location` (wiki-link:
where it happened), `participants` (wiki-links), `outcome` (one line;
shown on the location's What Happened Here timeline)

**Clue:** `clue_type` (physical, testimonial, documentary), `found_at`
(wiki-link: where it is, or was found), `found_by` (wiki-link: who
found it, empty until found), `leads_to` (wiki-links to what it points
at), `reliability` (solid, partial, misleading), `discoveryState` (per
PC)

**Document:** `doc_type` (letter, journal, map, contract, prophecy,
spell, tome), `author` (wiki-link: who wrote it, or as the PCs
believe), `date` (when written), `condition` (pristine, water-stained,
torn, partly burned), `current_holder` (wiki-link: who has it now),
`portrait` (a scan or prop image, if you have one). The text goes in
the body under `## The Text`; an older `content` field moves there.

**Prop:** `prop_kind` (document, object, diagram, supplied,
container), `prop_file` (a hand-made page, PDF or picture beside the
note), `prop_address` (its address on the site; empty means
`props/<note name>`, or `props/<note name>-prop.html` when a page the
site builds has that address), `prop_style` (the look of the page the
site makes from `## The Text`; not with a `prop_file`), `prop_hand` (a
hand id from the vault's `_meta/prop-hands.json`, so one writer always
has one hand; `prop_font` on the note wins), `prop_line` (one line for
the props page), `prop_group` (its heading there; empty uses its
chapter), `prop_container` (wiki-link to the container prop it sits
in), `show_sealed` (containers: `titles` or `none`), `revealed_in`
(the session it reached the players; wrap-up's reveal step writes it,
first arrival only), `prop_state` (containers: a `.js` file filled
with what the page lists, for its script), `prop_state_global` (the
global it sets; default `PROP_ITEMS`). Style fields (`prop_title`,
`prop_breaks`, `prop_shift`, `prop_font`, and each style's own) are
listed in publish-site's prop-styles reference. It publishes when the
note does.

**Plan:** `plan_type` (arc/scene/investigation/timeline), `chapter`
(wiki-link), `participants` (wiki-links), `locations` (wiki-links),
`leads_to` (wiki-links)

**Adventure Brief:** `title`, `system` (the game system's id, or
undecided), `scope` (campaign/one-shot/few-shot), `sessions_estimated`
(a number or a range), `continuation_type`
(new/new-chapter/new-arc/time-jump/prequel/parallel/new-pcs)

**Campaign Overview:** `campaign`, `game_system`, `setting_year`,
`current_game_date`, `genre_tags`, `scope`
(campaign/few-shot/one-shot), `status`
(abandoned/completed/in_progress/not_started/paused),
`sessions_played`, `last_session`, `last_play_date`, `current_arc`,
`arcs_planned`, `current_chapter`, `chapters_planned`, `portrait`,
`voice` (the campaign's storytelling voice, a few sentences; the GM
approves it; never published)

**Creature:** `creature_type` (beast, undead, construct, spirit,
deity, aberration), `threat_level` (how dangerous the PCs believe it
is, shown on the site), `location` (wiki-link: where it lairs or is
found), `portrait`, `abilities` (optional, publishes), `weaknesses`
(optional, publishes). Keep `abilities` and `weaknesses` in the body's
GM Notes to hide them.

**Heritage:** `lifespan_range` (min/max age array), `maturity_age`,
`average_height`, `notable_traits`, `portrait`

**World Domain:** `domain`, `status` (stub/active/inactive),
`summary`, `rules` (array of world rules, a sentence each)

**World Flags:** `last_reviewed`

### PC Body Structure

The PC body-heading hierarchy, the `## Current Status` block spec,
and the Story Companion Convention now live in
`shared/pc-body-structure.md`.

### The `mobrpg:` node (machine-managed — do not hand-edit)

Entities synced to a mobRPG world carry a `mobrpg:` node written by
the `mobrpg` CLI — a regenerable sync ledger, not authored content;
top-line frontmatter stays the source of truth. Never edit it or
copy it into another entity. mobRPG is canon: `accepted`/`edited`
entities (`review_state`) are refreshed from mobRPG on pull-down;
`pending`/`dismissed` ones keep their vault content. Scalar values
are JSON-encoded (`key: "text"`, `key: null`).

| Key | Meaning |
|-----|---------|
| `world_id` / `external_ref` / `element_id` / `element_kind` | identity anchors (element_id is null until mobRPG accepts) |
| `review_state` | `pending` / `accepted` / `dismissed` / `edited` / `deleted` |
| `content_hash` / `last_synced` / `review_note` | sync bookkeeping |
| `determined` | classifiers derived and sent (mobRPG canon overwrites on edit) |
| `relationships[]` | reified-Event ids keyed by `(predicate, target)` |
| `languages[]` | reserved (populated by the mobRPG skill) |

## Default Folder Mapping

| Type Category | Vault Folder |
|---------------|-------------|
| pc | Characters/PCs/ |
| npc | Characters/NPCs/ |
| location | Locations/ |
| faction, organization | Factions & Organizations/ |
| item (all subtypes) | Items & Artifacts/ |
| creature (all subtypes) | Creatures/ |
| event (all subtypes) | Events/ |
| document (all subtypes) | Documents/ |
| prop | beside its prop file, e.g. Chapters/{chapter}/Props/ or Documents/ |
| clue | Clues/ |
| plan | `Chapters/{chapter}/Planning/` |
| scene | `Chapters/{chapter}/Scenes/` |
| adventure-brief | Adventures/{adventure-name}/ |
| campaign_overview | _Campaign/ |
| heritage | Heritages/ |
| world_domain | _World/ |
| world_flags | _World/ |
