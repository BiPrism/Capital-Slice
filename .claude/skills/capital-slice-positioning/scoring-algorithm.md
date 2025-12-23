# Capital Slice Scoring Algorithm

This document defines the exact scoring logic for ranking locations.

---

## Overview

Each location receives a **Morning Score** and **Afternoon Score** calculated as:

```
Score = Base Score + Holiday Modifier + Weather Modifier + Event Modifier + Competition Modifier
```

The algorithm then:
1. Ranks locations by morning score → assigns trucks
2. Evaluates afternoon options for each truck
3. Decides on relocations vs staying
4. Outputs final positioning recommendation

---

## Step 1: Base Scores

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

### Base Score Derivation

Base scores come from the star ratings in `Capital Slice Site Analysis.md`:

| Star Rating | Score Range |
|-------------|-------------|
| ★★★★★ | 85 |
| ★★★★ | 70-85 |
| ★★★ | 50-65 |
| ★★ | 20-30 |
| ★ | 10 |

Scores vary within a tier based on location strength (e.g., Georgetown afternoon is 85 vs H Street afternoon at 70 — both ★★★★ but Georgetown is a stronger destination).

**Event-dependent locations:** Convention Center, Capital One Arena, and Navy Yard are rated ★★★★★* in the Site Analysis (asterisk = "only with events"). They have low base scores (10) because they're dead without events. Their value comes from event modifiers (+50 to +70), not baseline traffic.

---

## Step 2: Weather Modifiers

### 2a. Temperature Modifier

| Temperature Range | All Locations |
|-------------------|---------------|
| 65-78°F | +10 |
| 55-64°F or 79-85°F | +0 |
| 45-54°F or 86-90°F | -10 |
| <45°F or >90°F | -25 |

### 2b. Precipitation Modifier

**Outdoor-Dependent Locations:** National Mall, Georgetown Waterfront, Navy Yard

| Rain Probability | Outdoor Locations | Other Locations |
|------------------|-------------------|-----------------|
| 0-20% | +15 | +5 |
| 21-40% | +0 | +0 |
| 41-60% | -20 | -5 |
| 61-80% | -35 | -10 |
| 81-100% | -50 | -15 |

**Indoor Event Locations (when event scheduled):** Convention Center, Capital One Arena

| Rain Probability | Indoor Event Locations |
|------------------|------------------------|
| 0-20% | +0 |
| 21-40% | +5 |
| 41-60% | +15 |
| 61-80% | +25 |
| 81-100% | +30 |

### 2c. Wind Modifier

| Wind Speed | Modifier |
|------------|----------|
| <10 mph | +0 |
| 10-20 mph | -5 |
| >20 mph | -15 |

### Weather Modifier Calculation

```
Weather Modifier = Temperature Mod + Precipitation Mod + Wind Mod
```

### Time-Split Weather (Important!)

Calculate **separate weather modifiers** for morning and afternoon:

| Time Period | Use For | Typical Hours |
|-------------|---------|---------------|
| Morning | Morning scores | 7 AM - 12 PM conditions |
| Afternoon | Afternoon scores | 2 PM - 8 PM conditions |

**Why this matters:** Weather often changes throughout the day. A rainy morning that clears up means:
- Morning outdoor locations score poorly (rain penalty)
- Afternoon outdoor locations score well (clear weather bonus)

**Data source:** Use the time-split weather data from `data-gathering-guide.md` Weather Data Template.

**Example:** 70°F, 30% rain, 12 mph wind at National Mall
- Temperature: +10 (65-78°F range)
- Precipitation: +0 (21-40% range, outdoor location)
- Wind: -5 (10-20 mph range)
- **Total Weather Modifier: +5**

---

## Step 3: Event Modifiers

### 3a. Sports Events

| Event | Location | Afternoon Start | Evening Start |
|-------|----------|-----------------|---------------|
| Nationals Game | Navy Yard | +50 | +40 |
| Wizards Game | Capital One Arena | +60 | +50 |
| Capitals Game | Capital One Arena | +60 | +50 |
| Mystics Game | Capital One Arena | +55 | +45 |
| DC United Game | Navy Yard | +35 | +30 |

