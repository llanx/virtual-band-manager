---
name: virtual-band-manager
description: >-
  This skill should be used when the user asks to "write a song",
  "create a song", "band session", "manage the band",
  "create a band member", "edit a member", "genre blend",
  "suno tags", "build a track", "song concept", "write lyrics",
  "band overview", "band meeting", "negotiate genres",
  or invokes /virtual-band-manager. Manages a virtual band,
  handling member personas, genre negotiation, and 5-phase
  song construction that outputs Suno-ready song scripts.
---

# Virtual Band Manager

A band manager brain that knows who the members are, what they sound like, what genres they gravitate toward, and how to translate all of that into Suno-ready song scripts with square-bracket stage directions. The band persists across sessions via JSON profiles that drive every creative decision.

## Workflow

### Step 1: Load Band

Read the band profile from `bands/` directory. If no band file exists, offer to create one using the member management workflow. Present a brief roster summary: member names, instruments, roles, and genre leanings.

### Step 2: Select Mode

Offer three modes based on user intent:

- **Song Session** -- Write a new song (proceed to Step 4)
- **Member Management** -- Create, edit, or view member profiles (proceed to Step 3)
- **Band Overview** -- Display full roster with personality summaries, genre preferences, and group dynamics

### Step 3: Member Management

**Creating a new member:**
1. Copy the structure from `templates/blank-member.json`
2. Interview the user conversationally -- gather: name, stage name, age, instrument, role, position, personality traits, genre preferences, vocal characteristics, visual aesthetic, backstory
3. Validate against the schema documented in `references/persona-schema.md`
4. Generate the full persona JSON from responses
5. Add to the band file and save

**Editing an existing member:**
1. Load the member from the band file
2. Present current profile in a readable format
3. Accept targeted edits (e.g., "make Kaia more assertive", "change Evie's genre preference")
4. Save updated band file

**Removing a member:**
1. Confirm removal with the user
2. Remove from band file, preserve a backup note in the band's `history` field

### Step 4: Song Construction -- Phase 1 (Concept)

Gather the song's creative direction:

1. Ask for song intent -- mood, theme, narrative purpose, energy level
2. Optionally ask for game context (which biome/stage, BPM range, gameplay energy)
3. Run genre negotiation (see Genre Negotiation section below)
4. Each member "pitches" the concept in 1-2 sentences reflecting their personality
5. Produce a concept brief using `templates/song-concept-brief.md`
6. **Confirm the concept brief with the user before proceeding**

### Step 5: Song Construction -- Phase 2 (Structure)

Select and adapt a song structure:

1. Choose a structure template from `references/kpop-structures.md` based on the concept
2. Adapt the template -- adjust section count, lengths, add or remove bridge/breakdown
3. Assign members to each section:
   - Lead vocal (Serena by default for chorus, but varies by concept)
   - Supporting vocals, harmonies, ad-libs
   - Instrumental spotlights (guitar solo for Kaia, drum break for Mika, bass groove for Evie)
4. Present the section map with member assignments for user approval

### Step 6: Song Construction -- Phase 3 (Lyrics)

Write lyrics section by section, in each member's voice:

- Each member's lines reflect their `lyricPatterns`, `personality`, and `vocalStyle` from the persona
- Serena carries the most vocal weight (lead singer) but all members contribute
- Mark line distribution with member tags: `[SERENA]`, `[KAIA]`, etc.
- Mark harmonies: `[SERENA+EVIE]`, ad-libs: `[MIKA ad-lib]`
- Use square brackets `[]` for ALL stage directions, performance notes, and member tags -- consistent with Suno's bracket notation. Member name tags get stripped in Phase 4, but bracket format carries through to Suno output.
- Enforce thematic consistency with the concept brief
- Ensure natural transitions between vocal styles at section boundaries

