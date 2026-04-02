# Suno Tag & Style Reference

Complete guide to Suno's input system — covering the Style Prompt box, the Lyrics field (bracket tags + formatting symbols), and production techniques.

---

## Suno's Two Input Fields

Suno has two separate text inputs that serve different purposes. Do not conflate them.

### Style Prompt Box (up to 1,000 characters)

Plain text describing the overall sound. This is where genre, BPM, key, mood, vocal type, and texture belong. Suno uses this to set the global production character for the entire generation.

**What goes here:**
- Genre and sub-genre (e.g., `alt-pop, indie rock`)
- BPM (e.g., `140 BPM`)
- Key (e.g., `E minor`)
- Vocal type (e.g., `powerful female vocals`)
- Mood and energy (e.g., `energetic, anthemic`)
- Production texture (e.g., `lo-fi warmth, vinyl crackle`)

**Rules:**
- Front-load the most important descriptors — Suno weighs earlier words more heavily
- Plain text only — no brackets, no special formatting
- Do NOT duplicate genre/BPM/key inside the Lyrics field

**Recommended order:** Genre → vocal type → mood/energy → BPM → key → texture/production notes

**Example:**
```
Alt-pop, indie rock, powerful female vocals, energetic, anthemic, 140 BPM, E minor, polished production, stadium reverb
```

### Exclude Styles (Pro/Premier feature)

A separate field where you list styles to avoid. Helps Suno steer away from unwanted influences.

**Example:** `country twang, Auto-Tune, mumble rap, acoustic folk`

### Lyrics Field (up to 5,000 characters in V5)

This is where bracket tags and actual lyrics go. Structure tags, vocal delivery tags, instrument cues, and mood shifts live here — everything that controls section-by-section behavior.

**Rules:**
- Use square brackets `[]` for ALL instructions and section markers
- Genre, BPM, and key do NOT belong here (they go in Style Prompt)
- Parentheses `()` are NOT instructions — they produce backing vocal layers (see Lyric Formatting Symbols)

---

## Tag Categories

### 1. Structural Tags (Section Markers)

Define song structure. Place at the start of each section.

| Tag | Usage |
|-----|-------|
| `[Intro]` | Opening section, often instrumental |
| `[Verse]` or `[Verse 1]`, `[Verse 2]` | Numbered verses |
| `[Pre-Chorus]` | Build-up before chorus |
| `[Chorus]` | Main hook section |
| `[Post-Chorus]` | After chorus, maintains energy |
| `[Bridge]` | Contrasting section, usually before final chorus |
| `[Outro]` | Closing section |
| `[Break]` or `[Instrumental Break]` | Non-vocal section |
| `[Interlude]` | Brief transitional section |
| `[Rap]` or `[Rap Verse]` | Rap section |
| `[Hook]` | Repeated catchy phrase |
| `[Build]` | Gradual intensity increase, often before a drop |
| `[Drop]` | High-energy payoff after a build |
| `[Breakdown]` | Stripped-back section, usually mid-song |
| `[Solo]` | Instrumental solo section |
| `[Final Chorus]` | Last chorus, typically biggest arrangement |
| `[Beat switch]` | Rhythm, tempo, or feel change |

### 2. Vocal Style Tags

Describe how the vocals should sound for the following section.

#### Gender & Type
| Tag | Effect |
|-----|--------|
| `[Female vocal]` | General female voice |
| `[Male vocal]` | General male voice |
| `[Androgynous vocal]` | Gender-ambiguous voice |
| `[Duet]` | Two distinct vocal parts |

#### Power & Delivery
| Tag | Effect |
|-----|--------|
| `[Powerful female vocal]` | Strong, belting delivery |
| `[Soft female vocal]` | Gentle, intimate delivery |
| `[Breathy vocal]` | Airy, intimate quality |
| `[Raspy vocal]` | Rough, textured voice |
| `[Whispered]` | Very soft, close-mic feel |
| `[Belting]` | Full-power sustained notes |
| `[Falsetto]` | High, airy register |
| `[Crooning]` | Smooth, warm, jazz-influenced delivery |
| `[Operatic]` | Classical vocal power and vibrato |
| `[Growl]` | Low, gritty, aggressive vocal |
| `[Scream]` | High-intensity, punk/metal vocal |
| `[Talk-singing]` | Conversational melodic delivery |
| `[Spoken word]` | Non-melodic delivery |
| `[Sing-rap]` | Melodic rap style |

