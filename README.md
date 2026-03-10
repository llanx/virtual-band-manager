# Virtual Band Manager -- Claude Code Skill

A Claude Code skill that manages a virtual band -- handling member personas, genre negotiation, and a 5-phase song construction pipeline that outputs Suno-ready song scripts with square-bracket stage directions.

## Installation

Clone this repo and link it to your project's skill directory:

```bash
# Clone
git clone https://github.com/YOUR_USERNAME/virtual-band-manager.git

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
- "Band overview"
- "Build a track"

### Three Modes

1. **Song Session** -- 5-phase pipeline: Concept > Structure > Lyrics > Suno Tags > Assembly
2. **Member Management** -- Create, edit, or view band member profiles
3. **Band Overview** -- View full roster with personalities and group dynamics

## File Structure

```
virtual-band-manager/
├── SKILL.md                     # Main skill definition
├── references/
│   ├── persona-schema.md        # Member profile JSON schema
│   ├── genre-matrix.md          # Genre compatibility & blending rules
│   ├── kpop-structures.md       # Song structure templates
│   └── suno-tag-reference.md    # Suno bracket notation guide
├── templates/
│   ├── blank-member.json        # Empty persona template
│   ├── song-concept-brief.md    # Phase 1 output template
│   └── song-output.md          # Phase 5 assembly template
└── bands/
    └── placeholderbandname.json # Default band profile
```

## Song Construction Pipeline

1. **Concept** -- Gather intent, run genre negotiation, members pitch in-character
2. **Structure** -- Select song structure template, assign members to sections
3. **Lyrics** -- Write in each member's voice using their persona-defined style
4. **Suno Tags** -- Convert to bracket notation for Suno's custom lyrics field
5. **Assembly** -- Compile final output, split into segments if needed

## License

MIT