**Time Application:**
- Afternoon start (1-5 PM): Full modifier to afternoon score
- Evening start (6+ PM): 80% modifier to afternoon score
- Morning score: +10 for any game that day (anticipation traffic)

**No Game Penalty:**
- Navy Yard (no game): -20 from afternoon base
- Capital One Arena (no event): remains at base 10

### 3b. Convention Events

| Convention Size | Convention Center Modifier |
|-----------------|---------------------------|
| Large (8,000+) | +70 |
| Medium (3,000-7,999) | +50 |
| Small (1,000-2,999) | +30 |
| No Event | +0 (remains base 10) |

### 3c. Special Events

| Event | Location | Modifier |
|-------|----------|----------|
| H Street Festival | H Street | +50 |
| National Mall Rally/March (major) | National Mall | +40 |
| National Mall Rally (minor) | National Mall | +20 |
| Cherry Blossom Festival | National Mall | +35 |
| Neighborhood Festival | Affected location | +25 |
| Major Concert (9:30 Club, etc.) | U Street | +25 |

### 3d. Market Status

Eastern Market flea market is **assumed operating** (baseline).

If confirmed **closed** (holiday, weather cancellation):
- Eastern Market morning: -40

---

## Step 4: Competition Modifier

| Situation | Modifier |
|-----------|----------|
| Known direct competitor at location | -15 |
| Known indirect competitor (non-pizza) | -5 |
| Heavy food truck cluster expected | -10 |
| No known competition | +0 |

---

## Step 4b: Holiday Modifier

Apply these modifiers when the target Saturday falls on or near a major holiday.

### Holiday Modifier Table

| Holiday Period | All Locations | Exceptions |
|----------------|---------------|------------|
| Christmas Eve (Dec 24) | -40 | Arena +0 if game |
| Christmas Day (Dec 25) | -50 | Arena +0 if game |
| Christmas Week (Dec 26-30) | -20 | Arena +0 if game |
| New Year's Eve (Dec 31) | -20 | Arena +20 (evening events) |
| New Year's Day (Jan 1) | -30 | Arena +0 if game |
| July 4th | +0 | National Mall +50 |
| Summer Holiday Wknd | +10 (tourist locations) | — |

**Tourist locations:** National Mall, Georgetown Waterfront, Eastern Market, Navy Yard

### Eastern Market Holiday Status

| Situation | Morning Modifier |
|-----------|------------------|
| Confirmed CLOSED (holiday) | -40 |
| Uncertain (holiday weekend) | -20 |
| Confirmed OPEN | +0 |

### How to Apply

1. Check if target date is a holiday (see `data-gathering-guide.md` Holiday Awareness section)
2. Apply the holiday modifier to base scores BEFORE other modifiers
3. Note holiday status in the memo

**Example:** Christmas Week Saturday
- Eastern Market morning: 85 (base) - 20 (holiday) - 40 (closed) = 25
- Arena afternoon with game: 10 (base) + 0 (holiday exception) + 60 (game) = 70

---

## Step 5: Calculate Final Scores

### For Each Location, Calculate:

```
Morning Score = Morning Base
              + Holiday Modifier (if applicable)
              + Weather Modifier (morning conditions)
              + Event Modifier (morning-relevant events)
              + Competition Modifier

Afternoon Score = Afternoon Base
                + Holiday Modifier (if applicable)
                + Weather Modifier (afternoon conditions)
                + Event Modifier (afternoon-relevant events)
                + Competition Modifier
```

### Score Interpretation

| Score Range | Interpretation |
|-------------|----------------|
| 100+ | Exceptional opportunity |
| 80-99 | Strong choice |
| 60-79 | Good option |
| 40-59 | Acceptable |
| 20-39 | Weak - avoid if alternatives exist |
| <20 | Do not deploy |

---

## Step 6: Assignment Algorithm

### Morning Assignment

1. Rank all locations by Morning Score (descending)
2. Assign **Truck A** to highest-scoring location
3. Assign **Truck B** to second-highest-scoring location
4. Record morning assignments

### Afternoon Decision (for each truck)

Calculate **Relocation Value**:

```
Stay Value = Afternoon Score at current morning location

Relocate Value = (Best available afternoon score) - 15 (relocation penalty)
```

