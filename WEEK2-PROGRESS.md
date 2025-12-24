# Week 2 Progress: Testing, Evaluating & Improving

**Last Updated:** December 24, 2025
**Status:** Ready for Validation

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
| Holiday context missing | Medium | Fixed |
| Base score logic undocumented | Medium | Fixed |

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

### 4. Re-Tested the Skill (v2)
- Used improved data gathering process
- Compared 3 weather sources (found 11°F variance)
- Applied season awareness (skipped off-season teams)
- Verified home/away for all games
- Used fallback strategy for Convention Center
- Output: `memos/positioning-memo-2025-12-27-v2.md`

### 5. Final Test with All Improvements (v3)
- Applied holiday modifier (-20 for Christmas week)
- Used time-split weather calculations
- Included Customer Fit guidance
- Generated comprehensive memo with all new features
- Output: `memos/positioning-memo-2025-12-27-v3.md`

### 6. Created Validation Framework
- Added Post-Saturday Review template to data-gathering-guide
- Created blank review file for Dec 27: `memos/reviews/review-2025-12-27.md`
- Ready to collect actual revenue data and compare to predictions

---

## Files Modified

| File | Changes |
|------|---------|
| `.claude/skills/capital-slice-positioning/data-gathering-guide.md` | Fallbacks, seasons, confidence levels, holiday awareness, post-Saturday review template |
| `.claude/skills/capital-slice-positioning/scoring-algorithm.md` | Base score documentation, holiday modifiers, time-split weather |
| `.claude/skills/capital-slice-positioning/location-scoring-reference.md` | Customer Fit profiles for all 10 locations |
| `.claude/skills/capital-slice-positioning/product-testing-framework.md` | NEW - A/B testing, conversion rates, margin calculations |
| `memos/positioning-memo-2025-12-27.md` | Test 1 output |
| `memos/positioning-memo-2025-12-27-v2.md` | Test 2 output (improved) |
| `memos/positioning-memo-2025-12-27-v3.md` | Test 3 output (all improvements applied) |
| `memos/reviews/review-2025-12-27.md` | Blank review template for validation |

---

## Still To Do

### Future Improvements (Lower Priority)
1. **Data validation** - Automated checks for date errors, missing data

### Completed This Session
1. **Base score documentation** - Added star-to-score mapping in `scoring-algorithm.md`
2. **Holiday patterns** - Added Holiday Awareness section and Holiday Modifier (Step 4b)
3. **Time-split weather** - Added explicit guidance and updated worked example
4. **Scoring refinements** - Converted to feedback loop with Post-Saturday Review template
5. **Customer Fit profiles** - Added demographic/pizza fit/price sensitivity to all locations
6. **Product Testing Framework** - New file for A/B testing slice size, pricing, combos
7. **v3 Positioning Memo** - Generated with all improvements applied
8. **Validation Template** - Created blank review file for Dec 27

### Open Question (Resolved)
> "Where does the base score come from?"

**Answer:** Base scores come from Brian's Site Analysis star ratings. The mapping is now documented in `scoring-algorithm.md` under "Base Score Derivation".

---

## Next Steps: Validation

### Saturday, December 27, 2025
1. Run trucks at recommended locations:
   - Truck A: Eastern Market (AM) → Georgetown (PM)
   - Truck B: Dupont Circle (AM) → National Mall (PM)
2. Collect actual revenue, hours, and observations

### Monday, December 29, 2025
1. Complete `memos/reviews/review-2025-12-27.md`
2. Compare predicted scores to actual $/hr
3. Identify any score adjustments needed
4. Note whether holiday modifier (-20) was accurate

### After 4-8 Weeks of Data
1. Analyze patterns in review data
2. Adjust base scores if needed
3. Validate conversion rate estimates
4. Refine holiday/weather modifiers

---

## Test Results Comparison

| Aspect | Test 1 (v1) | Test 2 (v2) | Test 3 (v3) |
|--------|-------------|-------------|-------------|
| Weather sources | 1 | 3 | 3 |
| Season awareness | No | Yes | Yes |
| Home/Away check | Implicit | Explicit | Explicit |
| Confidence levels | None | Yes | Yes |
| Holiday modifiers | No | No | Yes (-20) |
| Time-split weather | No | No | Yes |
| Customer Fit guidance | No | No | Yes |
| Same recommendation? | Yes | Yes | Yes |

All three tests produced: **Eastern Market → Georgetown (Truck A), Dupont → Mall (Truck B)**

The consistent recommendation across all versions validates the core algorithm. The v3 improvements add context (holiday impacts, customer fit) without changing the fundamental logic.

---

*This file tracks Week 2 progress for the Capital Slice positioning skill.*