#### Emotion & Expression
| Tag | Effect |
|-----|--------|
| `[Emotional delivery]` | Expressive, feeling-forward |
| `[Defiant vocal]` | Bold, confrontational tone |
| `[Vulnerable vocal]` | Raw, exposed emotional quality |
| `[Playful vocal]` | Light, fun delivery |
| `[Yearning vocal]` | Longing, aching quality |

#### Vocal Effects
| Tag | Effect |
|-----|--------|
| `[Autotune vocal]` | Pitch-corrected, modern pop/trap feel |
| `[Vocoder]` | Robotic, synth-processed vocal |
| `[Distorted vocal]` | Overdriven, lo-fi vocal processing |
| `[Filtered vocal]` | Telephone or radio effect |
| `[Reverb-drenched vocal]` | Spacious, ambient vocal wash |

#### Group & Harmony
| Tag | Effect |
|-----|--------|
| `[Harmonies]` or `[Layered vocals]` | Multiple vocal layers |
| `[Chanting]` | Rhythmic group chant |
| `[Call and response]` | Back-and-forth vocal pattern |
| `[Ad-libs]` | Improvised vocal additions |
| `[Vocal runs]` | Melismatic embellishments |
| `[Choir]` | Full choral sound |
| `[Group chant]` | Unison rhythmic vocals |
| `[All singers]` | Full ensemble vocals |

#### Rap Delivery
| Tag | Effect |
|-----|--------|
| `[Rap]` or `[Fast rap]` | Rhythmic spoken delivery |
| `[Slow rap]` | Laid-back, deliberate flow |
| `[Aggressive rap]` | Hard-hitting, intense flow |
| `[Melodic rap]` | Sing-rap hybrid |

### 3. Instrument Tags

Specify instrumental elements for a section.

#### Keys & Synths
| Tag | Effect |
|-----|--------|
| `[Piano]` or `[Grand piano]` | Piano accompaniment |
| `[Electric piano]` | Rhodes or Wurlitzer tone |
| `[Organ]` | Hammond or church organ |
| `[Synth]` or `[Synth lead]` | Synthesizer prominence |
| `[Synth pad]` | Sustained synth atmosphere |
| `[Synth arpeggio]` | Rhythmic synth pattern |
| `[Synth bass]` | Electronic bass tone |
| `[Synth drop]` | Electronic drop moment |
| `[Analog synth]` | Warm, vintage synth character |
| `[Modular synth]` | Experimental electronic textures |

#### Guitars & Strings
| Tag | Effect |
|-----|--------|
| `[Electric guitar]` or `[Guitar riff]` | Prominent guitar |
| `[Acoustic guitar]` | Clean acoustic |
| `[Clean guitar]` | Undistorted electric guitar |
| `[Distorted guitar]` | Overdriven, heavy guitar |
| `[Guitar solo]` | Extended guitar lead |
| `[Power chords]` | Chunky, rock guitar |
| `[Fingerpicking]` | Delicate acoustic technique |
| `[Slide guitar]` | Blues/country slide technique |
| `[12-string guitar]` | Jangly, full acoustic sound |
| `[Bass guitar]` or `[Bass groove]` | Prominent bass |
| `[Slap bass]` | Funk-style percussive bass |
| `[Bass drop]` | Heavy low-end hit |
| `[Strings]` or `[Orchestral strings]` | String arrangement |
| `[Violin]` | Solo violin |
| `[Cello]` | Solo cello |
| `[Pizzicato strings]` | Plucked string technique |
| `[String swell]` | Rising string crescendo |
| `[Ukulele]` | Light, bright strumming |
| `[Banjo]` | Twangy, bright plucking |
| `[Harp]` | Glissando or arpeggiated harp |

