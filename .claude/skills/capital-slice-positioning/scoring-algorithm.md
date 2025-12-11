# Capital Slice Scoring Algorithm

This document defines the exact scoring logic for ranking locations.

---

## Overview

Each location receives a **Morning Score** and **Afternoon Score** calculated as:

```
Score = Base Score + Weather Modifier + Event Modifier + Competition Modifier
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

## Step 5: Calculate Final Scores

### For Each Location, Calculate:

```
Morning Score = Morning Base
              + Weather Modifier (morning conditions)
              + Event Modifier (morning-relevant events)
              + Competition Modifier

Afternoon Score = Afternoon Base
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
- **Weather:** 72°F, 15% rain, 8 mph wind
- **Events:** Nationals game at 4:05 PM
- **Competition:** None known

### Calculate Weather Modifiers

Morning (assume similar to overall):
- Temperature: +10 (65-78°F)
- Precipitation: +15 (outdoor), +5 (other), +0 (indoor event)
- Wind: +0 (<10 mph)

### Calculate Location Scores

| Location | Morning Base | Weather | Events | Total Morning | Afternoon Base | Weather | Events | Total Afternoon |
|----------|-------------|---------|--------|---------------|----------------|---------|--------|-----------------|
| Eastern Market | 85 | +15 | +0 | **100** | 30 | +15 | +0 | **45** |
| Dupont Circle | 75 | +15 | +0 | **90** | 60 | +15 | +0 | **75** |
| National Mall | 50 | +25 | +0 | **75** | 80 | +25 | +0 | **105** |
| Georgetown | 40 | +25 | +0 | **65** | 85 | +25 | +0 | **110** |
| U Street | 20 | +15 | +0 | **35** | 65 | +15 | +0 | **80** |
| Convention Ctr | 10 | +10 | +0 | **20** | 10 | +10 | +0 | **20** |
| Arena | 10 | +10 | +0 | **20** | 10 | +10 | +0 | **20** |
| Columbia Hts | 55 | +15 | +0 | **70** | 55 | +15 | +0 | **70** |
| H Street | 25 | +15 | +0 | **40** | 70 | +15 | +0 | **85** |
| Navy Yard | 30 | +25 | +10 | **65** | 75 | +25 | +50 | **150** |

### Morning Assignment
1. Eastern Market: 100 → **Truck A**
2. Dupont Circle: 90 → **Truck B**

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
