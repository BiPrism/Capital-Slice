# How to Use the Capital Slice Positioning Skill

## Quick Start

1. Open a terminal in the project folder
2. Start Claude Code:
   ```bash
   claude
   ```
3. Run the skill:
   ```
   /capital-slice-positioning Saturday, December 27, 2025
   ```
   Or simply ask:
   ```
   Generate a positioning memo for this Saturday
   ```

---

## What This Skill Does

Generates weekly truck positioning recommendations for Capital Slice food trucks in Washington DC by:

- Checking holiday status and applying modifiers
- Analyzing weather forecasts (morning vs afternoon)
- Checking sports schedules (Wizards, Capitals, Nationals, Mystics, DC United)
- Identifying events (conventions, festivals, markets)
- Scoring all 10 permitted locations
- Applying customer fit considerations
- Recommending morning and afternoon positions for both trucks
- Producing a decision memo with risk assessment and backup plans

---

## Example Prompts

| What You Want | What to Ask |
|---------------|-------------|
| Weekly memo | "Generate a positioning memo for Saturday December 27th" |
| Run the skill | "/capital-slice-positioning this Saturday" |
| Quick recommendation | "Where should we position the trucks this Saturday?" |
| Weather scenario | "What's our strategy if it's raining on Saturday?" |
| Event-based | "There's a Wizards game Saturday at 7pm - what's the plan?" |
| Compare options | "Should we go to Navy Yard or the Arena this Saturday?" |
| Holiday planning | "Generate positioning for July 4th weekend" |

---

## Skill Files

```
.claude\skills\capital-slice-positioning\
├── SKILL.md                        # Main skill definition (invoked by Claude)
├── scoring-algorithm.md            # Scoring logic, modifiers, formulas
├── location-scoring-reference.md   # 10 DC location profiles + Customer Fit
├── data-gathering-guide.md         # Data sources, holiday awareness, review template
├── product-testing-framework.md    # A/B testing for slice size, pricing, margins
├── HOW-TO-USE.md                   # This file
└── templates\
    └── decision-memo-template.md   # Memo format reference
```

### File Descriptions

| File | Purpose | When to Read |
|------|---------|--------------|
| `SKILL.md` | Core skill instructions for Claude | To understand what the skill does |
| `scoring-algorithm.md` | How scores are calculated (base + modifiers) | To understand or adjust scoring logic |
| `location-scoring-reference.md` | Profiles for all 10 locations + customer demographics | To understand location strengths |
| `data-gathering-guide.md` | Where to get weather, sports, events data | When troubleshooting data issues |
| `product-testing-framework.md` | How to run A/B tests on slice size, pricing | When optimizing products/margins |

---

## Weekly Workflow

### Thursday by 6 PM ET

1. Open Claude Code in the project folder
2. Run: `/capital-slice-positioning [Saturday date]`
3. Claude will:
   - Check holiday status
   - Search for weather forecasts
   - Check sports schedules
   - Look up DC events
   - Score all locations with modifiers
   - Generate the decision memo
4. Review memo in `memos/positioning-memo-YYYY-MM-DD.md`
5. Send to Raven and Brian

### Saturday

1. Run trucks at recommended locations
2. Collect revenue and observations data

### Monday

1. Complete the Post-Saturday Review in `memos/reviews/`
2. Compare predicted scores to actual $/hr
3. Note any scoring adjustments needed

---

## Key Features

### Holiday Awareness
The skill automatically applies modifiers for:
- Christmas week (-20 to most locations)
- July 4th (+50 to National Mall)
- Summer holiday weekends (+10 to tourist locations)
- New Year's, Memorial Day, Labor Day, etc.

### Time-Split Weather
Morning and afternoon weather are scored separately. A rainy morning that clears up means:
- Morning outdoor locations score poorly
- Afternoon outdoor locations score well

### Customer Fit Profiles
Each location includes demographic guidance:
- Primary demographic (who's there)
- Pizza fit (HIGH/MEDIUM/LOW)
- Price sensitivity
- Recommended positioning (quality vs speed vs value)

### Post-Saturday Review
Built-in feedback loop to calibrate scores:
- Compare predicted scores to actual revenue
- Track patterns over 4-8 weeks
- Adjust base scores based on real data

### Product Testing Framework
A/B test product variables:
- Slice size (standard vs large)
- Pricing ($4 vs $5 vs $6)
- Combos (slice + drink deals)
- Track margin impact

---

## The 10 Locations

| # | Location | Best For | Customer Fit |
|---|----------|----------|--------------|
| 1 | Eastern Market | Morning (market crowds) | Affluent foodies |
| 2 | Dupont Circle | Morning-Afternoon (steady) | Urban professionals |
| 3 | National Mall | Good weather afternoons | Tourists, families |
| 4 | Georgetown Waterfront | Good weather afternoons | Upscale leisure |
| 5 | U Street Corridor | Evenings (concerts) | Nightlife/music crowd |
| 6 | Convention Center | Convention days only | Business travelers |
| 7 | Capital One Arena | Game days only | Sports fans |
| 8 | Columbia Heights | Backup (low risk) | Neighborhood families |
| 9 | H Street Corridor | Festival days | Arts/culture crowd |
| 10 | Navy Yard / Wharf | Nationals game days | Baseball fans |

---

## Output Files

The skill generates files in the `memos/` folder:

```
memos/
├── positioning-memo-YYYY-MM-DD.md      # Weekly recommendations
├── positioning-memo-YYYY-MM-DD-v2.md   # Revised versions if needed
└── reviews/
    └── review-YYYY-MM-DD.md            # Post-Saturday feedback
```

---

## Customization

### Adjust Base Scores
Edit `scoring-algorithm.md` → Step 1: Base Scores table

### Add New Modifiers
Edit `scoring-algorithm.md` → Add new Step (e.g., Step 4c)

### Update Location Profiles
Edit `location-scoring-reference.md` → Detailed Location Profiles section

### Change Data Sources
Edit `data-gathering-guide.md` → Quick Reference tables

---

## Troubleshooting

**Skill not activating?**
- Make sure you're in the correct project folder
- Check that `.claude\skills\capital-slice-positioning\SKILL.md` exists
- Try running `/capital-slice-positioning` explicitly

**Data seems wrong?**
- Check `data-gathering-guide.md` for correct URLs
- Verify season awareness (no MLB Nov-Mar, etc.)
- Confirm home vs away for sports games

**Scores don't match expectations?**
- Review modifiers in `scoring-algorithm.md`
- Check if holiday modifier is being applied
- Use Post-Saturday Review to calibrate

**Want to see the scoring math?**
- Read `scoring-algorithm.md` for full calculation details
- Check the worked example in Step 7

---

## Installation

### Option A: Project-Specific
Copy `.claude\skills\capital-slice-positioning\` folder into any project's `.claude\skills\` directory.

### Option B: Global (All Projects)
Copy the folder to your user-level skills directory:
```
~/.claude/skills/capital-slice-positioning/
```
The skill will then be available in any project.

---

## Support & Resources

- **Project repo:** https://github.com/BiPrism/Capital-Slice
- **Brian Julius LinkedIn:** Weekly build-along updates
- **Progress tracking:** See `WEEK2-PROGRESS.md` in project root

---

*Last updated: December 24, 2025*