#### Drums & Percussion
| Tag | Effect |
|-----|--------|
| `[Drums]` or `[Heavy drums]` | Drum emphasis |
| `[Drum fill]` | Transitional drum pattern |
| `[Drum machine]` | Electronic, programmed drums |
| `[808 bass]` | Trap-style sub bass |
| `[808 hi-hats]` | Rapid trap hi-hat patterns |
| `[Boom bap drums]` | Classic hip-hop drum pattern |
| `[Snare roll]` | Building snare pattern |
| `[Kick drum]` | Prominent bass drum |
| `[Rim shot]` | Sharp, metallic drum hit |
| `[Percussion]` | General hand percussion |
| `[Claps]` | Handclap rhythm |
| `[Tambourine]` | Shaker/tambourine accent |
| `[Congas]` | Latin hand drums |
| `[Bongos]` | Small paired drums |
| `[Shaker]` | Rhythmic shaker pattern |

#### Brass & Wind
| Tag | Effect |
|-----|--------|
| `[Trumpet]` | Solo or section trumpet |
| `[Trombone]` | Low brass |
| `[Saxophone]` | Solo sax |
| `[Alto sax]` | Alto saxophone specifically |
| `[Tenor sax]` | Tenor saxophone specifically |
| `[Brass section]` | Full horn section |
| `[Flute]` | Woodwind flute |
| `[Clarinet]` | Woodwind clarinet |
| `[Harmonica]` | Blues harp |

#### Orchestral & Cinematic
| Tag | Effect |
|-----|--------|
| `[Orchestra]` | Full orchestral arrangement |
| `[Orchestral hit]` | Dramatic stab/accent |
| `[Timpani]` | Orchestral kettledrums |
| `[French horn]` | Warm, cinematic brass |
| `[Choir]` | Vocal ensemble |
| `[Music box]` | Delicate, tinkling melody |
| `[Glockenspiel]` | Bright, metallic bell tone |
| `[Marimba]` | Warm, wooden mallet percussion |

### 4. Mood & Energy Tags

Set the emotional tone of a section.

| Tag | Effect |
|-----|--------|
| `[Energetic]` | High energy, upbeat |
| `[Melancholic]` | Sad, reflective |
| `[Aggressive]` | Hard-hitting, intense |
| `[Dreamy]` | Ethereal, floating |
| `[Dark]` | Moody, minor key |
| `[Triumphant]` | Victorious, uplifting |
| `[Intimate]` | Close, personal |
| `[Building intensity]` | Growing energy |
| `[Sudden silence]` | Dramatic pause |
| `[Explosive]` | Sudden high energy |
| `[Bittersweet]` | Mixed emotions |
| `[Anthemic]` | Stadium-scale, singalong |
| `[Nostalgic]` | Wistful, longing for the past |
| `[Euphoric]` | Overwhelming joy, peak energy |
| `[Haunting]` | Eerie, lingering unease |
| `[Playful]` | Light, fun, bouncy |
| `[Cinematic]` | Epic, film-score scale |
| `[Gritty]` | Raw, unpolished, street-level |
| `[Ethereal]` | Otherworldly, floating |
| `[Tension]` | Suspenseful, unresolved |
| `[Swagger]` | Confident, cool energy |
| `[Solemn]` | Serious, grave, weighty |
| `[Chaotic]` | Unhinged, disordered energy |
| `[Serene]` | Calm, peaceful, still |
| `[Defiant]` | Bold, rebellious |
| `[Wistful]` | Gentle longing, thoughtful |
| `[Angry]` | Raw anger, intensity |

### 5. Production Tags

Control production and arrangement elements.

#### Arrangement
| Tag | Effect |
|-----|--------|
| `[Stripped back]` | Minimal instrumentation |
| `[Full band]` | All instruments playing |
| `[A cappella]` | Vocals only |
| `[Instrumental]` | No vocals, instruments only |
| `[Sparse arrangement]` | Very few instruments |
| `[Dense arrangement]` | Many layered instruments |
| `[Minimalist]` | Bare essentials only |
| `[Maximalist]` | Everything at once, wall of sound |

