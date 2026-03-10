# Genre Compatibility & Blending Reference

## Genre Compatibility Matrix

Scores from 1 (clashing) to 5 (natural blend). Only upper triangle shown; the matrix is symmetric.

| | pop | rock | indie | alt | punk | metal | rnb | soul | funk | edm | hiphop | trap | jazz |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| **pop** | - | 3 | 4 | 3 | 2 | 1 | 4 | 3 | 3 | 5 | 3 | 3 | 2 |
| **rock** | | - | 5 | 5 | 5 | 4 | 2 | 2 | 3 | 2 | 2 | 2 | 3 |
| **indie** | | | - | 5 | 4 | 2 | 3 | 3 | 3 | 3 | 2 | 2 | 4 |
| **alt** | | | | - | 4 | 3 | 3 | 3 | 3 | 3 | 3 | 3 | 3 |
| **punk** | | | | | - | 4 | 1 | 1 | 2 | 2 | 2 | 2 | 2 |
| **metal** | | | | | | - | 1 | 1 | 2 | 2 | 2 | 2 | 2 |
| **rnb** | | | | | | | - | 5 | 5 | 3 | 4 | 4 | 4 |
| **soul** | | | | | | | | - | 5 | 2 | 3 | 2 | 5 |
| **funk** | | | | | | | | | - | 3 | 3 | 3 | 4 |
| **edm** | | | | | | | | | | - | 4 | 5 | 2 |
| **hiphop** | | | | | | | | | | | - | 5 | 3 |
| **trap** | | | | | | | | | | | | - | 2 |
| **jazz** | | | | | | | | | | | | | - |

### High-Compatibility Pairs (4-5)
- pop + edm, pop + rnb, pop + indie
- rock + indie, rock + alt, rock + punk, rock + metal
- indie + alt, indie + jazz
- rnb + soul, rnb + funk, rnb + hiphop, rnb + trap
- soul + funk, soul + jazz
- edm + trap, edm + hiphop
- hiphop + trap

### Low-Compatibility Pairs (1-2)
- punk + rnb, punk + soul
- metal + rnb, metal + soul, metal + pop
- jazz + trap, jazz + edm

---

## Genre Blending Algorithm

### Step 1: Collect Preferences

For each featured member, collect their `genrePreferences` object.

### Step 2: Weight by Assertiveness

Multiply each member's genre scores by their assertiveness modifier:

```
modifier = 0.5 + (assertiveness * 0.2)
```

| Assertiveness | Modifier | Effect |
|---------------|----------|--------|
| 1 | 0.7 | Preferences count 70% |
| 2 | 0.9 | Preferences count 90% |
| 3 | 1.1 | Preferences count 110% |
| 4 | 1.3 | Preferences count 130% |
| 5 | 1.5 | Preferences count 150% |

### Step 3: Sum Weighted Scores

For each genre, sum the weighted scores across all featured members. Normalize to get a percentage.

### Step 4: Apply Compatibility Check

Take the top 3 genres by weighted score. Check pairwise compatibility from the matrix above:
- If compatibility >= 4: blend freely
- If compatibility == 3: blend works but note the tension (can be creative)
- If compatibility <= 2: flag as potential clash, suggest alternatives or lean into it as intentional contrast

### Step 5: Produce Output

- **Primary genre**: Highest weighted score
- **Secondary influence**: Second highest (if compatibility >= 3 with primary)
- **Accent**: Third highest (if compatibility >= 3 with primary, optional)

Format: "Primary / Secondary with Accent touches" -- e.g., "Alt-pop / Rock with R&B touches"

---

## Fusion Genre Suggestions

When two genres with moderate compatibility (3) blend, suggest a fusion name:

| Genre A | Genre B | Fusion Name |
|---------|---------|-------------|
| pop | rock | pop-rock, power pop |
| rock | rnb | alt-R&B with guitar |
| indie | edm | indie-electronic, synth-pop |
| pop | hiphop | pop-rap |
| rock | edm | electronic rock, cyberpunk |
| rnb | rock | alternative R&B |
| soul | edm | future soul |
| funk | edm | electro-funk |
| indie | hiphop | art-rap, alt-hip-hop |
| pop | soul | pop-soul |
| rock | funk | funk-rock |
| jazz | hiphop | jazz-rap |

---

## Example Negotiations

### Example 1: Full Band (Serena + Kaia + Mika + Evie)

**Weighted scores (top genres):**
- pop: Serena(5*1.3) + Kaia(3*1.3) + Mika(4*1.1) + Evie(3*0.9) = 6.5 + 3.9 + 4.4 + 2.7 = 17.5
- rock: Serena(3*1.3) + Kaia(5*1.3) + Mika(3*1.1) + Evie(0) = 3.9 + 6.5 + 3.3 = 13.7
- rnb: Serena(4*1.3) + Kaia(0) + Mika(3*1.1) + Evie(5*0.9) = 5.2 + 3.3 + 4.5 = 13.0
- indie: Serena(3*1.3) + Kaia(5*1.3) + Mika(0) + Evie(3*0.9) = 3.9 + 6.5 + 2.7 = 13.1

**Result:** Primary: pop | Secondary: rock | Accent: R&B
**Genre label:** "Alt-pop / Rock with R&B soul"

### Example 2: Kaia + Evie Duet

**Weighted scores (top genres):**
- rock: Kaia(5*1.3) = 6.5
- rnb: Evie(5*0.9) = 4.5
- indie: Kaia(5*1.3) = 6.5
- soul: Evie(5*0.9) = 4.5

**Compatibility check:** rock + rnb = 2 (clash!), indie + rnb = 3 (workable)
**Result:** Primary: indie | Secondary: R&B | Creative tension from rock edge
**Genre label:** "Indie R&B with guitar edge"

### Example 3: Serena + Mika Duet

**Weighted scores:**
- pop: Serena(5*1.3) + Mika(4*1.1) = 6.5 + 4.4 = 10.9
- rnb: Serena(4*1.3) + Mika(3*1.1) = 5.2 + 3.3 = 8.5
- edm: Mika(4*1.1) + Serena(2*1.3) = 4.4 + 2.6 = 7.0

**Compatibility:** pop + rnb = 4, pop + edm = 5
**Result:** Primary: pop | Secondary: R&B | Accent: EDM
**Genre label:** "Pop / R&B with electronic production"
