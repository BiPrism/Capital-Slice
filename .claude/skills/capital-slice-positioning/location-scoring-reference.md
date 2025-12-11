# Capital Slice Location Scoring Reference

## Quick Reference Matrix

| # | Location | Morning | Afternoon | Weather Dep. | Event Dep. | Competition |
|---|----------|---------|-----------|--------------|------------|-------------|
| 1 | Eastern Market | ★★★★★ | ★★ | High | Medium | Medium |
| 2 | Dupont Circle | ★★★★ | ★★★ | Medium | Medium | High |
| 3 | National Mall | ★★★ | ★★★★ | Very High | Low | Medium |
| 4 | Georgetown Waterfront | ★★★ | ★★★★ | Very High | Low | High |
| 5 | U Street Corridor | ★★ | ★★★ | Medium | High | Medium |
| 6 | Convention Center | ★ | ★★★★★* | None | Critical | Low |
| 7 | Capital One Arena | ★ | ★★★★★* | Inverse | Critical | Medium |
| 8 | Columbia Heights | ★★★ | ★★★ | Medium | Low | Low |
| 9 | H Street Corridor | ★★ | ★★★★ | Medium | High | Medium |
| 10 | Navy Yard / Wharf | ★★ | ★★★★★* | Medium | Critical | High |

*Event-dependent: Only high value when event is scheduled

---

## Detailed Location Profiles

### 1. Eastern Market (Capitol Hill)
**Address:** 7th St & C St SE
**Coordinates:** 38.8863, -76.9958

**Profile:**
- Weekend flea market draws 5,000+ visitors
- Strong breakfast/brunch culture (breakfast pizza optimal)
- Metro accessible (Eastern Market station)
- High-income Capitol Hill demographic

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 85 | 30 |
| Good Weather | +5 | +5 |
| Bad Weather | -25 | -15 |
| Market Operating | +0 (assumed) | +0 |

**Strategic Notes:**
- PRIMARY morning location in good weather
- Traffic dies sharply after 2 PM
- Relocate truck after morning rush

---

### 2. Dupont Circle
**Address:** Dupont Circle NW
**Coordinates:** 38.9096, -77.0434

**Profile:**
- Constant metro foot traffic
- Affluent neighborhood, high spend per customer
- Both breakfast and lunch viable
- Sunday farmers market (Saturday still active area)

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 75 | 60 |
| Good Weather | +10 | +10 |
| Bad Weather | -15 | -15 |

**Strategic Notes:**
- Reliable secondary morning location
- Moderate afternoon - consider relocation
- High restaurant competition

---

### 3. National Mall
**Address:** 14th St & Constitution Ave NW
**Coordinates:** 38.8893, -77.0328

**Profile:**
- Highest foot traffic in DC
- Tourist demographic willing to spend
- All-day viability in good weather
- Special events (rallies, festivals) spike traffic

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 50 | 80 |
| Good Weather | +25 | +25 |
| Bad Weather | -40 | -40 |
| Major Event | +40 | +40 |

**Strategic Notes:**
- BEST afternoon location in good weather
- Extremely weather-dependent - avoid if rain >30%
- No repeat customer base (tourists)

---

### 4. Georgetown Waterfront
**Address:** K St & 31st St NW
**Coordinates:** 38.9019, -77.0637

**Profile:**
- Scenic destination draws weekend crowds
- Joggers, recreational visitors, shoppers
- Upscale dining spillover
- Premium pricing acceptable

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 40 | 85 |
| Good Weather | +20 | +20 |
| Bad Weather | -45 | -45 |

**Strategic Notes:**
- TOP afternoon destination in perfect weather
- Completely weather-dependent
- Parking/logistics challenging

---

### 5. U Street Corridor
**Address:** U St & 14th St NW
**Coordinates:** 38.9169, -77.0319

**Profile:**
- Vibrant nightlife district
- Concert/venue proximity (9:30 Club, Lincoln Theatre)
- Diverse, food-adventurous demographic
- Evening-focused activity

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 20 | 65 |
| Good Weather | +10 | +10 |
| Bad Weather | -10 | -10 |
| Concert Night | +0 | +30 |

**Strategic Notes:**
- Skip for morning positioning
- Consider for late afternoon into evening
- Best when concerts scheduled at nearby venues

---

### 6. Convention Center
**Address:** 9th St & Mt Vernon Pl NW
**Coordinates:** 38.9048, -77.0229

**Profile:**
- Major conventions = 5,000-15,000 captive attendees
- Business crowd = higher per-transaction spend
- Weather-independent (indoor venue)
- DEAD when no events

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 10 | 10 |
| Convention Day | +70 | +70 |
| Bad Weather + Convention | +80 | +80 |

**Strategic Notes:**
- ONLY deploy when convention confirmed
- Must verify schedule weekly
- Binary: excellent or zero

---

### 7. Capital One Arena
**Address:** 7th St & F St NW
**Coordinates:** 38.8981, -77.0209

**Profile:**
- Wizards, Capitals, Mystics games (18,000 capacity)
- Pre-game hunger window is prime time
- Pizza + sports = natural pairing
- Weather-independent (indoor)

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 10 | 10 |
| Game Day (afternoon start) | +15 | +60 |
| Game Day (evening start) | +10 | +50 |
| Bad Weather + Game | +20 | +70 |