#### Dynamics & Transitions
| Tag | Effect |
|-----|--------|
| `[Crescendo]` | Building to peak |
| `[Decrescendo]` | Fading down |
| `[Tempo change]` | Shift in speed |
| `[Key change]` | Modulation (usually up for final chorus) |
| `[Fade out]` | Gradual volume decrease |
| `[Hard stop]` | Abrupt ending |
| `[Sudden silence]` | All instruments cut -- dramatic moment |
| `[Break]` | Non-vocal pause -- instruments may continue softly |
| `[Pause]` | Brief pause -- Suno decides duration |
| `[Slow build]` | Gradual layering of elements |
| `[Dynamic contrast]` | Loud-quiet-loud shifts |

#### Mix Character
| Tag | Effect |
|-----|--------|
| `[Lo-fi]` | Warm, degraded, vintage quality |
| `[Polished production]` | Clean, radio-ready mix |
| `[Raw recording]` | Unprocessed, live feel |
| `[Spacious mix]` | Wide stereo, reverb-heavy |
| `[Dry mix]` | Minimal reverb, upfront |
| `[Warm mix]` | Rounded, analog-style tone |
| `[Crisp mix]` | Bright, detailed highs |

#### Atmosphere & Ambient
| Tag | Effect |
|-----|--------|
| `[Ambient textures]` | Background sonic atmosphere |
| `[Rain sounds]` | Nature ambience |
| `[Vinyl crackle]` | Record player noise |
| `[Static]` | Electronic noise texture |
| `[Echo]` | Repeated delay effect |
| `[Reverb]` | Spacious room sound |

---

## Lyric Formatting Symbols

These symbols go inside the Lyrics field and affect how Suno renders text.

### Parentheses `( )` — Backing Vocal Layer

Text in parentheses is sung as a **background vocal**, like a backing singer echoing or harmonizing. This is NOT an instruction mechanism.

```
I won't let go (won't let go)
Standing tall (standing tall) in the fire
```

**WARNING:** Never use parentheses for production instructions. `(instrumental)`, `(guitar solo)`, `(whispered)` will be sung as backing vocals, not interpreted as directions. Use bracket tags instead: `[Instrumental]`, `[Guitar solo]`, `[Whispered]`.

### Hyphen `-` — Syllable Stretch

A hyphen between syllables extends/stretches the word across more beats.

```
I'm fal-ling a-part tonight
Hold o-o-on to me
```

### ALL CAPS — Emphasis/Force

Writing 1-3 words in ALL CAPS tells Suno to deliver them with extra force or emphasis. Use sparingly — overuse reduces impact.

```
I will NEVER let you down
We are ALIVE tonight
```

Do NOT capitalize entire lines or more than 3 consecutive words — Suno may ignore it or produce distorted results.

### Ellipsis `...` — Pause

An ellipsis creates a brief **pause** in delivery. It does not sustain a note.

```
And then I realized... it was over
Wait... no
```

### Ad-lib Format

Use the `[adlib]` tag followed by the sound in ALL CAPS:

```
[adlib] YEAH
[adlib] OH OH OH
[adlib] HEY
```

---

## Pipe Stacking Syntax

Combine multiple modifiers in a single bracket tag using pipes `|`. This lets you layer instructions concisely.

```
[Verse 1 | soft female vocal | acoustic guitar | intimate]
[Chorus | belting | full band | anthemic | building intensity]
```

**Rules:**
- Keep to 4-6 elements max per stacked tag — beyond that Suno may ignore some
- The first element is typically the structural tag
- Order matters less within a stacked tag, but put the most important descriptor early
- This is equivalent to separate bracket lines but more compact

---

## Style Prompt Construction Guide

The Style Prompt box is Suno's strongest lever for overall sound. Build it carefully.

### Recommended Order

```
[Genre] [Sub-genre], [Vocal type], [Mood/Energy], [BPM], [Key], [Production texture]
```

### Front-Loading

Suno weights the beginning of the Style Prompt more heavily. Put your most important descriptors first.

**Good:** `Indie rock, female vocals, melancholic, 120 BPM, A minor, lo-fi warmth`
**Weak:** `120 BPM, A minor, indie rock with female vocals and melancholic mood`

### Example Style Prompts

**Radio-ready pop:**
```
Pop, female vocals, catchy, polished production, 118 BPM, C major, bright, uplifting
```

**Dark indie:**
```
Indie rock, alt-pop, breathy female vocal, melancholic, 95 BPM, D minor, lo-fi, reverb-heavy
```

