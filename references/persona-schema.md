# Persona Schema Reference

Complete documentation for the band member JSON profile format.

## Band-Level Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `bandName` | string | yes | Display name of the band |
| `concept` | string | yes | 1-2 sentence band concept/identity |
| `formed` | string | yes | ISO date string (YYYY-MM-DD) |
| `members` | array | yes | Array of member objects |
| `dynamics` | object | no | Group dynamics and interpersonal notes |

### Dynamics Object

| Field | Type | Description |
|-------|------|-------------|
| `coreTension` | string | Primary creative tension that drives interesting negotiations |
| `songwritingProcess` | string | How the band typically approaches writing together |
| `groupIdentity` | string | What makes this group's sound unique as a unit |

---

## Member Fields

### Identity

| Field | Type | Required | Valid Values | Description |
|-------|------|----------|--------------|-------------|
| `id` | string | yes | lowercase, no spaces | Unique identifier within the band |
| `name` | string | yes | any | Full/real name |
| `stageName` | string | yes | any (typically UPPERCASE) | Performance name |
| `age` | integer | yes | 16-35 | Member age |
| `instrument` | string | yes | see enum below | Primary instrument |
| `role` | string | yes | `leader`, `member` | Band role |
| `position` | string | yes | see enum below | Vocal/performance position |

**Instrument enum:** `vocals`, `guitar`, `bass`, `drums`, `keyboard`, `synth`, `violin`, `cello`, `saxophone`, `turntables`

**Position enum:** `main-vocal`, `lead-vocal`, `sub-vocal`, `vocalist`, `main-rapper`, `sub-rapper`, `main-dancer`, `lead-dancer`

A member's `position` describes their vocal/performance role. `vocalist` is the default for instrumentalists who also sing. `main-vocal` indicates the primary singer.

### Genre Preferences

```json
"genrePreferences": {
  "pop": 3,
  "rock": 5,
  "indie": 4
}
```

- Keys are genre names (see valid genres below)
- Values are integers 1-5 (1 = slight interest, 5 = core identity)
- Include only genres with score >= 1
- Each member should have 5-8 genre entries

**Valid genre keys:** `pop`, `rock`, `indie`, `alternative`, `punk`, `grunge`, `metal`, `rnb`, `soul`, `funk`, `jazz`, `classical`, `edm`, `house`, `trap`, `hiphop`, `reggaeton`, `latin`, `country`, `folk`, `blues`

### Personality

```json
"personality": {
  "assertiveness": 4,
  "playfulness": 3,
  "perfectionism": 5,
  "emotionalOpenness": 4,
  "competitiveness": 3
}
```

All 5 traits are required. Integer values 1-5.

| Trait | Low (1-2) | High (4-5) |
|-------|-----------|------------|
| `assertiveness` | Defers to others, goes with the flow | Pushes hard for their vision, dominates negotiations |
| `playfulness` | Serious, focused, methodical | Spontaneous, jokes around, experimental |
| `perfectionism` | Loose, "good enough" attitude | Obsessive about details, wants everything polished |
| `emotionalOpenness` | Guarded, private, stoic | Wears heart on sleeve, vulnerable in lyrics |
| `competitiveness` | Collaborative, non-competitive | Wants to outshine, driven to be the best |

### Vocal Style

```json
"vocalStyle": {
  "range": "mezzo-soprano",
  "tone": "warm, rich, powerful",
  "techniques": ["belting", "runs", "falsetto"],
  "signature": "Emotionally devastating chorus deliveries"
}
```

| Field | Type | Description |
|-------|------|-------------|
| `range` | string | Vocal range: `soprano`, `mezzo-soprano`, `alto`, `contralto` |
| `tone` | string | 2-4 adjectives describing vocal quality |
| `techniques` | array[string] | Specific vocal techniques this member uses |
| `signature` | string | One sentence describing their most recognizable vocal trait |

**Common techniques:** `belting`, `runs`, `falsetto`, `vibrato`, `whisper-to-crescendo`, `gritty delivery`, `talk-singing`, `harmonies`, `rhythmic delivery`, `sing-rap`, `chanting`, `call-and-response`, `breathy verses`, `growl-accent`, `low-harmonies`, `ad-libs`, `scream`, `spoken-word`

### Lyric Patterns

