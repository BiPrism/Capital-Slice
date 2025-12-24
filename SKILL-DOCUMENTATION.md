# Capital Slice Positioning Skill - Technical Documentation

**Version:** 1.0
**Last Updated:** December 24, 2025
**Status:** Production Ready (pending real-world validation)

---

## Overview

The Capital Slice Positioning Skill is a Claude Code skill that generates weekly truck positioning recommendations for a two-truck food operation in Washington DC. It analyzes weather, events, holidays, and location characteristics to optimize Saturday revenue.

---

## Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         USER REQUEST                             │
│            "Generate positioning for this Saturday"              │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                          SKILL.md                                │
│                   (Entry point - Claude reads this)              │
└─────────────────────────────────────────────────────────────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          ▼                     ▼                     ▼
┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
│ data-gathering-  │  │ scoring-         │  │ location-scoring-│
│ guide.md         │  │ algorithm.md     │  │ reference.md     │
│                  │  │                  │  │                  │
│ • Data sources   │  │ • Base scores    │  │ • 10 locations   │
│ • Holiday check  │  │ • Weather mods   │  │ • Customer fit   │
│ • Season aware   │  │ • Event mods     │  │ • Strategic notes│
│ • Review template│  │ • Holiday mods   │  │                  │
└──────────────────┘  └──────────────────┘  └──────────────────┘
          │                     │                     │
          └─────────────────────┼─────────────────────┘
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                    WEB DATA COLLECTION                           │
│     Weather (NWS, AccuWeather) + Sports (ESPN) + Events (DC.gov) │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                     SCORING CALCULATION                          │
│   Score = Base + Holiday + Weather + Event + Competition         │
└─────────────────────────────────────────────────────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────┐
│                      OUTPUT: DECISION MEMO                       │
│                 memos/positioning-memo-YYYY-MM-DD.md             │
└─────────────────────────────────────────────────────────────────┘
```

---

## File Reference

### Core Skill Files

| File | Size | Purpose | Key Sections |
|------|------|---------|--------------|
| `SKILL.md` | 8.5KB | Entry point - Claude reads this when skill is invoked | Overview, locations table, scoring algorithm, output format |
| `scoring-algorithm.md` | 11.5KB | Complete scoring logic | Base scores, weather/event/holiday/competition modifiers, worked example |
| `location-scoring-reference.md` | 15KB | Detailed location profiles | 10 location profiles, customer fit, quick reference matrices |
| `data-gathering-guide.md` | 21.4KB | Data sources and procedures | Holiday awareness, weather sources, sports schedules, review template |
| `product-testing-framework.md` | 11.1KB | A/B testing guide | Conversion rates, test design, margin calculations |
| `HOW-TO-USE.md` | 3.6KB | User guide | Quick start, examples, troubleshooting |

### Supporting Files

| File | Location | Purpose |
|------|----------|---------|
| `decision-memo-template.md` | `templates/` | Format reference for memo output |
| `WEEK2-PROGRESS.md` | Project root | Development progress tracking |
| `Capital Slice Site Analysis.md` | Project root | Original location analysis (Brian's input) |
| `Capital-Slice-business-challenge-briefing.md` | Project root | Full business context |

### Output Files

| File | Location | Generated When |
|------|----------|----------------|
| `positioning-memo-YYYY-MM-DD.md` | `memos/` | Each Thursday when skill runs |
| `review-YYYY-MM-DD.md` | `memos/reviews/` | Each Monday after Saturday operations |

---

## Scoring System

### Formula

```
Score = Base Score + Holiday Modifier + Weather Modifier + Event Modifier + Competition Modifier
```

### Base Scores (from star ratings)

| Stars | Score Range | Example |
|-------|-------------|---------|
| ★★★★★ | 85 | Eastern Market morning |
| ★★★★ | 70-85 | Georgetown afternoon |
| ★★★ | 50-65 | Columbia Heights |
| ★★ | 20-30 | U Street morning |
| ★ | 10 | Arena without event |

### Modifier Ranges

| Modifier Type | Range | Biggest Impact |
|---------------|-------|----------------|
| Holiday | -50 to +50 | Christmas Day (-50), July 4th (+50 Mall) |
| Weather | -50 to +25 | Rain on outdoor locations |
| Event | +30 to +70 | Wizards/Capitals game (+60) |
| Competition | -15 to 0 | Direct competitor present |

---

## Key Features

### 1. Holiday Awareness
- Automatically detects major holidays
- Applies appropriate modifiers
- Warns about Eastern Market closures
- See: `data-gathering-guide.md` → Holiday Awareness section

### 2. Time-Split Weather
- Separate morning vs afternoon calculations
- Outdoor locations penalized for morning rain even if afternoon clears
- See: `scoring-algorithm.md` → Time-Split Weather section

### 3. Season Awareness
- Skips MLB checks November-March
- Skips WNBA checks October-April
- Prevents false "no game" penalties
- See: `data-gathering-guide.md` → Season Awareness table

### 4. Customer Fit Profiles
- Demographics for each location
- Pizza fit assessment (HIGH/MEDIUM/LOW)
- Price sensitivity guidance
- See: `location-scoring-reference.md` → Customer Fit sections

### 5. Post-Saturday Review
- Template for collecting actual revenue data
- Predicted vs actual comparison
- Score calibration notes
- See: `data-gathering-guide.md` → Post-Saturday Review section

### 6. Product Testing Framework
- A/B test design templates
- Margin impact calculations
- Decision framework
- See: `product-testing-framework.md`

---

## Maintenance Guide

### Weekly Maintenance
- None required - skill fetches fresh data each run

### Periodic Updates Needed

| What | When | File to Edit |
|------|------|--------------|
| Base scores | After 4-8 weeks of reviews | `scoring-algorithm.md` → Step 1 |
| Weather modifiers | If predictions consistently wrong | `scoring-algorithm.md` → Step 2 |
| Event modifiers | If game day performance differs | `scoring-algorithm.md` → Step 3 |
| Data source URLs | If sources change | `data-gathering-guide.md` → Quick Reference |
| Location profiles | If venue changes | `location-scoring-reference.md` |

### Adding New Features

1. **New Modifier:**
   - Add section to `scoring-algorithm.md` (e.g., Step 4c)
   - Update formula in Overview and Step 5
   - Add to worked example

2. **New Location:**
   - Add to `SKILL.md` locations table
   - Add profile to `location-scoring-reference.md`
   - Add base scores to `scoring-algorithm.md`

3. **New Data Source:**
   - Add to `data-gathering-guide.md` → Quick Reference
   - Add fallback strategy if primary fails

---

## Version History

| Version | Date | Changes |
|---------|------|---------|
| 0.1 | Dec 11, 2025 | Initial skill build (Week 1) |
| 0.2 | Dec 22, 2025 | Added data source reliability, season awareness |
| 1.0 | Dec 24, 2025 | Added holiday modifiers, time-split weather, customer fit, product testing, post-Saturday review |

---

## Testing Checklist

Before deploying changes, verify:

- [ ] Skill invokes correctly (`/capital-slice-positioning [date]`)
- [ ] Weather data is fetched from multiple sources
- [ ] Sports schedules show correct home/away status
- [ ] Holiday modifier applies for Christmas/July 4th dates
- [ ] Memo generates with all sections
- [ ] Scores seem reasonable for the conditions

---

## Known Limitations

1. **Weather Forecasts:** Accuracy degrades beyond 5 days
2. **Convention Center:** Often lacks event details - uses conservative estimate
3. **Competitor Intelligence:** Not automated - relies on manual observation
4. **Conversion Rates:** Estimated, not validated with real data yet
5. **Base Scores:** Derived from expert judgment, not historical sales data

---

## Dependencies

- Claude Code (for skill execution)
- Internet access (for web searches)
- Git/GitHub (for version control)

No API keys required - skill uses web searches for data.

---

## Support

- **Repository:** https://github.com/BiPrism/Capital-Slice
- **Author:** Brian Julius
- **Technical Assistance:** Claude Code (Anthropic)

---

*This documentation covers the Capital Slice Positioning Skill as of version 1.0*