**Aggressive rock:**
```
Hard rock, powerful female vocals, aggressive, gritty, 145 BPM, E minor, distorted guitars, heavy drums
```

**Chill R&B:**
```
R&B, neo-soul, smooth female vocal, sultry, laid-back, 85 BPM, Ab major, warm bass, lush pads
```

---

## Key & Scale Reference

Key choice affects mood. Use this as a guide when specifying key in the Style Prompt.

| Key | Mood Character |
|-----|---------------|
| C major | Bright, pure, happy |
| C minor | Dark, dramatic, tense |
| D major | Triumphant, joyful, energetic |
| D minor | Melancholic, serious, introspective |
| E major | Bright, powerful, confident |
| E minor | Emotional, moody, versatile (very common in rock/pop) |
| F major | Warm, pastoral, calm |
| F minor | Dark, passionate, intense |
| G major | Happy, driving, uplifting |
| G minor | Brooding, dark, elegant |
| A major | Warm, bright, open |
| A minor | Sad, reflective, natural minor feel |
| Bb major | Bold, warm, rich |
| Bb minor | Very dark, heavy, somber |
| Eb major | Heroic, bold, majestic |
| Ab major | Lush, romantic, smooth (great for R&B) |

### Scales Beyond Major/Minor

You can specify modes and scales in the Style Prompt for more specific color:

- **Dorian** — minor with a brighter 6th (jazz, funk, indie)
- **Mixolydian** — major with a flat 7th (rock, blues, folk)
- **Pentatonic** — 5-note scale (blues, rock, pop hooks)
- **Harmonic minor** — dramatic, Middle Eastern inflection
- **Blues scale** — gritty, soulful quality

---

## Time Signature Tags

Suno defaults to 4/4. For other feels, specify in the Style Prompt or as a bracket tag.

| Tag / Style Prompt Text | Feel |
|-------------------------|------|
| `3/4` or `waltz` | Waltz feel, three beats per bar |
| `6/8` | Compound time, flowing/swaying feel (ballads, folk) |
| `7/8` | Asymmetric, progressive feel |
| `swing` | Jazz swing feel, triplet-based |
| `shuffle` | Shuffled eighth notes, blues/rock groove |
| `half-time` | Half-time feel, heavy and spacious |
| `double-time` | Double-time feel, fast and driving |

---

## Genre Anchors

Genre is Suno's strongest signal for overall sound. Anchoring to a specific genre gives Suno a clear sonic target.

### High-Value Genre Anchors

| Genre | Character |
|-------|-----------|
| Pop | Clean, catchy, radio-ready, hook-driven |
| Rock | Guitar-driven, energetic, dynamic |
| Indie Rock | Lo-fi edge, organic, less polished than pop |
| Alt-Pop | Experimental pop, synth-forward, atmospheric |
| Punk Rock | Fast, raw, aggressive, DIY energy |
| Pop-Punk | Catchy hooks + punk energy, driving drums |
| Grunge | Heavy, distorted, raw, 90s influence |
| Metal | Heavy, aggressive, complex, powerful |
| R&B | Smooth, groove-based, vocal-forward |
| Neo-Soul | Warm, organic, jazzy R&B |
| Hip-Hop | Beat-driven, rhythmic vocals, bass-heavy |
| Trap | 808s, hi-hats, dark, heavy bass |
| EDM | Electronic, build-and-drop, high energy |
| House | Four-on-the-floor, groovy, electronic |
| Synthwave | 80s retro, analog synths, nostalgic |
| Lo-fi | Warm, degraded, chill, imperfect |
| Jazz | Improvised, complex harmony, swing |
| Blues | 12-bar, soulful, guitar-driven, raw |
| Folk | Acoustic, storytelling, organic |
| Country | Twangy, narrative, guitar/fiddle |
| Funk | Groovy, bass-heavy, rhythmic |
| Soul | Emotional, vocal-driven, warm |
| Gospel | Spiritual, choir-heavy, powerful vocals |
| Classical | Orchestral, composed, dynamic |
| Reggaeton | Latin, dancehall, dembow rhythm |
| Bossa Nova | Brazilian, gentle, jazzy |
| K-pop | Polished, genre-blending, high production |
| Ballad | Slow, emotional, vocal-focused |
| Power Ballad | Slow build to big chorus, arena-scale |
| Acoustic | Unplugged, organic, intimate |

