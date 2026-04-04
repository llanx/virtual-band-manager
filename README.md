# Virtual Band Manager -- Claude Code Skill

A Claude Code skill that manages virtual bands across multiple universes -- handling member personas, genre negotiation, and a 5-phase song construction pipeline that outputs Suno-ready song scripts with square-bracket stage directions. Create your own bands, characters, and worlds, or use the default band to get started.

## Installation

Clone this repo and link it to your project's skill directory:

```bash
# Clone
git clone https://github.com/llanx/virtual-band-manager.git

# Link to your project (Windows junction)
mklink /J "C:\path\to\your-project\.claude\skills\virtual-band-manager" "C:\path\to\virtual-band-manager"

# Link to your project (macOS/Linux symlink)
ln -s /path/to/virtual-band-manager /path/to/your-project/.claude/skills/virtual-band-manager
```

Or install globally for all projects:

```bash
# Copy or symlink to global skills directory
ln -s /path/to/virtual-band-manager ~/.claude/skills/virtual-band-manager
```

## Usage

Invoke with `/virtual-band-manager` or trigger naturally with phrases like:
- "Write a song"
- "Band session"
- "Create a band member"
- "Create a band" / "Create a universe"
- "Switch universe" / "Switch band"
- "Band overview"
- "Clean slate" / "Start fresh"

### Modes

1. **Song Session** -- 5-phase pipeline: Concept > Structure > Lyrics > Suno Tags > Assembly
2. **Member Management** -- Create, edit, or remove band member profiles
3. **Band Overview** -- View full roster with personalities and group dynamics
4. **Band Management** -- Create, delete, switch, or list bands within a universe
5. **Universe Management** -- Create, delete, or switch between isolated universes

### Multi-Universe System

Each universe is fully isolated with its own bands, lore, songs, and pattern tracking. This means you can:
- Run multiple bands in separate fictional worlds without cross-contamination
- Delete all existing content and start fresh with your own characters ("clean slate")
- Share the skill with others who can create their own universes independently

The skill tracks which universe and band you're working in via `active-context.json`, so it picks up where you left off between sessions.

## File Structure

```
virtual-band-manager/
├── SKILL.md                              # Main skill definition
├── active-context.json                   # Tracks active universe + band
├── references/                           # Shared (universal) references
│   ├── persona-schema.md                 # Member profile JSON schema
│   ├── genre-matrix.md                   # Genre compatibility & blending rules
│   ├── kpop-structures.md                # Song structure templates
│   └── suno-tag-reference.md             # Suno bracket notation guide
├── templates/                            # Shared templates
│   ├── blank-member.json                 # Empty member persona template
│   ├── blank-band.json                   # Empty band template
│   ├── blank-universe.json               # Empty universe template
│   ├── blank-song-dna-registry.md        # Empty DNA registry for new universes
│   ├── song-concept-brief.md             # Phase 1 output template
│   └── song-output.md                    # Phase 5 assembly template
└── universes/                            # All universe-specific content
    └── {universe-slug}/
        ├── universe.json                 # Universe metadata
        ├── bands/
        │   └── {band-slug}.json          # Band profiles
        ├── lore/                          # Universe-specific story files
        ├── songs/
        │   └── {band-slug}/              # Songs per band
        └── song-dna-registry.md          # Per-universe pattern tracking
```

## Song Construction Pipeline

1. **Concept** -- Gather intent, run genre negotiation, members pitch in-character
2. **Structure** -- Select song structure template, assign members to sections
3. **Lyrics** -- Write in each member's voice using their persona-defined style
4. **Suno Tags** -- Convert to bracket notation for Suno's custom lyrics field
5. **Assembly** -- Compile final output, split into segments if needed

### Bilingual Lyrics

Bilingual lyric support is opt-in per band via the `lyricLanguageConfig` field. Configure a primary and secondary language with a target ratio, and the skill handles placement rules and rhyme constraints automatically. Bands without this config write monolingual lyrics.

## Default Band

The repo ships with a default 4-member band in the "Cosmic Battle" universe. You can use them as-is, modify them, or archive them and start from scratch with your own characters.

## License

MIT