Lyric voice guidelines per instrument archetype:
- **Vocalist (Serena):** Versatile, emotionally expressive, carries melody and hooks
- **Guitarist (Kaia):** Edge and attitude in phrasing, guitar-influenced rhythmic patterns
- **Drummer (Mika):** Rhythmic, percussive syllable patterns, punchy delivery
- **Bassist (Evie):** Smooth, groove-oriented phrasing, laid-back cool

### Bilingual Lyric Rules (English/Korean)

- Target ratio: 75–80% English, 20–25% Korean across the full song
- Korean placement — vary across the song using all three patterns:
  - **Mid-line substitution**: swap a phrase or 2–4 words to Korean within an English line
    e.g. `"I'm still running 달려가 through the fire"`
  - **Full Korean line**: one complete line of a stanza written entirely in Korean
  - **Stanza position rotation**: alternate which line carries the Korean — sometimes first, sometimes a middle line, sometimes the last
- Rhyme constraint: any Korean word or phrase that falls at a rhyme point must end on a syllable whose romanized pronunciation rhymes with the English rhyme target of that stanza. Verify the match before finalizing the line.
- In the member-tagged lyrics (Phase 3 output), place an English translation in parentheses immediately after every Korean phrase or line:
  e.g. `[SERENA] 우리는 여기 있어 (we are still here) — don't you dare look away`
  e.g. `[KAIA] Burn the script, 내 방식대로 (my own way), every chord a throne`
- Do NOT include translations in the Suno-ready script (Phase 4).

### Step 7: Song Construction -- Phase 4 (Suno Tags)

Convert the Phase 3 lyrics into a single Suno-ready script. The output is one cohesive text that gets pasted directly into Suno's custom lyrics field in a single generation.

1. Consult `references/suno-tag-reference.md` for valid bracket syntax, formatting symbols, and Style Prompt construction
2. **Recommend a Persona**: Pick the member who dominates the song (usually Serena for chorus-heavy tracks). The user selects this Persona in Suno before generating.
3. **Compose the Style Prompt** for Suno's Style Prompt box (separate from lyrics). Front-load the most important descriptors. Include genre, vocal type, mood, BPM, key. Blend the song's negotiated genre with the lead Persona's `genrePairing`. Keep under 1,000 characters. Example: `Alt-pop, indie rock, powerful female vocals, energetic, 145 BPM, E minor, polished production`
   - 3a. **Compose Exclude Styles suggestion** (optional, Pro/Premier feature). List styles to avoid. Example: `country twang, Auto-Tune, mumble rap`
4. **Convert each section** from Phase 3 lyrics:
   a. Add structural tags: `[Verse 1]`, `[Chorus]`, `[Bridge]`, `[Build]`, `[Drop]`, `[Breakdown]`, etc.
   b. At each section boundary where the lead vocalist changes, add the member's `sunoLabel` + `effectiveVocalTags`. Example: `[Singer B, raspy female vocal, gritty delivery]`. This nudges Suno toward a different vocal delivery for that section.
   c. Add instrument tags: `[Electric guitar riff]`, `[Drum fill]`, `[Bass groove]`
   d. Add mood/energy tags from the concept: `[Building intensity]`, `[Aggressive]`
   e. Strip ALL member name tags — replace with sunoLabels and vocal texture tags
   f. Strip all parenthetical translation annotations — Korean characters pass through as-is, but remove any `(translation text)` that follows them. Do NOT add `[Korean]` or `[English]` language tags; Suno does not use them and they waste the tag budget.
5. For shared/group sections (gang vocals, chants), use `[Group chant]`, `[All singers]`, or `[Layered vocals]` tags
6. Keep tags to 2-4 per section — over-tagging causes Suno to ignore some. Use pipe stacking (`[element | modifier | modifier]`) when combining multiple cues in a single bracket for compactness
7. If the script exceeds ~5,000 characters, split into two segments with 2-4 lines of overlap at the boundary and `[Continuation]` tag on segment 2. Segment 2 does NOT need genre repeated (genre lives in Style Prompt, not lyrics)

### Step 8: Song Construction -- Phase 5 (Final Output)

Compile the final output using `templates/song-output.md`:

