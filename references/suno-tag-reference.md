# Suno Bracket Notation Reference

Complete guide to Suno's square-bracket tag system for the Custom Lyrics input field.

## How Tags Work

Tags are placed on their own line, wrapped in square brackets `[]`, before the lyrics they describe. Multiple tags can be on the same line or separate lines. Tags influence Suno's AI generation for the section that follows.

```
[Verse 1]
[Soft female vocal, acoustic guitar]
I remember when the lights went low
And every word felt like a prayer
```

---

## Tag Categories

### 1. Structural Tags (Section Markers)

These define song structure. Place at the start of each section.

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

### 2. Genre Tags

Place at the very start of the song (first line) to set overall style. Can also be placed mid-song for genre shifts.

**Effective genre tags:**
- `[K-pop]`, `[Pop]`, `[Rock]`, `[Indie Rock]`, `[Alternative]`
- `[R&B]`, `[Soul]`, `[Neo-Soul]`, `[Funk]`
- `[Hip-Hop]`, `[Trap]`, `[EDM]`, `[House]`, `[Dance Pop]`
- `[Ballad]`, `[Power Ballad]`, `[Acoustic]`
- `[Punk Rock]`, `[Pop-Punk]`, `[Grunge]`
- `[Jazz]`, `[Lo-fi]`, `[Synthwave]`

**Combining genres:** `[K-pop, Rock, R&B fusion]` or `[Alt-pop with rock edge]`

### 3. Vocal Style Tags

Describe how the vocals should sound for the following section.

| Tag | Effect |
|-----|--------|
| `[Female vocal]` | General female voice |
| `[Powerful female vocal]` | Strong, belting delivery |
| `[Soft female vocal]` | Gentle, intimate delivery |
| `[Breathy vocal]` | Airy, intimate quality |
| `[Raspy vocal]` | Rough, textured voice |
| `[Whispered]` | Very soft, close-mic feel |
| `[Belting]` | Full-power sustained notes |
| `[Falsetto]` | High, airy register |
| `[Harmonies]` or `[Layered vocals]` | Multiple vocal layers |
| `[Rap]` or `[Fast rap]` | Rhythmic spoken delivery |
| `[Sing-rap]` | Melodic rap style |
| `[Spoken word]` | Non-melodic delivery |
| `[Chanting]` | Rhythmic group chant |
| `[Call and response]` | Back-and-forth vocal pattern |
| `[Ad-libs]` | Improvised vocal additions |
| `[Vocal runs]` | Melismatic embellishments |

### 4. Instrument Tags

Specify instrumental elements for a section.

| Tag | Effect |
|-----|--------|
| `[Electric guitar]` or `[Guitar riff]` | Prominent guitar |
| `[Acoustic guitar]` | Clean acoustic |
| `[Guitar solo]` | Extended guitar lead |
| `[Bass groove]` or `[Bass line]` | Prominent bass |
| `[Bass drop]` | Heavy low-end hit |
| `[Drums]` or `[Heavy drums]` | Drum emphasis |
| `[Drum fill]` | Transitional drum pattern |
| `[Piano]` or `[Grand piano]` | Piano accompaniment |
| `[Synth]` or `[Synth lead]` | Synthesizer prominence |
| `[Synth drop]` | Electronic drop moment |
| `[Strings]` or `[Orchestral strings]` | String arrangement |
| `[808 bass]` | Trap-style sub bass |
| `[Beat switch]` | Rhythm/tempo change |

### 5. Mood & Energy Tags

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

### 6. Production Tags

Control production and arrangement elements.

| Tag | Effect |
|-----|--------|
| `[Stripped back]` | Minimal instrumentation |
| `[Full band]` | All instruments playing |
| `[A cappella]` | Vocals only |
| `[Crescendo]` | Building to peak |
| `[Decrescendo]` | Fading down |
| `[Tempo change]` | Shift in speed |
| `[Key change]` | Modulation (usually up for final chorus) |
| `[Fade out]` | Gradual volume decrease |
| `[Hard stop]` | Abrupt ending |

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

### Empty Lines
Use empty lines between sections. Do NOT use empty lines between tags and lyrics within a section.

### Line Breaks in Lyrics
Each line of lyrics should be its own line. Suno interprets line breaks as phrasing cues.

---

## Character Limits & Segment Splitting

Suno's custom lyrics field has a limit of approximately **3000 characters** per generation. A typical 3:30 song may need 2 segments.

### How to Split

1. Find a natural section boundary (end of a chorus, before a bridge)
2. End Segment 1 at that boundary
3. Start Segment 2 with the genre tag again, plus `[Continuation]` or context tags
4. Include 2-4 lines of overlap (the last lines of Segment 1 repeated at the start of Segment 2) for tonal continuity

### Segment Template

**Segment 1 of 2:**
```
[K-pop, Alt-pop, Rock, Female vocals]

[Intro]
[Electric guitar, building drums]
(instrumental)

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
[K-pop, Alt-pop, Rock, Female vocals]
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

## Common Pitfalls

- **Don't over-tag**: 2-4 tags per section is ideal. More than that and Suno may ignore some
- **Genre tag first**: Always put the genre tag as the very first line of the entire script
- **Avoid contradictions**: Don't combine `[Soft]` and `[Aggressive]` in the same section
- **Instrumental sections**: Use `(instrumental)` or `(guitar solo)` in parentheses as placeholder lyrics for non-vocal sections
- **Parenthetical directions**: Use `(whispered)` or `(building)` inline within lyrics for micro-directions
- **Repetition**: If you want a line repeated, write it out multiple times -- don't use "x2" notation
- **Member names**: Strip all member assignment tags before submitting to Suno. Suno doesn't know who SERENA or KAIA are

---

## Quick Reference: Tag Cheat Sheet

```
STRUCTURE:  [Intro] [Verse] [Pre-Chorus] [Chorus] [Bridge] [Outro] [Break] [Rap]
VOCAL:      [Powerful] [Soft] [Breathy] [Raspy] [Whispered] [Belting] [Harmonies] [Rap]
INSTRUMENT: [Guitar] [Bass] [Drums] [Piano] [Synth] [Strings] [808] [Beat switch]
MOOD:       [Energetic] [Melancholic] [Aggressive] [Dreamy] [Dark] [Triumphant] [Anthemic]
PRODUCTION: [Stripped back] [Full band] [A cappella] [Crescendo] [Key change] [Fade out]
```
