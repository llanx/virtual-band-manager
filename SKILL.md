---
name: virtual-band-manager
description: >-
  This skill should be used when the user asks to "write a song",
  "create a song", "band session", "manage the band",
  "create a band member", "edit a member", "genre blend",
  "suno tags", "build a track", "song concept", "write lyrics",
  "band overview", "band meeting", "negotiate genres",
  "create a band", "delete a band", "switch band",
  "create a universe", "delete a universe", "switch universe",
  "clean slate", "start fresh",
  or invokes /virtual-band-manager. Manages virtual bands
  across multiple universes, handling member personas, genre
  negotiation, and 5-phase song construction that outputs
  Suno-ready song scripts.
---

# Virtual Band Manager

A band manager brain that knows who the members are, what they sound like, what genres they gravitate toward, and how to translate all of that into Suno-ready song scripts with square-bracket stage directions. Bands persist across sessions via JSON profiles that drive every creative decision. Multiple bands can exist across isolated universes, each with their own lore, songs, and pattern tracking.

## Path Resolution

All paths in this skill use `{universe}` and `{band}` as placeholders that resolve from `active-context.json`:
- `{universe}` = the `activeUniverse` value (a universe slug)
- `{band}` = the `activeBand` value (a band slug)

Example: `universes/{universe}/bands/{band}.json` → `universes/cosmic-battle/bands/placeholderbandname.json`

## Workflow

### Step 1: Load Band

1. Read `active-context.json` from the project root. It contains `activeUniverse`, `activeBand`, and `lastAccessed`.
2. If the file exists and points to a valid universe and band, load the band profile from `universes/{universe}/bands/{band}.json`. Present a brief roster summary: member names, instruments, roles, and genre leanings. Display the active universe name alongside the roster.
3. If `active-context.json` is missing, empty, or points to nonexistent paths, enter **Selection Mode**:
   - List all universes found in `universes/` (read each `universe.json` for display names)
   - If zero universes exist, offer to create one (proceed to Step 3c)
   - If exactly one universe exists, auto-select it, then list its bands
   - If multiple universes exist, ask the user to pick one
   - Within the selected universe, list bands in `universes/{universe}/bands/`. Same logic: zero = offer creation, one = auto-select, multiple = ask
   - Update `active-context.json` with the selection

**Song DNA Registry:** The registry (`universes/{universe}/song-dna-registry.md`) is NOT consulted during writing. It exists as an optional rewrite aid after Phase 4 (see Step 7b) and is updated after Phase 5.

### Step 2: Select Mode

Offer modes based on user intent:

- **Song Session** -- Write a new song (proceed to Step 4)
- **Member Management** -- Create, edit, or view member profiles (proceed to Step 3)
- **Band Overview** -- Display full roster with personality summaries, genre preferences, and group dynamics
- **Band Management** -- Create, delete, switch, or list bands (proceed to Step 3b)
- **Universe Management** -- Create, delete, switch universes, or start fresh (proceed to Step 3c)

### Step 3: Member Management

**Creating a new member:**
1. Copy the structure from `templates/blank-member.json`
2. Interview the user conversationally -- gather: name, stage name, age, instrument, role, position, personality traits, genre preferences, vocal characteristics, visual aesthetic, backstory
3. If the active universe has `hasFantasyProfiles: true`, also gather fantasy profile details (class, title, weapon, fighting style, combat personality, signature, weakness)
4. Validate against the schema documented in `references/persona-schema.md`
5. Generate the full persona JSON from responses
6. Add to the band file at `universes/{universe}/bands/{band}.json` and save

**Editing an existing member:**
1. Load the member from the band file
2. Present current profile in a readable format
3. Accept targeted edits (e.g., "make her more assertive", "change the bassist's genre preference")
4. Save updated band file

**Removing a member:**
1. Confirm removal with the user
2. Remove from band file, preserve a backup note in the band's `history` field

### Step 3b: Band Management

