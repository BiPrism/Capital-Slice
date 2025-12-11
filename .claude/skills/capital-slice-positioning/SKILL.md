---
name: capital-slice-positioning
description: Optimize Capital Slice food truck positioning for Saturdays in Washington DC. Analyzes weather forecasts, events (sports, conventions, festivals, markets), and competitor activity to score 10 permitted locations. Recommends morning and afternoon positions for both trucks with relocation decisions. Generates a 2-page decision memo by Thursday evening.
---

# Capital Slice Saturday Positioning Optimizer

## Purpose

Every Thursday by 11:59pm ET, generate a data-driven positioning strategy for Capital Slice's two food trucks for the upcoming Saturday. The output is a clear, actionable 2-page memo for partners Raven and Brian.

## The Optimization Problem

| Truck | Morning (7 AM - 12 PM) | Afternoon (2 PM - 8 PM) |
|-------|------------------------|-------------------------|
| Truck A | Location ? | Location ? (may relocate) |
| Truck B | Location ? | Location ? (may relocate) |

**Constraints:**
- 10 permitted DC locations, each with unique characteristics
- Each truck can relocate once mid-day (costs 45-60 min downtime)
- Trucks cannot be at the same location (cannibalization)
- Weather affects outdoor vs indoor venue value differently
- Events create predictable traffic spikes

## The 10 Locations

| # | Location | Category | Best Time | Weather Dependency | Event Dependency |
|---|----------|----------|-----------|-------------------|------------------|
| 1 | Eastern Market | Market District | Morning | High | Medium (market) |
| 2 | Dupont Circle | Metro/Urban Hub | Morning-Afternoon | Medium | Medium (market) |
| 3 | National Mall | Tourist/Monument | All Day | Very High | Low |
| 4 | Georgetown Waterfront | Waterfront/Upscale | Afternoon | Very High | Low |
| 5 | U Street Corridor | Arts/Music | Evening | Medium | High (concerts) |
| 6 | Convention Center | Convention/Business | Event Days Only | None | Critical |
| 7 | Capital One Arena | Sports/Entertainment | Game Days Only | None (inverse) | Critical |
| 8 | Columbia Heights | Residential | Midday | Medium | Low |
| 9 | H Street Corridor | Arts/Festival | Afternoon-Evening | Medium | High (festivals) |
| 10 | Navy Yard / Wharf | Waterfront/Sports | Game Days | Medium | Critical (Nationals) |

## Data Gathering Workflow

### Step 1: Weather Forecast
Gather Saturday's forecast for Washington DC:
- Temperature (high/low)
- Precipitation probability by time window (morning vs afternoon)
- Wind conditions
- Overall conditions (sunny, cloudy, rainy)

**Sources:** National Weather Service, OpenWeather, or weather.com

### Step 2: Events Calendar
Check for Saturday events:

**Sports (check game times):**
- Nationals (MLB) at Nationals Park - impacts Navy Yard
- Wizards (NBA) at Capital One Arena
- Capitals (NHL) at Capital One Arena
- Mystics (WNBA) at Capital One Arena
- DC United (MLS) at Audi Field

**Recurring Markets:**
- Eastern Market weekend flea market (typically operates)
- Dupont Circle farmers market (Sunday, but check Saturday events)

**Special Events:**
- Convention Center schedule
- National Mall events (rallies, festivals)
- H Street festivals
- Neighborhood cultural events

**Sources:** Team websites, ESPN, Eventbrite, washington.org, DC.gov calendar

### Step 3: Competitor Intelligence (Optional)
- Check food truck social media for announced positions
- Note any direct pizza competitors
- Identify likely clustering locations

**Sources:** Instagram, Twitter/X, food truck aggregator sites

## Scoring Algorithm

### Base Scores by Time Window

Each location has a base score for morning (M) and afternoon (A):

| Location | Morning Base | Afternoon Base |
|----------|-------------|----------------|
| Eastern Market | 85 | 30 |
| Dupont Circle | 75 | 60 |
| National Mall | 50 | 80 |
| Georgetown Waterfront | 40 | 85 |
| U Street | 20 | 65 |
| Convention Center | 10 | 10 |
| Capital One Arena | 10 | 10 |
| Columbia Heights | 55 | 55 |
| H Street | 25 | 70 |
| Navy Yard / Wharf | 30 | 75 |

### Weather Modifiers

**Good Weather (sunny, <20% rain, 60-80°F):**
- Outdoor locations (Mall, Georgetown, Navy Yard): +20
- All locations: +5

