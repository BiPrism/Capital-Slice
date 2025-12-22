# Week 2 Progress: Testing, Evaluating & Improving

**Last Updated:** December 22, 2025
**Status:** In Progress

---

## What We Accomplished

### 1. Tested the Skill
- Generated positioning memo for Saturday, December 27, 2025
- Gathered weather, sports, convention, and event data
- Ran scoring algorithm and produced recommendation
- Output: `memos/positioning-memo-2025-12-27.md`

### 2. Identified Issues During Testing

| Issue | Severity | Status |
|-------|----------|--------|
| Weather data gaps (wind, hourly temps) | Medium | Fixed |
| Convention Center blind spot | High | Fixed |
| No seasonality awareness (MLB in December) | Medium | Fixed |
| Home vs Away game confusion | Medium | Fixed |
| Date calculation error | Low | Noted |
| Holiday context missing | Medium | Not started |
| Base score logic undocumented | Medium | Identified |

### 3. Improved Data Source Reliability

Updated `data-gathering-guide.md` with:
- Priority table showing primary vs fallback sources
- Season awareness table (don't check MLB Nov-Mar, etc.)
- Home vs away verification step
- Multiple fallback sources for each data type
- Uncertainty protocol for conflicting forecasts
- Conservative default assumptions when data unavailable
- Data quality indicators ([HIGH/MODERATE/LOW CONFIDENCE])
- Quick reference table of all URLs
- Fallback strategies & troubleshooting section

### 4. Re-Tested the Skill
- Used improved data gathering process
- Compared 3 weather sources (found 11°F variance)
- Applied season awareness (skipped off-season teams)
- Verified home/away for all games
- Used fallback strategy for Convention Center
- Output: `memos/positioning-memo-2025-12-27-v2.md`

---

## Files Modified

| File | Changes |
|------|---------|
| `.claude/skills/capital-slice-positioning/data-gathering-guide.md` | Major update - fallbacks, seasons, confidence levels |
| `memos/positioning-memo-2025-12-27.md` | Test 1 output |
| `memos/positioning-memo-2025-12-27-v2.md` | Test 2 output (improved) |

---

## Still To Do

### Identified Improvements Not Yet Implemented
1. **Holiday patterns** - Special handling for Christmas week, New Year's, July 4th
2. **Time-split weather** - Morning vs afternoon weather separately in scoring
3. **Scoring refinements** - Adjust base scores based on test experience
4. **Data validation** - Automated checks for date errors, missing data
5. **Base score documentation** - Explain how star ratings map to numbers

### Open Question
> "Where does the base score come from?"

The base scores were derived from Brian's Site Analysis document star ratings:
- ★★★★★ morning → 85 base score
- ★ morning → 10-20 base score
- Event-dependent locations have low base but high event modifiers

**Gap identified:** The exact mapping from stars to numbers isn't documented in the skill.

---

## To Continue This Work

1. Open Claude Code in this folder
2. Say: "Continue Week 2 improvements" or reference this file
3. Pick up from the "Still To Do" section above

---

## Test Results Comparison

| Aspect | Test 1 | Test 2 |
|--------|--------|--------|
| Weather sources | 1 | 3 |
| Season awareness | No | Yes |
| Home/Away check | Implicit | Explicit |
| Confidence levels | None | Yes |
| Same recommendation? | Yes | Yes |

Both tests produced: Eastern Market → Georgetown (Truck A), Dupont → Mall (Truck B)

---

*This file tracks Week 2 progress for the Capital Slice positioning skill.*
