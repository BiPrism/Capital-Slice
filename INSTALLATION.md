# Capital Slice Positioning Skill - Installation Guide

## Prerequisites

- **Claude Code CLI** installed and configured
- **Git** (optional, for cloning)
- **Internet access** (skill fetches live weather/event data)

---

## Quick Install

### Option 1: Clone from GitHub

```bash
# Navigate to your Claude skills directory
cd ~/.claude/skills

# Clone the skill
git clone https://github.com/BiPrism/Capital-Slice.git capital-slice-positioning

# Or for project-specific installation:
cd your-project/.claude/skills
git clone https://github.com/BiPrism/Capital-Slice.git capital-slice-positioning
```

### Option 2: Download ZIP

1. Go to https://github.com/BiPrism/Capital-Slice
2. Click **Code** → **Download ZIP**
3. Extract to `~/.claude/skills/capital-slice-positioning/` (global) or `.claude/skills/capital-slice-positioning/` (project)

### Option 3: Manual Copy

Copy these files to your skills directory:

```
capital-slice-positioning/
├── SKILL.md                        # Required - entry point
├── scoring-algorithm.md            # Required - scoring logic
├── location-scoring-reference.md   # Required - location profiles
├── data-gathering-guide.md         # Required - data sources
├── product-testing-framework.md    # Optional - A/B testing
├── HOW-TO-USE.md                   # Optional - user guide
└── templates/
    └── decision-memo-template.md   # Optional - memo format
```

---

## Installation Locations

| Location | Path | When to Use |
|----------|------|-------------|
| **Global** | `~/.claude/skills/capital-slice-positioning/` | Available in all projects |
| **Project** | `your-project/.claude/skills/capital-slice-positioning/` | Single project only |

### Windows Paths

- Global: `C:\Users\<username>\.claude\skills\capital-slice-positioning\`
- Project: `C:\path\to\project\.claude\skills\capital-slice-positioning\`

### macOS/Linux Paths

- Global: `~/.claude/skills/capital-slice-positioning/`
- Project: `~/projects/your-project/.claude/skills/capital-slice-positioning/`

---

## Verify Installation

1. Open a terminal in your project folder (or any folder for global install)

2. Start Claude Code:
   ```bash
   claude
   ```

3. Test the skill:
   ```
   /capital-slice-positioning Saturday, January 4, 2025
   ```

4. Claude should:
   - Read the skill files
   - Search for weather forecasts
   - Check sports schedules
   - Generate a positioning memo

---

## Required Files

These files must be present for the skill to work:

| File | Purpose | Required |
|------|---------|----------|
| `SKILL.md` | Entry point - Claude reads this first | Yes |
| `scoring-algorithm.md` | Scoring logic and formulas | Yes |
| `location-scoring-reference.md` | 10 DC location profiles | Yes |
| `data-gathering-guide.md` | Data sources and procedures | Yes |
| `product-testing-framework.md` | A/B testing guide | No |
| `HOW-TO-USE.md` | User documentation | No |
| `templates/decision-memo-template.md` | Memo format reference | No |

---

## Output Directory Setup

The skill generates memos in a `memos/` folder. Create it if it doesn't exist:

```bash
mkdir -p memos/reviews
```

Output structure:
```
memos/
├── positioning-memo-YYYY-MM-DD.md      # Weekly recommendations
└── reviews/
    └── review-YYYY-MM-DD.md            # Post-Saturday feedback
```

---

## Customization

### Adjust for Your Business

1. **Edit locations**: Update `location-scoring-reference.md` with your permitted locations
2. **Adjust scores**: Modify base scores in `scoring-algorithm.md`
3. **Change data sources**: Update URLs in `data-gathering-guide.md`

### Rename the Skill

1. Rename the folder (e.g., `my-food-truck-optimizer`)
2. Update references in `SKILL.md`
3. Invoke with new name: `/my-food-truck-optimizer`

---

## Troubleshooting

### Skill Not Recognized

- Verify `SKILL.md` exists in the skill folder
- Check folder is in correct location (`.claude/skills/`)
- Restart Claude Code

### No Weather Data

- Check internet connection
- Skill will use fallback sources automatically
- If all sources fail, memo will note data limitations

### Wrong Date Calculated

- Specify explicit date: `/capital-slice-positioning January 4, 2025`
- Avoid relative dates like "this Saturday"

### Permission Errors

- Ensure write access to `memos/` directory
- On Windows, run terminal as administrator if needed

---

## Updates

### Check for Updates

```bash
cd ~/.claude/skills/capital-slice-positioning
git pull
```

### Manual Update

1. Download latest files from GitHub
2. Replace existing files in skill directory
3. Review CHANGELOG for breaking changes

---

## Uninstall

Simply delete the skill folder:

```bash
# Global
rm -rf ~/.claude/skills/capital-slice-positioning

# Project
rm -rf .claude/skills/capital-slice-positioning
```

---

## Support

- **Repository:** https://github.com/BiPrism/Capital-Slice
- **Issues:** https://github.com/BiPrism/Capital-Slice/issues
- **Documentation:** See `HOW-TO-USE.md` and `SKILL-DOCUMENTATION.md`

---

*Version 1.0.0 - December 2025*
