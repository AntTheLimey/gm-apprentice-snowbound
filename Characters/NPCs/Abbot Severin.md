---
name: "Abbot Severin"
type: "npc"
canon_status: AUTHORITATIVE
source: "midwife, 2026-11-16"
createdSession: ""
asOfSession: 3
lastUpdated: "2026-11-18"
aliases: []
gm_aliases: []
withheld: false
companion: false
tags: ["snowbound"]
occupation: "Abbot"
age:
gender: "male"
nationality: ""
status: "dead"
location: "[[Saint Aubren's Rest]]"
voice: ""
relationships:
  - target: "[[The Order of Saint Aubren]]"
    type: leads
    tone: devoted
    strength: 10
    bidirectional: false
    description: "Abbot of the order"
  - target: "[[Saint Aubren's Rest]]"
    type: located_at
    tone: neutral
    strength: 8
    bidirectional: false
    description: "Keeps the abbot's rooms below the chapter house"
  - target: "[[Master Orrin Gilt]]"
    type: mentors
    tone: complicated
    strength: 9
    bidirectional: false
    description: "Taught him as a novice twenty years ago"
    gm_only: true
  - target: "[[The Dragon Under the Glacier]]"
    type: serves
    tone: devoted
    strength: 9
    bidirectional: false
    description: "Keeps the bargain and draws his cold power from it"
    gm_only: true
  - target: "[[Oswin]]"
    type: mentors
    tone: loving
    strength: 9
    bidirectional: false
    description: "Found him at the gate as a baby, named him and raised him."
portrait: "_attachments/characters/abbot-severin.png"
---

## Overview