**Decision Rule:**
- If `Relocate Value > Stay Value + 10`: RELOCATE
- Otherwise: STAY

The +10 buffer accounts for relocation risk and operational preference for stability.

### Conflict Resolution

If both trucks would select the same afternoon location:
1. Calculate marginal benefit for each truck: `(Target Score) - (Current Location Afternoon Score)`
2. Assign target location to truck with higher marginal benefit
3. Assign other truck to next-best available option

---

## Step 7: Worked Example

### Input Data
- **Morning Weather:** 58°F, 40% rain, 12 mph wind
- **Afternoon Weather:** 72°F, 10% rain, 8 mph wind
- **Events:** Nationals game at 4:05 PM
- **Competition:** None known

### Calculate Weather Modifiers

**Morning Weather Modifiers:**
- Temperature: +0 (55-64°F range)
- Precipitation: +0 outdoor / +0 other / +5 indoor event (21-40% range)
- Wind: -5 (10-20 mph)
- **Morning total:** -5 outdoor, -5 other, +0 indoor event

**Afternoon Weather Modifiers:**
- Temperature: +10 (65-78°F range)
- Precipitation: +15 outdoor / +5 other / +0 indoor event (0-20% range)
- Wind: +0 (<10 mph)
- **Afternoon total:** +25 outdoor, +15 other, +10 indoor event

### Calculate Location Scores

Note how the marginal morning weather reduces morning scores, while the excellent afternoon weather boosts afternoon scores.

| Location | Morning Base | Weather | Events | Total AM | Afternoon Base | Weather | Events | Total PM |
|----------|-------------|---------|--------|----------|----------------|---------|--------|----------|
| Eastern Market | 85 | -5 | +0 | **80** | 30 | +15 | +0 | **45** |
| Dupont Circle | 75 | -5 | +0 | **70** | 60 | +15 | +0 | **75** |
| National Mall | 50 | -5 | +0 | **45** | 80 | +25 | +0 | **105** |
| Georgetown | 40 | -5 | +0 | **35** | 85 | +25 | +0 | **110** |
| U Street | 20 | -5 | +0 | **15** | 65 | +15 | +0 | **80** |
| Convention Ctr | 10 | +0 | +0 | **10** | 10 | +10 | +0 | **20** |
| Arena | 10 | +0 | +0 | **10** | 10 | +10 | +0 | **20** |
| Columbia Hts | 55 | -5 | +0 | **50** | 55 | +15 | +0 | **70** |
| H Street | 25 | -5 | +0 | **20** | 70 | +15 | +0 | **85** |
| Navy Yard | 30 | -5 | +10 | **35** | 75 | +25 | +50 | **150** |

### Morning Assignment
1. Eastern Market: 80 → **Truck A**
2. Dupont Circle: 70 → **Truck B**

### Afternoon Decision

**Truck A (at Eastern Market, afternoon score 45):**
- Best available: Navy Yard (150)
- Relocate Value: 150 - 15 = 135
- Stay Value: 45
- Decision: **RELOCATE to Navy Yard** (135 >> 55)

**Truck B (at Dupont Circle, afternoon score 75):**
- Best available: Georgetown (110) - Navy Yard taken
- Relocate Value: 110 - 15 = 95
- Stay Value: 75
- Decision: **RELOCATE to Georgetown** (95 > 85)

### Final Recommendation

| | Morning | Afternoon |
|---------|---------|-----------|
| **Truck A** | Eastern Market | Navy Yard |
| **Truck B** | Dupont Circle | Georgetown Waterfront |

---

## Edge Cases

### No Good Options
If all morning scores < 40, consider:
- Columbia Heights as safe backup
- Delaying start time
- Flagging as high-risk day

### Weather Uncertainty
If forecast is volatile (conflicting models):
- Favor weather-independent locations (Arena, Convention Center if events)
- Favor covered urban locations (Dupont, Columbia Heights)
- Avoid waterfront locations

### Multiple Events Same Time
- Stack event modifiers
- Cap total event modifier at +80

### Truck Maintenance / Unavailability
- Run algorithm with single truck
- Choose highest-value locations across both time periods