**Creating a new band:**
1. Confirm the active universe (or ask which universe to create the band in)
2. Copy structure from `templates/blank-band.json`
3. Interview the user: band name, concept, formation date
4. Ask about lyric language config: monolingual or bilingual? If bilingual, gather primary language, secondary language, ratio, and placement rules. Save as `lyricLanguageConfig` in the band JSON
5. Generate a slug from the band name (lowercase, hyphens, no special characters)
6. Save to `universes/{universe}/bands/{slug}.json`
7. Create the empty songs directory: `universes/{universe}/songs/{slug}/`
8. Update `active-context.json` to point to the new band
9. Offer to proceed to Member Management (Step 3) to add the first member

**Deleting a band:**
1. List bands in the active universe with member counts
2. User selects which band to delete
3. Confirm with the user, displaying the band name and member count
4. Move the band file and its song directory to `_archive/` within the universe (soft delete, recoverable)
5. If the deleted band was the active band, clear `activeBand` in `active-context.json` and prompt for a new selection

**Switching bands:**
1. List all bands in the active universe with member counts
2. User picks one
3. Update `active-context.json`

**Listing bands:**
1. Read all `.json` files in `universes/{universe}/bands/`
2. Display band name, member count, and concept for each

### Step 3c: Universe Management

**Creating a new universe:**
1. Copy structure from `templates/blank-universe.json`
2. Interview: universe name, description, themes, whether it includes fantasy profiles
3. Generate slug (lowercase, hyphens, no special characters)
4. Create the directory tree: `universes/{slug}/`, `universes/{slug}/bands/`, `universes/{slug}/lore/`, `universes/{slug}/songs/`
5. Save `universe.json`
6. Initialize an empty `song-dna-registry.md` by copying `templates/blank-song-dna-registry.md`
7. Update `active-context.json` to point to the new universe (clear `activeBand`)
8. Offer to create the first band (proceed to Step 3b)

**Deleting a universe:**
1. List all universes with display names and band counts
2. User selects one
3. Double-confirm: display universe name, number of bands, and number of songs
4. Move the entire universe directory to a top-level `_archive/` folder (soft delete, recoverable)
5. If the deleted universe was active, clear `active-context.json` and prompt for new selection

**Switching universes:**
1. List all universes with display names and band counts
2. User picks one
3. Update `active-context.json` (set universe, clear `activeBand` since bands differ per universe)
4. Proceed to band selection within the new universe