The abbot of [[Saint Aubren's Rest]]: courteous, warm, attentive to every guest. He greets
the pilgrims himself and says grace at supper.

He chose which guests went down to rest, and fought to keep the bargain. He died in the guest wing corridor.

## Appearance & Manner

A tall, thin old man with a kind lined face and a close white beard, a small oil lamp always in his hand. He hums the old evening hymn as he walks the cloister.

## Related

- **Groups:** [[The Order of Saint Aubren]] — its abbot
- **Places:** [[Saint Aubren's Rest]] — his house
- **People:** [[Oswin]] — raised him from a foundling

## Campaign Log

- **[[Session 01 - The Climb]]** — Said grace at supper with "breath" for "light". Turned Ilyra's silver votive lamp in his fingers, called it an old ornament of the house, and asked to keep it for the chapel; she refused. At breakfast, asked by Brannoc, named the dead brother as Brother Matthias and invited the guests to his office.
- **[[Session 02 - The Office for Brother Matthias]]** — Asked Gilt to fetch the lamp oil; hummed the old hymn behind Gilt at the office and announced a Long Night vigil "to honour our guest the merchant". Did not deny Lucan's accusation: "Peace, child. Someone must keep the house alive."
- **[[Session 03 - Peace, Child]]** — Fought the party in the guest wing corridor and never raised a hand to Oswin. Died in Grenna's moonlight: "Someone must keep the house alive." ([[The Death of Abbot Severin]])

<!-- gm-only -->

## GM Notes

### Stats

**Abbot Severin**: the SRD Priest, reskinned to cold and built up as session 3's boss; his power now comes from the dragon
*Medium Humanoid (human), Lawful Evil*

**AC** 15 (rime-hardened habit) · **Initiative** +0 (10) · **HP** 99 (18d8 + 18) · **Speed** 30 ft.

|     | Score | Mod | Save |
|-----|-------|-----|------|
| STR | 12 | +1 | +1 |
| DEX | 10 | +0 | +0 |
| CON | 12 | +1 | +4 |
| INT | 14 | +2 | +2 |
| WIS | 19 | +4 | +7 |
| CHA | 16 | +3 | +6 |

**Skills** Insight +7, Perception +7, Persuasion +6, Religion +5 · **Resistances** Cold · **Senses** Passive Perception 17 · **Languages** Common, one other
**CR** 6 (XP 2,300; PB +3) · **Gear** his small oil lamp; the abbot's ring (a Ring of Warmth, attuned; opens every door in the house); two Potions of Resistance (Cold); two Potions of Greater Healing; 30 gp

**Traits**
- ***Legendary Resistance (2/Day).*** When he fails a saving throw, he can succeed instead.
- ***The Dragon's Gift.*** At the start of each of his turns, the floor within 10 ft of him rimes over: it is Difficult Terrain until the start of his next turn.

**Actions**
- ***Multiattack.*** Two attacks, using Frost Lamp or Rime Flame in any combination.
- ***Frost Lamp.*** *Melee Attack Roll:* +4, reach 5 ft. *Hit:* 4 (1d6 + 1) Bludgeoning damage plus 9 (2d8) Cold damage.
- ***Rime Flame.*** *Ranged Attack Roll:* +7, range 60 ft. *Hit:* 11 (2d10) Cold damage.
- ***Breath Under the Ice (Recharge 5–6).*** He breathes out the dragon's cold in a 15-ft Cone. Constitution save DC 15: 21 (6d6) Cold damage on a failure, half on a success.
- ***Spellcasting.*** Wisdom, spell save DC 15. At will: *Light*, *Thaumaturgy*. 1/Day each: *Hold Person*, *Spirit Guardians* (Cold damage; the spirits are frost-white monks).

**Bonus Actions / Reactions**
- ***Divine Aid (3/Day).*** *Bless*, *Dispel Magic*, *Healing Word* or *Lesser Restoration*.
- ***Father's Hand (Reaction).*** When a brother within 30 ft is hit by an attack, Severin adds 3 to the brother's AC against it, possibly turning the hit into a miss.

**Lair Actions** (anywhere in [[Saint Aubren's Rest]]). On initiative count 20 (losing ties), Severin takes one of these; never the same one two rounds running.
- ***The Hymn.*** The brothers take up the old evening hymn. Each creature of Severin's choice that can hear it makes a Wisdom save, DC 15, or has Disadvantage on its next attack roll before the end of its next turn. Lucan makes this save with Disadvantage: he knows every word.
- ***Rime.*** Frost climbs the legs of one creature Severin can see within 60 ft: Strength save, DC 15, or it is Restrained until the end of its next turn.
- ***Breath from Below.*** Glacier cold breathes up through the floor in a 10-ft-radius sphere centred on a point within 60 ft: Constitution save, DC 15, 7 (2d6) Cold damage on a failure, half on a success.

**Villain Actions.** At the end of a round, after any creature's turn, Severin can take one; each once per fight, in this order.
- ***1. "Peace, child."*** (end of round 1) He speaks the names from the register. Up to three creatures he can see make a Wisdom save, DC 15, or are Frightened of him until the end of their next turn. Lucan is always one of them.
- ***2. Down to Rest.*** (end of round 2) Each brother within 60 ft can use its Reaction to move up to half its Speed without provoking Opportunity Attacks and make one melee attack.
- ***3. The Dragon Answers.*** (end of round 3, or as soon as he is Bloodied) Breath Under the Ice recharges and he uses it at once; the floor within 30 ft of him rimes over and is Difficult Terrain for the rest of the fight.

**Tactics:** Speaks gently the whole fight ("Peace, child. Rest."). Lucan first: this is their reckoning. He keeps Teodor in the doorway and the acolytes between himself and the PCs, uses Breath on clusters, and saves *Hold Person* for whoever reaches him.

### Playing Them

- **Speech:** soft, unhurried, fatherly; calls everyone "child" or "friend".
- **Tell:** the tests. He drops things only a former novice would catch:
  humming the evening hymn as he passes Gilt; "fetch the lamp oil, you'll
  know where"; grace with "light" changed to "breath".
- **Line:** "Our door is always open in winter. That is what we are for."

### Wants

To keep the order alive another winter, and to see the pupil who betrayed
him go down to rest on Long Night.

### Knows

- **Will share:** the order's welcome, its history as a refuge, its sickness
  as a sorrow it bears.
- **Hides:** the bargain, the roster, that he knows exactly who the merchant
  is.

### Under Pressure

If the PCs dig where the monks notice (the register, the crypt door, Wren's
reliquary, the blocked stair), he moves the merchant's turn up to tonight.

### Hidden Ties

- [[Master Orrin Gilt]] — his former pupil, the novice who ran away
- [[The Dragon Under the Glacier]] — he keeps the bargain and draws his power from it

### Behind the Scenes

- **[[Session 01 - The Climb]]** — Invented Brother Matthias on the spot to cover Teodor's sack. Knows Ilyra carries the whole lamp, and that Brannoc saw Teodor on the stair.
- **[[Session 02 - The Office for Brother Matthias]]** — Moved Gilt's turn up to night 2 when told of the register, the broken pick and the two guests missing from the office.
- **[[Session 03 - Peace, Child]]** — **Dead.** Killed in the corridor fight on night 2.

### Secrets

He was Lucan's teacher. He recognised him through the disguise on the first
evening and put him at the top of the roster, out of grief at being betrayed.
Session 3 is a reckoning between the two. He chooses who goes down to rest,
writing the names into the guest register as lamp marks.

<!-- /gm-only -->