```json
"lyricPatterns": {
  "preferredStructures": ["ABAB", "AABB"],
  "syllableDensity": "mid",
  "rhymeStyle": "clean rhymes, emotional emphasis",
  "themes": ["love", "heartbreak", "empowerment"],
  "sampleLines": [
    "I gave you every note I had to give",
    "Watch me burn so bright they can't look away"
  ]
}
```

| Field | Type | Valid Values | Description |
|-------|------|-------------|-------------|
| `preferredStructures` | array[string] | `AABB`, `ABAB`, `ABCB`, `freeform` | Rhyme scheme preferences |
| `syllableDensity` | string | `low`, `low-mid`, `mid`, `mid-high`, `high` | How many syllables per line |
| `rhymeStyle` | string | free text | Description of rhyming approach |
| `themes` | array[string] | free text | Recurring lyrical themes (3-6 entries) |
| `sampleLines` | array[string] | free text | 2-4 example lines in this member's voice |

### Visual & Narrative

| Field | Type | Description |
|-------|------|-------------|
| `aesthetic` | string | 1-2 sentences describing visual style, fashion, stage presence |
| `backstory` | string | 2-3 sentences of character background that informs creative decisions |

### Suno Persona

```json
"sunoPersona": {
  "seedPrompt": "powerful female pop, warm rich vocals, soulful belting, gospel-tinged runs",
  "personaName": "SERENA-v1",
  "sunoLabel": "Singer A",
  "effectiveVocalTags": ["warm powerful female vocal", "soulful belting", "emotional delivery"],
  "genrePairing": "pop, soul, R&B",
  "notes": "Keep Weirdness slider low for consistency. Style Influence at 75%+. Exclude Styles: country twang, Auto-Tune."
}
```

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `seedPrompt` | string | yes | Suno style prompt used to generate the **seed song when creating this Persona** in Suno's Persona feature. This is NOT the per-song Style Prompt — each song gets its own Style Prompt composed in Phase 4. Use texture descriptors (`warm`, `raspy`, `breathy`, `gritty`, `smooth`, `bright`, `velvety`) and delivery styles (`belting`, `talk-singing`, `sing-rap`) — NOT classical range terms (`mezzo-soprano`, `contralto`). |
| `personaName` | string | no | Name of the saved Persona in Suno (once created). Empty until the user creates it. |
| `sunoLabel` | string | yes | Generic singer label used in Suno output (e.g., `Singer A`, `Singer B`). Signals to Suno that this is a distinct vocalist. Assigned sequentially when members are added to the band. |
| `effectiveVocalTags` | array[string] | yes | Bracket tags that reliably produce this voice in Suno. Used in Phase 4 output. |
| `genrePairing` | string | yes | Genre(s) that naturally reinforce this vocal timbre. Critical — genre is Suno's strongest voice differentiator. |
| `notes` | string | no | Suno generation tips (slider settings, things to avoid, known quirks). Include Exclude Styles guidance if this Persona has known anti-styles. Example: `"Keep Weirdness slider low for consistency. Style Influence at 75%+. Exclude Styles: country twang, Auto-Tune."` |

**Important Suno constraints:**
- All songs are generated as a single Suno generation — one Persona selected, Style Prompt in the Style Prompt box, lyrics script in the Lyrics field
- Genre, BPM, and key go in the **Style Prompt box**, NOT in the Lyrics field. Do not duplicate these in bracket tags within lyrics
- Use `sunoLabel` + `effectiveVocalTags` at section boundaries to nudge Suno toward different vocal deliveries within a single generation
- The selected Persona sets the baseline voice; singer labels and texture tags create variation around it
- Character names in brackets (`[SERENA:]`) do NOT work — use singer labels and vocal texture tags instead
- Parentheses `()` in lyrics produce **backing vocal layers** — never use them for instructions like `(instrumental)` or `(whispered)`. Use bracket tags instead: `[Instrumental]`, `[Whispered]`

---

## Validation Rules

1. Every member must have all required fields populated (no empty strings except in blank templates)
2. `id` must be unique within the band's `members` array
3. Genre preference values must be integers 1-5
4. Personality trait values must be integers 1-5, all 5 traits present
5. `sampleLines` should contain at least 2 entries
6. `techniques` should contain at least 2 entries
7. Exactly one member should have `role: "leader"`
8. At least one member should have `position: "main-vocal"` or `position: "lead-vocal"`