1. Include metadata: genre, BPM, duration, structure template used
2. Include singer label map (member → Singer A/B/C/D → voice profile)
3. Include the concept brief (or summary)
4. Include full lyrics with member assignment tags (for reference)
5. Include the Suno-ready output with two components: **Style Prompt** (for the Style Prompt box) and **lyrics script** (for the Lyrics field). Ready to copy-paste into their respective Suno fields.
6. Include generation notes:
   - Which Persona to select (or seed prompt if no Persona saved)
   - Style Prompt to paste into Suno's Style Prompt box
   - Exclude Styles suggestion (if applicable)
   - Slider combo recommendations:
     - **Radio-ready**: Style Influence 80%+, Weirdness low
     - **Experimental**: Style Influence 50-70%, Weirdness mid-high
     - **Persona showcase**: Style Influence 85%+, Weirdness low
     - **Genre fusion**: Style Influence 60-75%, Weirdness mid
   - If split into segments: overlap lines and stitching notes
7. Present to the user for final review

## Genre Negotiation

When determining a song's genre:

1. Identify which members are featured (default: all 4)
2. Collect each member's `genrePreferences` weighted by their preference scores (1-5)
3. Factor in member assertiveness -- higher assertiveness pushes harder for their preferred genre
4. Check genre compatibility using `references/genre-matrix.md`
5. Produce: **Primary genre**, **Secondary influence**, **Optional accent**
6. Allow manual override at any point ("make this a straight rock track")

When two members with different affinities are both prominent, suggest fusion genres. Example: rock-leaning Kaia + R&B-leaning Evie = "alt-R&B with guitar edge."

## In-Character Dialogue

When simulating member reactions (pitches, negotiations, feedback on lyrics):

- Use personality traits from the persona (assertiveness, playfulness, perfectionism, emotionalOpenness, competitiveness)
- Keep dialogue brief: 1-3 sentences per member per beat
- Reflect each member's instrument identity in how they think about music
- Create natural interpersonal dynamics (agreements, friendly disagreements, compromises)

## Key Constraints

- Always load the band file before any operation. If missing, offer to create from template
- Never fabricate member details not present in the persona JSON. If a trait is unspecified, ask the user or mark as TBD
- The final output includes two components: a **Style Prompt** (for Suno's Style Prompt box) and a **lyrics script** (for the Lyrics field). Both must be copy-pasteable without modification — one generation
- Use `sunoPersona.effectiveVocalTags` and `sunoLabel` for vocal style tags — never use classical range terms or character names in Suno output
- Keep the pipeline interruptible -- the user can stop after any phase and resume later
- All member changes save immediately to the band JSON file
- When writing lyrics, respect each member's syllable density, rhyme style, and thematic preferences from their persona
- The band file path must be provided when the skill loads (check `bands/` directory for available bands)

## Additional Resources

For detailed guidance, consult:

- **`references/persona-schema.md`** -- Read when creating or editing members. Documents every JSON field, valid enum values, and validation rules
- **`references/genre-matrix.md`** -- Read during Phase 1 genre negotiation. Contains compatibility scores for 13 genres and the blending algorithm
- **`references/kpop-structures.md`** -- Read during Phase 2 structure selection. Contains 5 song structure templates with section durations and member distribution guidelines
- **`references/suno-tag-reference.md`** -- Read during Phase 4. Contains Suno's two-input-field system (Style Prompt vs. Lyrics), bracket tag reference, lyric formatting symbols (parentheses = backing vocals, ALL CAPS, hyphens), pipe stacking syntax, Style Prompt construction guide, key/scale reference, time signatures, genre anchors, and segment splitting guidance
- **`references/persona-schema.md` → Suno Persona section** -- Read during Phase 4. Documents `sunoPersona` fields, effective vocal tags, and singer labels
- **`templates/blank-member.json`** -- Copy when creating a new band member
- **`templates/song-concept-brief.md`** -- Fill during Phase 1 output
- **`templates/song-output.md`** -- Fill during Phase 5 assembly