**Bad Weather (>50% rain OR <45°F OR >90°F):**
- Outdoor locations: -40
- Indoor event locations (Arena, Convention Center): +25 if event scheduled
- Covered/urban locations: -10

**Marginal Weather (20-50% rain, moderate temps):**
- Outdoor locations: -15
- Indoor event locations: +10 if event scheduled

### Event Modifiers

**Sports Game Scheduled:**
- Capital One Arena (Wizards/Caps/Mystics): +60 (peaks 2-3 hrs before game)
- Navy Yard (Nationals): +50 (peaks 2-3 hrs before first pitch)
- Afternoon game: apply to afternoon score
- Evening game: apply to afternoon score (pre-game crowds)

**Convention at Convention Center:**
- Convention Center: +70
- Apply to time windows when attendees are present

**Festival/Special Event:**
- H Street Festival: +50 to H Street
- National Mall event: +40 to National Mall
- Apply modifier to relevant time window

**No Events at Event-Dependent Location:**
- Convention Center: remains at base 10
- Capital One Arena: remains at base 10
- Navy Yard (no game): -20 from base

### Competition Modifier

If known competitor at location: -15

## Decision Logic

### Step 1: Calculate All Scores
For each location, calculate:
- Morning Score = Base Morning + Weather Modifier + Event Modifier + Competition Modifier
- Afternoon Score = Base Afternoon + Weather Modifier + Event Modifier + Competition Modifier

### Step 2: Identify Top Morning Locations
Rank locations by morning score. Assign Truck A to #1, Truck B to #2.

### Step 3: Evaluate Afternoon Options
For each truck, compare:
- **Stay**: Afternoon score at current location
- **Relocate**: (Best available afternoon score) - 15 (relocation penalty)

Relocate if: Relocated Score > Stay Score

### Step 4: Avoid Conflicts
- If both trucks would be at same location, assign to truck with higher marginal benefit
- Reassign other truck to next best option

### Step 5: Calculate Expected Value
Sum the final scores for all 4 position-time combinations. Compare to baseline (average Saturday).

## Output: Decision Memo Format

Generate a memo following this structure (max 2 pages):

```
CAPITAL SLICE POSITIONING MEMO
Saturday, [DATE]
Prepared: Thursday, [DATE]

RECOMMENDATION SUMMARY
┌─────────┬────────────────────┬────────────────────┐
│         │ Morning (7AM-12PM) │ Afternoon (2PM-8PM)│
├─────────┼────────────────────┼────────────────────┤
│ Truck A │ [Location]         │ [Location/STAY]    │
│ Truck B │ [Location]         │ [Location/STAY]    │
└─────────┴────────────────────┴────────────────────┘

KEY FACTORS THIS WEEK
• Weather: [1-2 sentence summary]
• Events: [List key events affecting positioning]
• Competition: [Any known competitor positions]

LOCATION ANALYSIS

Morning Positioning:
[2-3 sentences explaining why these morning locations were chosen]

Afternoon Strategy:
[2-3 sentences on afternoon positioning and relocation decisions]

RISK ASSESSMENT
• Primary Risk: [Biggest uncertainty, e.g., weather change]
• Backup Plan: [What to do if conditions change]

EXPECTED PERFORMANCE
[1-2 sentences comparing expected revenue vs typical Saturday]
```

## Usage Examples

### Example 1: Good Weather, Nationals Game
**Input:** Sunny 75°F, Nationals 4pm game, no other major events
**Output:**
- Truck A: Eastern Market (morning) → Navy Yard (afternoon)
- Truck B: Dupont Circle (morning) → Georgetown Waterfront (afternoon)

### Example 2: Rainy Day, Wizards Game
**Input:** 60% rain, 55°F, Wizards 7pm game
**Output:**
- Truck A: Columbia Heights (morning) → Capital One Arena (afternoon)
- Truck B: Eastern Market (morning) → STAY (covered area)

### Example 3: Perfect Weather, No Events
**Input:** Sunny 72°F, no sports/conventions
**Output:**
- Truck A: Eastern Market (morning) → National Mall (afternoon)
- Truck B: Dupont Circle (morning) → Georgetown Waterfront (afternoon)

## Reference Documents

- `Capital Slice Site Analysis.md` - Detailed location profiles
- `Capital-Slice-business-challenge-briefing.md` - Full business context
- `dc-locations-map.html` - Interactive location map