### Genre Fusion Pairs

Some genres blend naturally — others fight. Use this to guide fusion choices.

**Strong Fusion Pairs** (reinforce each other):
- Pop + Rock → power-pop, pop-rock
- Indie + Electronic → indie-electronic, synth-pop
- R&B + Hip-Hop → contemporary R&B
- Rock + Blues → blues-rock
- Pop + EDM → dance-pop, electropop
- Jazz + Hip-Hop → jazz-rap, lo-fi hip-hop
- Folk + Rock → folk-rock, Americana
- Punk + Pop → pop-punk
- Soul + Funk → classic Motown, neo-funk
- K-pop + EDM → standard K-pop sound
- K-pop + Rock → K-rock crossover
- Trap + R&B → modern dark R&B

**Difficult Fusion Pairs** (may confuse Suno — use carefully):
- Metal + Bossa Nova — extreme contrast in energy
- Country + Trap — conflicting production aesthetics
- Classical + Punk — opposing philosophies
- Gospel + EDM — competing vocal approaches
- Jazz + Metal — rhythmic/harmonic clash
- Folk + Trap — organic vs. synthetic tension

When fusing difficult pairs, anchor strongly to one genre and use the other as a light accent. For example: "Rock with subtle bossa nova guitar" rather than "Rock bossa nova fusion."

---

## Character Limits & Segment Splitting

Suno's Lyrics field allows up to **5,000 characters** per generation (V5). A typical 3:30 song fits in one generation. Longer or denser songs may need 2 segments.

### How to Split

1. Find a natural section boundary (end of a chorus, before a bridge)
2. End Segment 1 at that boundary
3. Start Segment 2 with `[Continuation]` or context tags — do NOT repeat genre (genre lives in Style Prompt)
4. Include 2-4 lines of overlap (the last lines of Segment 1 repeated at the start of Segment 2) for tonal continuity

### Segment Template

**Segment 1 of 2:**
```
[Intro]
[Electric guitar, building drums]
[Instrumental]

[Verse 1]
[Soft female vocal]
First verse lyrics here...
...

[Chorus]
[Powerful female vocal, full band]
Chorus lyrics here...
```

**Segment 2 of 2:**
```
[Continuation from previous section]

[Chorus]
[Powerful female vocal, full band]
(last 2 lines of chorus from segment 1 for continuity)
Chorus lyrics repeated...

[Bridge]
[Stripped back, intimate]
Bridge lyrics here...

[Final Chorus]
[Key change, explosive, anthemic]
Final chorus lyrics...

[Outro]
[Fade out]
```

---

## Formatting Rules

### Tag Placement
```
[Section tag]
[Style tags, mood tags]
[Instrument tags]
Lyrics go here immediately after tags
More lyrics on the next line
```

### Combining Tags
Multiple tags on one line separated by commas:
```
[Verse 1, soft female vocal, acoustic guitar]
```

Or on separate lines for clarity:
```
[Chorus]
[Powerful female vocal, full band]
[Anthemic, building intensity]
```

Or using pipe stacking:
```
[Chorus | powerful female vocal | full band | anthemic]
```

### Empty Lines
Use empty lines between sections. Do NOT use empty lines between tags and lyrics within a section.

### Line Breaks in Lyrics
Each line of lyrics should be its own line. Suno interprets line breaks as phrasing cues.

---

## Common Pitfalls

- **Parentheses are NOT instructions**: `(instrumental)` gets sung as a backing vocal. Use `[Instrumental]` instead. This is the most common mistake
- **Don't put genre in lyrics**: Genre, BPM, and key belong in the Style Prompt box, not the Lyrics field
- **Don't over-tag**: 2-4 tags per section is ideal. More than that and Suno may ignore some
- **Avoid contradictions**: Don't combine `[Soft]` and `[Aggressive]` in the same section
- **ALL CAPS sparingly**: Only 1-3 words at a time for emphasis. Entire lines in caps produce unpredictable results
- **Repetition**: If you want a line repeated, write it out multiple times — don't use "x2" notation
- **Member names**: Strip all member assignment tags before submitting to Suno. Suno doesn't know who SERENA or KAIA are
- **Pause duration**: Avoid `[Pause X seconds]` or `[Silence Xs]` with specific durations -- Suno treats these as vague suggestions at best. For precise silence, add it in post-production