**Clean slate:**
1. User explicitly requests "start fresh" or "clean slate"
2. Warn that this archives ALL universes and their content
3. Move entire `universes/` contents to `_archive/{date}/`
4. Clear `active-context.json`
5. Offer to create a new universe from scratch (proceed to Step 3c)

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
   - Lead vocal (the member with `position: main-vocal` by default for chorus, but varies by concept)
   - Supporting vocals, harmonies, ad-libs
   - Instrumental spotlights (solos and featured sections for each member's instrument)
4. Present the section map with member assignments for user approval

### Step 6: Song Construction -- Phase 3 (Lyrics)

Write lyrics section by section, in each member's voice:

- Each member's lines reflect their `lyricPatterns`, `personality`, and `vocalStyle` from the persona
- The member with `position: main-vocal` carries the most vocal weight but all members contribute
- Mark line distribution with member tags: `[STAGENAME]` (e.g., `[SERENA]`, `[KAIA]`)
- Mark harmonies: `[MEMBER1+MEMBER2]`, ad-libs: `[MEMBER ad-lib]`
- Use square brackets `[]` for ALL stage directions, performance notes, and member tags -- consistent with Suno's bracket notation. Member name tags get stripped in Phase 4, but bracket format carries through to Suno output.
- For pauses and silence, consult the Pause & Silence Guide in `references/suno-tag-reference.md`. Use `[Break]` for structural pauses, `[Sudden silence]` for dramatic cuts, and `...` for vocal hesitation. Avoid specifying exact durations -- Suno does not reliably respect them.
- Enforce thematic consistency with the concept brief
- Ensure natural transitions between vocal styles at section boundaries

Lyric voice guidelines per instrument archetype:
- **Vocalist (main-vocal):** Versatile, emotionally expressive, carries melody and hooks
- **Guitarist:** Edge and attitude in phrasing, guitar-influenced rhythmic patterns
- **Drummer:** Rhythmic, percussive syllable patterns, punchy delivery
- **Bassist:** Smooth, groove-oriented phrasing, laid-back cool
- **Keyboardist/Synth:** Atmospheric, layered phrasing, textural approach
- **Other instrumentalists:** Adapt vocal style to reflect their instrument's character

### Bilingual Lyric Rules (Conditional)

**These rules apply only if the active band has a `lyricLanguageConfig` with a non-empty `secondary` value.** If `lyricLanguageConfig` is absent or `secondary` is empty, write monolingual lyrics in the primary language and skip this section entirely.

When bilingual rules apply, use the configured `primary` and `secondary` languages and `ratio`:

- Target the configured ratio (e.g., 75–80% primary / 20–25% secondary) across the full song
- Secondary language placement — vary across the song using all three patterns:
  - **Mid-line substitution**: swap a phrase or 2–4 words to the secondary language within a primary-language line
  - **Full secondary-language line**: one complete line of a stanza written entirely in the secondary language
  - **Stanza position rotation**: alternate which line carries the secondary language — sometimes first, sometimes a middle line, sometimes the last
- Rhyme constraint: any secondary-language word or phrase that falls at a rhyme point must end on a syllable whose romanized pronunciation rhymes with the primary-language rhyme target of that stanza. Verify the match before finalizing the line.
- In the member-tagged lyrics (Phase 3 output), place a primary-language translation in parentheses immediately after every secondary-language phrase or line
- Do NOT include translations in the Suno-ready script (Phase 4).

### Step 6b: Song Construction -- Phase 3.5 (Lyric Review)

After completing Phase 3 lyrics, present the following review matrix to the user. This is a suggestion output -- the user decides which (if any) items to address before moving to Phase 4.

#### A. Lyric Logic Review

Scan the completed lyrics and surface any potential issues:

| Check | What to flag |
|-------|-------------|
| Thematic coherence | Lines that contradict or drift from the concept brief |
| Logical flow | Non-sequiturs between consecutive lines within a section |
| Mixed metaphors | Incompatible metaphors colliding in the same section |
| Awkward phrasing | Lines that sound unnatural or are contorted to force a rhyme |
| Emotional arc | Lines that undermine their section's intended mood |
| Member voice | Lines that feel out-of-character for the assigned member's persona |
| Korean integration | Korean phrases that feel forced or have inaccurate translations |

Present findings in a numbered table: line, issue, and a suggested alternative. If nothing is flagged, say so and move on.

#### B. Rhyme Review

Scan line-ending words and identify rhyme pairs within each section:

1. Flag any **same-word rhymes** (e.g., face/face) -- present for user approval
2. Flag any **identity rhymes with different meaning** (e.g., rock/rock as stone vs. music) -- note the dual meaning for user consideration
3. For any flagged pair, suggest 2-3 alternative words that preserve the line's meaning
4. Do NOT flag slant rhymes or near-rhymes -- these are legitimate technique

Present as a simple approval matrix:

| Line # | Rhyme pair | Type | Suggestion | Keep? |
|--------|-----------|------|------------|-------|

The user marks which to keep or revise, then proceed to Phase 4.

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

### Step 7b: Song Construction -- Phase 4.5 (DNA Registry Check — Optional)

If the user is unhappy with the Phase 4 output and wants to revise, the Song DNA Registry (`universes/{universe}/song-dna-registry.md`) can be consulted as a rewrite aid. This step is **never automatic** — the user must request it.

When consulted:
1. Read the registry and compare the current song's lyrics against tracked patterns
2. Flag any overlap with `[SATURATED]` or `[WATCH]` patterns — imagery, structural devices, Korean phrases, rhyme targets, ad-libs, breakdown formulas
3. Suggest specific alternatives for flagged patterns, drawing on fresh/unused options from the registry
4. The user decides which suggestions to accept; revise the Phase 3 lyrics and re-run Phase 4

This exists so the user can check for unintentional repetition across the catalog without having to re-read every previous song.

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
8. Save the final song output to `universes/{universe}/songs/{band}/` using the track number and title as filename (e.g., `05-steel-and-spell.md`)
9. After the user approves, update `universes/{universe}/song-dna-registry.md`:
   a. Add the new song to the Song Fingerprints table
   b. Scan the finalized lyrics for all tracked pattern categories
   c. Update pattern counts, track lists, and Status flags
   d. Add any new patterns not yet tracked
   e. Recalculate statuses: 1 use = `OK`, 2 = `[WATCH]`, 3+ = `[SATURATED]`

## Genre Negotiation

When determining a song's genre:

1. Identify which members are featured (default: all 4)
2. Collect each member's `genrePreferences` weighted by their preference scores (1-5)
3. Factor in member assertiveness -- higher assertiveness pushes harder for their preferred genre
4. Check genre compatibility using `references/genre-matrix.md`
5. Produce: **Primary genre**, **Secondary influence**, **Optional accent**
6. Allow manual override at any point ("make this a straight rock track")

When two members with different affinities are both prominent, suggest fusion genres. Example: a rock-leaning guitarist + an R&B-leaning bassist = "alt-R&B with guitar edge."

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
- The band file path resolves from `active-context.json` → `universes/{universe}/bands/{band}.json`

## Additional Resources

For detailed guidance, consult:

**Shared references (universal, not universe-specific):**
- **`references/persona-schema.md`** -- Read when creating or editing members. Documents every JSON field, valid enum values, validation rules, universe schema, and lyric language config
- **`references/genre-matrix.md`** -- Read during Phase 1 genre negotiation. Contains compatibility scores for 13 genres and the blending algorithm
- **`references/kpop-structures.md`** -- Read during Phase 2 structure selection. Contains 5 song structure templates with section durations and member distribution guidelines
- **`references/suno-tag-reference.md`** -- Read during Phase 4. Contains Suno's two-input-field system (Style Prompt vs. Lyrics), bracket tag reference, lyric formatting symbols (parentheses = backing vocals, ALL CAPS, hyphens), pipe stacking syntax, Style Prompt construction guide, key/scale reference, time signatures, genre anchors, and segment splitting guidance
- **`references/persona-schema.md` → Suno Persona section** -- Read during Phase 4. Documents `sunoPersona` fields, effective vocal tags, and singer labels

**Templates:**
- **`templates/blank-member.json`** -- Copy when creating a new band member
- **`templates/blank-band.json`** -- Copy when creating a new band (includes `lyricLanguageConfig`)
- **`templates/blank-universe.json`** -- Copy when creating a new universe
- **`templates/blank-song-dna-registry.md`** -- Copy when initializing a new universe's DNA registry
- **`templates/song-concept-brief.md`** -- Fill during Phase 1 output
- **`templates/song-output.md`** -- Fill during Phase 5 assembly

**Universe-specific resources (paths resolve from `active-context.json`):**
- **`universes/{universe}/bands/{band}.json`** -- Active band profile
- **`universes/{universe}/universe.json`** -- Universe metadata (themes, fantasy profile toggle)
- **`universes/{universe}/lore/`** -- Universe-specific story, timeline, and world-building files
- **`universes/{universe}/songs/{band}/`** -- Songs for the active band
- **`universes/{universe}/song-dna-registry.md`** -- Optional rewrite aid (Phase 4.5). Never consulted before or during writing. If the user wants to check for unintentional repetition after seeing the Phase 4 output, consult this file to flag overlapping patterns and suggest alternatives. Updated after Phase 5 finalization. Tracks imagery, structural devices, language usage, rhyme targets, ad-libs, and breakdown patterns across all songs. Flags patterns as `OK` / `[WATCH]` / `[SATURATED]` based on reuse frequency

**Other:**
- **Step 6b (Lyric Review)** -- Optional review matrix after Phase 3. Surfaces logic issues and same-word rhymes for user consideration
