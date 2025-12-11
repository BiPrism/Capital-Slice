# How to Use the Capital Slice Positioning Skill

## Quick Start

1. Open a terminal
2. Navigate to the project folder:
   ```bash
   cd "C:\Users\danie\OneDrive\Personal Development\Training\Brian Julius AI Claude"
   ```
3. Start Claude Code:
   ```bash
   claude
   ```
4. Ask for a positioning recommendation:
   ```
   Generate a positioning memo for this Saturday
   ```

---

## What This Skill Does

Generates weekly truck positioning recommendations for Capital Slice food trucks in Washington DC by:

- Analyzing weather forecasts
- Checking sports schedules (Nationals, Wizards, Capitals, Mystics)
- Identifying events (conventions, festivals, markets)
- Scoring all 10 permitted locations
- Recommending morning and afternoon positions for both trucks
- Producing a 2-page decision memo

---

## Example Prompts

| What You Want | What to Ask |
|---------------|-------------|
| Weekly memo | "Generate a positioning memo for Saturday December 20th" |
| Quick recommendation | "Where should we position the trucks this Saturday?" |
| Weather scenario | "What's our strategy if it's raining on Saturday?" |
| Event-based | "There's a Wizards game Saturday at 7pm - what's the plan?" |
| Compare options | "Should we go to Navy Yard or the Arena this Saturday?" |

---

## Skill Location

The skill files are stored at:

```
.claude\skills\capital-slice-positioning\
├── SKILL.md                      # Main skill definition
├── location-scoring-reference.md # 10 DC location profiles
├── scoring-algorithm.md          # Scoring logic
├── data-gathering-guide.md       # How to collect weekly data
├── templates\
│   └── decision-memo-template.md # Memo format
└── HOW-TO-USE.md                 # This file
```

---

## Using the Skill Elsewhere

### Option A: Project-Specific
Copy the `.claude\skills\capital-slice-positioning\` folder into any project's `.claude\skills\` directory.

### Option B: Global (All Projects)
Copy the folder to your user directory:
```
C:\Users\danie\.claude\skills\capital-slice-positioning\
```
The skill will then be available in any project.

---

## Weekly Workflow

**Every Thursday by 6 PM:**

1. Open Claude Code in this folder
2. Ask: "Generate a positioning memo for this Saturday"
3. Claude will:
   - Search for weather forecasts
   - Check sports schedules
   - Look up DC events
   - Score all locations
   - Generate the 2-page memo
4. Review and send to Raven and Brian

---

## The 10 Locations

| # | Location | Best For |
|---|----------|----------|
| 1 | Eastern Market | Morning (market crowds) |
| 2 | Dupont Circle | Morning-Afternoon (steady traffic) |
| 3 | National Mall | Good weather afternoons (tourists) |
| 4 | Georgetown Waterfront | Good weather afternoons (upscale) |
| 5 | U Street Corridor | Evenings (concerts/nightlife) |
| 6 | Convention Center | Convention days only |
| 7 | Capital One Arena | Game days only |
| 8 | Columbia Heights | Backup (low risk) |
| 9 | H Street Corridor | Festival days |
| 10 | Navy Yard / Wharf | Nationals game days |

---

## Troubleshooting

**Skill not activating?**
- Make sure you're in the correct project folder
- Check that `.claude\skills\capital-slice-positioning\SKILL.md` exists

**Need to update the skill?**
- Edit files in `.claude\skills\capital-slice-positioning\`
- Commit changes: `git add . && git commit -m "Update skill" && git push`

**Want to see the scoring math?**
- Read `scoring-algorithm.md` for the full calculation details

---

## Support

- Project repo: https://github.com/BiPrism/Capital-Slice
- Brian Julius LinkedIn series for weekly updates