### Pause & Silence Guide

Suno does not support exact timed pauses. Use these techniques by intent:

| Intent | Tag / Technique | Notes |
|--------|----------------|-------|
| Brief vocal hesitation | `...` (ellipsis in lyrics) | Most reliable micro-pause |
| Structural break (no vocals) | `[Break]` or `[Instrumental Break]` | Clean non-vocal section |
| Dramatic all-instruments-cut | `[Sudden silence]` | Works for tension moments |
| Force near-silence | `[Break: Silence, Acapella, Whispered]` | Community "anti-drop" stack -- stronger than `[Silence]` alone |
| Strip back instrumentation | `[Breakdown]` | Reduces layers, near-quiet feel |
| Abrupt song ending | `[Hard stop]` | Song-ending only |
| Generic pause | `[Pause]` | No duration -- Suno decides length |

**Tip:** Always follow a silence/pause tag with a clear re-entry cue (section tag, instrument tag, or vocal tag) so Suno knows how to resume.

---

## Quick Reference: Tag Cheat Sheet

```
STRUCTURE:   [Intro] [Verse] [Pre-Chorus] [Chorus] [Post-Chorus] [Bridge] [Outro]
             [Break] [Build] [Drop] [Breakdown] [Solo] [Final Chorus] [Beat switch]

VOCAL TYPE:  [Female vocal] [Male vocal] [Duet] [Androgynous vocal]

VOCAL STYLE: [Powerful] [Soft] [Breathy] [Raspy] [Whispered] [Belting] [Falsetto]
             [Crooning] [Operatic] [Growl] [Scream] [Talk-singing] [Spoken word]

VOCAL FX:    [Autotune vocal] [Vocoder] [Distorted vocal] [Filtered vocal]

GROUP:       [Harmonies] [Layered vocals] [Choir] [Call and response] [Group chant]
             [All singers] [Ad-libs] [Vocal runs]

RAP:         [Rap] [Fast rap] [Slow rap] [Aggressive rap] [Melodic rap] [Sing-rap]

INSTRUMENT:  [Piano] [Electric piano] [Organ] [Synth] [Synth pad] [Analog synth]
             [Guitar] [Acoustic guitar] [Distorted guitar] [Guitar solo] [Power chords]
             [Bass groove] [Slap bass] [Bass drop] [808 bass] [808 hi-hats]
             [Strings] [Violin] [Cello] [Harp] [Ukulele] [Banjo]
             [Drums] [Heavy drums] [Drum fill] [Drum machine] [Percussion]
             [Trumpet] [Saxophone] [Brass section] [Flute] [Harmonica]
             [Orchestra] [Orchestral hit] [Timpani] [Glockenspiel] [Music box]

MOOD:        [Energetic] [Melancholic] [Aggressive] [Dreamy] [Dark] [Triumphant]
             [Intimate] [Anthemic] [Euphoric] [Haunting] [Nostalgic] [Playful]
             [Cinematic] [Gritty] [Ethereal] [Serene] [Defiant] [Chaotic]

ENERGY:      [Building intensity] [Sudden silence] [Break] [Explosive] [Tension] [Swagger]

PRODUCTION:  [Stripped back] [Full band] [A cappella] [Instrumental] [Minimalist]
             [Crescendo] [Decrescendo] [Key change] [Tempo change]
             [Fade out] [Hard stop] [Slow build] [Dynamic contrast]

MIX:         [Lo-fi] [Polished production] [Raw recording] [Spacious mix] [Dry mix]

ATMOSPHERE:  [Ambient textures] [Vinyl crackle] [Echo] [Reverb] [Rain sounds]

FORMATTING:  ( ) = backing vocal    - = syllable stretch    ALL CAPS = emphasis (1-3 words)
             ... = pause            [adlib] SOUND = ad-lib

TIME SIG:    3/4  6/8  7/8  swing  shuffle  half-time  double-time
```