**Strategic Notes:**
- Peak is 2-3 hours before game time
- Bad weather INCREASES value (indoor event more appealing)
- Skip when no game scheduled

---

### 8. Columbia Heights
**Address:** 14th St & Irving St NW
**Coordinates:** 38.9283, -77.0326

**Profile:**
- Metro plaza creates gathering point
- Residential weekend brunch culture
- Less direct competition
- Lower risk, lower ceiling

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 55 | 55 |
| Good Weather | +5 | +5 |
| Bad Weather | -10 | -10 |

**Strategic Notes:**
- BACKUP location when primary locations compromised
- Consistent but unspectacular
- Good for testing new menu items

---

### 9. H Street Corridor
**Address:** H St & 12th St NE
**Coordinates:** 38.9001, -76.9931

**Profile:**
- Major street festivals draw 4,000+ visitors
- Streetcar delivers foot traffic
- Growing food/arts destination
- Event-dependent performance

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 25 | 70 |
| Good Weather | +10 | +10 |
| Bad Weather | -20 | -20 |
| H Street Festival | +50 | +50 |
| Other Festival | +30 | +30 |

**Strategic Notes:**
- H Street Festival is MUST-DEPLOY event
- Skip morning positioning
- Strong afternoon option on festival days

---

### 10. Navy Yard / The Wharf
**Address:** Half St SE / Maine Ave SW
**Coordinates:** 38.8769, -77.0074 / 38.8783, -77.0253

**Profile:**
- Nationals Park proximity (41,000 capacity)
- Wharf = dining destination year-round
- Pre-game crowds hungry and spending
- Waterfront atmosphere

**Scoring:**
| Factor | Morning | Afternoon |
|--------|---------|-----------|
| Base Score | 30 | 75 |
| Nationals Game (afternoon) | +20 | +50 |
| Nationals Game (evening) | +10 | +40 |
| Good Weather | +15 | +15 |
| Bad Weather | -25 | -25 |
| No Game | -20 | -20 |

**Strategic Notes:**
- TOP game day destination
- Peak is 2-3 hours before first pitch through 7th inning
- MLB season only (April-October) for game traffic
- Wharf provides baseline but high competition

---

## Weather Scoring Rules

### Temperature Bands

| Condition | Modifier | Notes |
|-----------|----------|-------|
| 65-78°F | +10 | Optimal comfort zone |
| 55-64°F or 79-85°F | +0 | Acceptable |
| 45-54°F or 86-90°F | -10 | Marginal |
| <45°F or >90°F | -25 | Avoid outdoor locations |

### Precipitation Probability

| Rain Chance | Outdoor Locations | Indoor Event Locations |
|-------------|-------------------|------------------------|
| 0-20% | +15 | +0 |
| 21-40% | +0 | +5 |
| 41-60% | -20 | +15 |
| 61-80% | -35 | +25 |
| 81-100% | -50 | +30 |

### Wind Conditions

| Wind Speed | Modifier | Notes |
|------------|----------|-------|
| <10 mph | +0 | Normal |
| 10-20 mph | -5 | Affects setup, customer comfort |
| >20 mph | -15 | Significant operational impact |

---

## Event Impact Reference

### Sports Events

| Event | Venue | Capacity | Impact Location | Modifier |
|-------|-------|----------|-----------------|----------|
| Nationals (MLB) | Nationals Park | 41,000 | Navy Yard | +50 |
| Wizards (NBA) | Capital One Arena | 18,000 | Arena | +60 |
| Capitals (NHL) | Capital One Arena | 18,000 | Arena | +60 |
| Mystics (WNBA) | Capital One Arena | 18,000 | Arena | +55 |
| DC United (MLS) | Audi Field | 20,000 | Navy Yard | +35 |

### Timing Adjustments

| Game Time | Morning Modifier | Afternoon Modifier |
|-----------|------------------|-------------------|
| 1-3 PM start | +10 | +full |
| 4-5 PM start | +5 | +full |
| 7+ PM start | +0 | +75% of full |

### Recurring Events

| Event | Location | Frequency | Modifier |
|-------|----------|-----------|----------|
| Eastern Market Flea | Eastern Market | Weekly | +0 (baseline) |
| Dupont Farmers Market | Dupont Circle | Sunday | Check Saturday |
| Convention (major) | Convention Center | Variable | +70 |
| H Street Festival | H Street | Annual | +50 |

---

## Optimal Pairing Quick Reference

### Scenario: Fair Weather, No Major Events
**Morning:** Eastern Market + Dupont Circle
**Afternoon:** National Mall + Georgetown Waterfront

### Scenario: Rainy Day, Indoor Events Available
**All Day:** Capital One Arena + Convention Center

### Scenario: Major Sports Game (Afternoon Start)
**Morning:** Eastern Market + Dupont Circle
**Afternoon:** Navy Yard (relocate) + Capital One Arena

### Scenario: Festival Day (H Street)
**Morning:** Eastern Market + Dupont Circle
**Afternoon:** H Street (relocate) + stay at morning winner

### Scenario: Marginal Weather, No Events
**All Day:** Columbia Heights + Dupont Circle (low risk)
