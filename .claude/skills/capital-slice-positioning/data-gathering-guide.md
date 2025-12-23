# Data Gathering Guide

This guide outlines how to collect the weekly data needed for positioning decisions.

---

## Data Collection Priority

**CRITICAL:** Collect data in this order. If a primary source fails, immediately use the fallback.

| Data Type | Primary Source | Fallback Sources | Without Data |
|-----------|---------------|------------------|--------------|
| Weather | NWS | Weather.com → AccuWeather | Cannot proceed |
| Sports | ESPN | Team websites → NBA/NHL sites | Assume no games |
| Convention | EventsDC | ConventionCalendar.com | Assume no event |
| Special Events | Washington.org | Eventbrite → DC.gov | Assume none |

---

## Holiday Awareness (Check First!)

Before gathering data, check if the target Saturday falls on or near a major holiday. Holidays significantly affect traffic patterns.

### Holiday Impact Reference

| Holiday | Typical Date | Eastern Market | Tourist Areas | Event Venues | Overall Impact |
|---------|--------------|----------------|---------------|--------------|----------------|
| New Year's Day | Jan 1 | CLOSED | Low | Variable | Low traffic |
| MLK Weekend | 3rd Mon Jan | Open | Moderate | Low | Normal+ |
| Presidents Day Wknd | 3rd Mon Feb | Open | Moderate | Low | Normal |
| Easter Weekend | Variable | Check | High | Low | Tourist surge |
| Memorial Day Wknd | Last Mon May | Open | HIGH | Low | Tourist surge |
| July 4th | Jul 4 | Open | EXCEPTIONAL | Low | Mall is packed |
| Labor Day Wknd | 1st Mon Sep | Open | High | Low | Tourist surge |
| Columbus Day Wknd | 2nd Mon Oct | Open | Moderate | Low | Normal+ |
| Veterans Day | Nov 11 | Open | Moderate | Low | Normal |
| Thanksgiving Wknd | 4th Thu Nov | Fri: Check, Sat: Open | Moderate | Low | Mixed |
| Christmas Eve | Dec 24 | CLOSED | Low | Low | Very low |
| Christmas Day | Dec 25 | CLOSED | Very Low | Low | Dead |
| Christmas Week | Dec 26-30 | Check | Low-Moderate | Low | Reduced |
| New Year's Eve | Dec 31 | Check | Moderate | HIGH (Arena) | Evening focus |

### Holiday-Specific Guidance

**Christmas Week (Dec 24-31):**
- Eastern Market flea market typically closed Dec 24-25, may be reduced Dec 26-31
- Office/business areas dead (Convention Center unlikely to have events)
- Tourist spots (National Mall) have SOME visitors but reduced
- Residential areas (Columbia Heights) may be stronger relative to usual
- Arena may have holiday events (Wizards/Capitals games common)
- **Scoring adjustment:** -20 to all base scores except Arena (if game scheduled)

**New Year's Eve/Day:**
- Dec 31 evening: Downtown/Arena area for celebrations
- Jan 1: Most locations slow, Eastern Market closed
- **Scoring adjustment:** Jan 1 gets -30 to outdoor locations

**July 4th Weekend:**
- National Mall is THE destination (fireworks, celebrations)
- Massive crowds but also massive competition and logistics challenges
- Consider: Is the extra volume worth the operational difficulty?
- **Scoring adjustment:** National Mall +50, but note HIGH COMPETITION flag

**Summer Holiday Weekends (Memorial Day, Labor Day):**
- Tourist surge across all outdoor locations
- Eastern Market strong, waterfront locations excellent
- **Scoring adjustment:** +10 to tourist-facing locations

**Thanksgiving Weekend:**
- Friday: Locals shopping, tourists arriving
- Saturday: Mixed - some tourists, some locals with family
- Eastern Market typically open Saturday
- **Scoring adjustment:** Normal, but note uncertainty

### Holiday Checklist

Add this to your data collection:

```
HOLIDAY CHECK - Saturday [DATE]

□ Is this a holiday weekend? [YES/NO]
□ Holiday name: [_____________]
□ Eastern Market status: [Open / Closed / Uncertain]
□ Expected tourist level: [High / Normal / Low]
□ Arena/Convention special events? [YES/NO]
□ Apply holiday scoring adjustments? [YES/NO]

Notes: [Any special considerations]
```

---

## Step 1: Weather Forecast

### Required Data Points
- **Date:** Target Saturday
- **Temperature:** High and low (MUST have both morning and afternoon if possible)
- **Precipitation:** Probability by time window (CRITICAL for outdoor locations)
- **Conditions:** Sunny, partly cloudy, cloudy, rain, etc.
- **Wind:** Speed in mph (if unavailable, assume <10mph)

### Data Sources (In Order of Reliability)

**Primary: National Weather Service (Free, No API Key)**
- URL: `https://forecast.weather.gov/MapClick.php?lat=38.9072&lon=-77.0369`
- Provides hourly forecasts for Washington DC
- **Reliability:** High for 5-day forecast, degrades beyond
- **Tip:** Look for the "Hourly Weather Forecast" link for time-specific data

**Fallback 1: Weather.com**
- URL: `https://weather.com/weather/hourbyhour/l/38.90,-77.04`
- Hourly breakdown available
- **Reliability:** Good, commercial grade

**Fallback 2: AccuWeather**
- URL: `https://www.accuweather.com/en/us/washington/20006/hourly-weather-forecast/327659`
- Provides "RealFeel" temperature which accounts for wind/humidity
- **Reliability:** Good for extended forecasts

**Fallback 3: OpenWeather**
- URL: `https://openweathermap.org/city/4140963` (Washington DC)
- API available for programmatic access
- **Reliability:** Moderate, but has structured API

### Weather Uncertainty Protocol

If forecasts conflict between sources:
1. Use NWS as primary
2. If NWS shows >30% different from others, note "HIGH UNCERTAINTY" in memo
3. For high uncertainty days, favor weather-independent locations

### Weather Data Template

```
WEATHER FORECAST - Saturday [DATE]

Morning (7 AM - 12 PM):
- Temperature: [XX]°F
- Precipitation: [XX]%
- Conditions: [Sunny/Cloudy/Rain]
- Wind: [XX] mph

Afternoon (2 PM - 8 PM):
- Temperature: [XX]°F
- Precipitation: [XX]%
- Conditions: [Sunny/Cloudy/Rain]
- Wind: [XX] mph

Overall Assessment: [Good/Marginal/Bad]
```

---

## Step 2: Sports Schedules

### Season Awareness (CRITICAL)

Before checking schedules, verify if teams are in-season:

| Team | Sport | Typical Season | Off-Season Months |
|------|-------|----------------|-------------------|
| Washington Nationals | MLB | April - October | November - March |
| Washington Wizards | NBA | October - April | May - September |
| Washington Capitals | NHL | October - April | May - September |
| Washington Mystics | WNBA | May - September | October - April |
| DC United | MLS | March - October | November - February |

**For off-season teams:** Skip schedule check, apply "No Game" penalty to relevant locations.

### Teams to Check

| Team | Sport | Venue | Impact Location |
|------|-------|-------|-----------------|
| Washington Nationals | MLB | Nationals Park | Navy Yard |
| Washington Wizards | NBA | Capital One Arena | Arena |
| Washington Capitals | NHL | Capital One Arena | Arena |
| Washington Mystics | WNBA | Capital One Arena | Arena |
| DC United | MLS | Audi Field | Navy Yard area |

### Data Sources (In Order of Reliability)

**Primary: ESPN Schedules (Most Reliable)**
- Wizards: `https://www.espn.com/nba/team/schedule/_/name/wsh`
- Capitals: `https://www.espn.com/nhl/team/schedule/_/name/wsh`
- Nationals: `https://www.espn.com/mlb/team/schedule/_/name/wsh`
- Mystics: `https://www.espn.com/wnba/team/schedule/_/name/wsh`
- DC United: `https://www.espn.com/soccer/team/fixtures/_/id/13884`
- **Reliability:** High - updated in real-time, includes game times and TV info

**Fallback 1: Official Team Websites**
- Nationals: `https://www.mlb.com/nationals/schedule`
- Wizards: `https://www.nba.com/wizards/schedule`
- Capitals: `https://www.nhl.com/capitals/schedule`
- Mystics: `https://mystics.wnba.com/schedule/`
- DC United: `https://www.dcunited.com/schedule`
- **Reliability:** High - authoritative source

**Fallback 2: Venue Websites**
- Capital One Arena: `https://www.capitalonearena.com/events`
- Nationals Park: `https://www.mlb.com/nationals/ballpark`
- **Reliability:** Good - shows all venue events, not just sports

**Fallback 3: CBS Sports / Yahoo Sports**
- Wizards: `https://www.cbssports.com/nba/teams/WAS/washington-wizards/schedule/`
- Capitals: `https://www.cbssports.com/nhl/teams/WAS/washington-capitals/schedule/`
- **Reliability:** Good backup

### Home vs Away Verification

**CRITICAL:** Only HOME games impact our positioning!
- Check if game shows venue as "Capital One Arena" or "Nationals Park"
- Away games have NO impact on DC locations
- If source doesn't clearly indicate home/away, verify on team website

### Sports Data Template

```
SPORTS EVENTS - Saturday [DATE]

□ Nationals: [No Game / vs [OPPONENT] at [TIME]]
□ Wizards: [No Game / vs [OPPONENT] at [TIME]]
□ Capitals: [No Game / vs [OPPONENT] at [TIME]]
□ Mystics: [No Game / vs [OPPONENT] at [TIME]]
□ DC United: [No Game / vs [OPPONENT] at [TIME]]

Games Affecting Positioning:
- [List games with venue and time]
```

---

## Step 3: Convention Center Schedule

### Data Sources (In Order of Reliability)

**Primary: Events DC Official Calendar**
- Events Calendar: `https://eventsdc.com/venue/walter-e-washington-convention-center/events-calendar`
- Main site: `https://eventsdc.com/`
- **Reliability:** Authoritative but sometimes sparse on details
- **Tip:** Calendar may only show that an event exists, not the name/size

**Fallback 1: Convention Calendar Aggregators**
- ConventionCalendar.com: `https://conventioncalendar.com/us/dc/washington-dc/walter-e-washington-convention-center/`
- 10times.com: `https://10times.com/venues/washington-convention-center`
- **Reliability:** Good - often has event names and expected attendance

**Fallback 2: Web Search Strategy**
- Search: `"Walter E Washington Convention Center" [target date] event`
- Search: `"Washington DC convention" [month] [year]`
- **Reliability:** Variable but can find press releases for major events

**Fallback 3: Trade Publication Calendars**
- TSNN.com (Trade Show News Network): Search for DC conventions
- ExhibitorOnline.com: Major trade show listings
- **Reliability:** Good for industry-specific events

### What to Look For
- Major conventions (5,000+ attendees) → +70 modifier
- Trade shows (3,000-5,000) → +50 modifier
- Consumer shows (1,000-3,000) → +30 modifier
- Corporate events (<1,000) → +10 modifier or ignore
- Note: Smaller events (<2,000) may not justify primary positioning

### Event Identification Strategy

If only "event exists" is confirmed but no details:
1. Check event hours: 7am-3pm suggests consumer/public event
2. Check if it's a weekend: Weekends favor consumer shows over business conventions
3. Estimate conservatively: Use +30 (small event) if uncertain
4. Note uncertainty in memo

### Convention Data Template

```
CONVENTION CENTER - Saturday [DATE]

Event: [EVENT NAME or "Unknown Event" or "No Event Scheduled"]
Expected Attendance: [NUMBER or "Unknown - estimated small/medium/large"]
Hours: [START - END or N/A]
Source: [Where this info came from]
Confidence: [High/Medium/Low]

Impact: [High/Medium/Low/None]
```

---

## Step 4: Special Events & Festivals

### Data Sources

**Washington.org Events:**
- URL: `https://washington.org/things-do-washington-dc`
- Filter by date for Saturday events

**DC.gov Events Calendar:**
- URL: `https://calendar.dc.gov/`

**Eventbrite DC:**
- URL: `https://www.eventbrite.com/d/dc--washington/events/`
- Filter by Saturday date

**National Mall Events:**
- National Park Service: `https://www.nps.gov/nama/planyourvisit/calendar.htm`

### Events to Watch For

| Event Type | Impact Location | Typical Modifier |
|------------|-----------------|------------------|
| H Street Festival | H Street | +50 |
| National Mall Rally/March | National Mall | +40 |
| Cherry Blossom Festival | National Mall, Tidal Basin | +30 |
| Neighborhood Festivals | Various | +20-30 |
| Concerts at Major Venues | U Street, Arena | +20-30 |

### Events Data Template

```
SPECIAL EVENTS - Saturday [DATE]

□ National Mall: [Event or "No major event"]
□ H Street: [Event or "No festival"]
□ Other Festivals: [List any neighborhood events]
□ Concerts/Shows: [List relevant performances]

Key Events Affecting Positioning:
- [Event 1: Location, Time, Expected Impact]
- [Event 2: Location, Time, Expected Impact]
```

---

## Step 5: Recurring Markets

### Markets to Confirm

| Market | Location | Day | Hours |
|--------|----------|-----|-------|
| Eastern Market Flea | Eastern Market | Sat-Sun | 10 AM - 5 PM |
| Dupont Circle Farmers | Dupont Circle | Sunday | 9 AM - 1 PM |
| FRESHFARM Markets | Various | Various | Check schedule |

**Note:** Eastern Market operates most Saturdays but may be affected by holidays or weather. Confirm if in doubt.

### Market Data Template

```
MARKETS - Saturday [DATE]

□ Eastern Market Flea: [Operating / Closed / TBD]
□ Other relevant markets: [List]
```

---

## Step 6: Competitor Intelligence (Optional)

### Data Sources

**Social Media:**
- Search Twitter/X: `food truck DC Saturday`
- Search Instagram: #dcfoodtrucks, #dcstreetfood
- Check competitor accounts for location announcements

**Food Truck Aggregators:**
- Food Truck Fiesta: `https://foodtruckfiesta.com/`
- Roaming Hunger: `https://roaminghunger.com/dc`

### What to Track
- Direct pizza competitors (rare)
- Italian food trucks
- Popular trucks that draw crowds (may indicate good spots)
- Trucks avoiding certain areas (may indicate problem)

### Competitor Data Template

```
COMPETITOR INTELLIGENCE - Saturday [DATE]

Known Competitor Positions:
- [Competitor 1]: [Location or "Unknown"]
- [Competitor 2]: [Location or "Unknown"]

Observations:
- [Any patterns or notable intelligence]
```

---

## Weekly Data Collection Checklist

Complete by **Thursday 6 PM ET** to allow time for analysis:

```
WEEKLY DATA COLLECTION - Saturday [DATE]

□ Weather forecast gathered
  □ Morning conditions
  □ Afternoon conditions
  □ Overall assessment

□ Sports schedules checked
  □ Nationals
  □ Wizards
  □ Capitals
  □ Mystics
  □ DC United

□ Convention Center checked
  □ Event identified (if any)
  □ Attendance estimated

□ Special events researched
  □ National Mall
  □ H Street
  □ Other neighborhoods
  □ Concerts/shows

□ Markets confirmed
  □ Eastern Market status

□ Competitor intelligence (optional)
  □ Social media scanned
  □ Aggregator sites checked

Data Collection Complete: [YES/NO]
Ready for Analysis: [YES/NO]
```

---

## Sample Completed Data Collection

```
WEEKLY DATA - Saturday, December 14, 2024

WEATHER:
Morning: 45°F, 10% precipitation, Partly Cloudy, 8 mph wind
Afternoon: 52°F, 15% precipitation, Partly Cloudy, 10 mph wind
Assessment: MARGINAL (cool but dry)

SPORTS:
□ Nationals: Off-season
□ Wizards: vs Celtics at 7:00 PM
□ Capitals: No Game
□ Mystics: Off-season
□ DC United: Off-season

CONVENTION CENTER:
Event: Tech Conference 2024
Attendance: ~8,000
Hours: 9 AM - 6 PM
Impact: HIGH

SPECIAL EVENTS:
□ National Mall: No major event
□ H Street: No festival
□ Other: Holiday market at Union Market

MARKETS:
□ Eastern Market: Operating

COMPETITORS:
- DC Slices (competitor): Unknown
- Italian food truck spotted at Dupont last week

ANALYSIS READY: YES
```

---

## Fallback Strategies & Troubleshooting

### When Primary Sources Fail

| Scenario | Action |
|----------|--------|
| NWS weather unavailable | Use Weather.com → AccuWeather → delay analysis |
| ESPN schedule shows errors | Use official team websites → venue calendars |
| EventsDC has no details | Use aggregator sites → web search → estimate conservatively |
| All sources down | Use conservative assumptions, note HIGH UNCERTAINTY |

### Conservative Default Assumptions

When data is unavailable, use these defaults:

| Data Type | Default Assumption | Impact |
|-----------|-------------------|--------|
| Weather (unknown) | Marginal conditions | -10 outdoor locations |
| Sports game (uncertain) | No game | Base scores only |
| Convention (event exists, unknown size) | Small event | +30 modifier |
| Eastern Market (holiday) | Possibly closed | -40 if confirmed closed |
| Competition (unknown) | No known competitors | +0 modifier |

### Data Quality Indicators

Add these flags to your memo when relevant:

- **[HIGH CONFIDENCE]** - Multiple sources confirm, specific details available
- **[MODERATE CONFIDENCE]** - Single authoritative source OR multiple partial sources
- **[LOW CONFIDENCE]** - Assumptions made, limited data available
- **[UNCERTAIN]** - Data conflicting or unavailable, using conservative defaults

### Common Failure Patterns

1. **Holiday weekends:** Many event calendars are sparse; search for "[holiday] DC events [year]"
2. **Far-future dates:** Weather forecasts degrade past 5 days; note uncertainty
3. **Private events:** Convention Center may host unlisted corporate events
4. **Last-minute changes:** Sports games can be rescheduled; check day-of if possible

---

## Quick Reference: All Data Sources

### Weather
| Priority | Source | URL |
|----------|--------|-----|
| 1 | NWS | forecast.weather.gov/MapClick.php?lat=38.9072&lon=-77.0369 |
| 2 | Weather.com | weather.com/weather/hourbyhour/l/38.90,-77.04 |
| 3 | AccuWeather | accuweather.com/en/us/washington/20006/hourly-weather-forecast/327659 |

### Sports (In-Season Only)
| Team | ESPN URL |
|------|----------|
| Wizards | espn.com/nba/team/schedule/_/name/wsh |
| Capitals | espn.com/nhl/team/schedule/_/name/wsh |
| Nationals | espn.com/mlb/team/schedule/_/name/wsh |
| Mystics | espn.com/wnba/team/schedule/_/name/wsh |
| DC United | espn.com/soccer/team/fixtures/_/id/13884 |

### Venues
| Venue | Events URL |
|-------|------------|
| Capital One Arena | capitalonearena.com/events |
| Convention Center | eventsdc.com/venue/walter-e-washington-convention-center/events-calendar |

### Events
| Source | URL |
|--------|-----|
| Washington.org | washington.org/find-dc-listings/dc-events |
| Eventbrite | eventbrite.com/d/dc--washington/events/ |
| DC.gov Calendar | calendar.dc.gov/

---

## Post-Saturday Review (Score Calibration)

Complete this review by **Monday** after each Saturday to build data for score calibration.

### Review Template

```
POST-SATURDAY REVIEW - [DATE]

=== WHAT WE PREDICTED ===
Truck A: [Morning Location] → [Afternoon Location]
Truck B: [Morning Location] → [Afternoon Location]

Morning Scores: [Location]: [Score], [Location]: [Score]
Afternoon Scores: [Location]: [Score], [Location]: [Score]

Expected Performance: [from memo]

=== WHAT ACTUALLY HAPPENED ===

TRUCK A:
Morning Location: [Where deployed]
  - Hours worked: [X:XX - X:XX]
  - Revenue: $[XXX]
  - Revenue/hour: $[XX]
  - Observations: [Busy? Slow? Weather impact?]

Afternoon Location: [Where deployed]
  - Hours worked: [X:XX - X:XX]
  - Revenue: $[XXX]
  - Revenue/hour: $[XX]
  - Did we relocate as planned? [Yes/No]
  - Observations: [Busy? Slow? Event impact?]

TRUCK B:
Morning Location: [Where deployed]
  - Hours worked: [X:XX - X:XX]
  - Revenue: $[XXX]
  - Revenue/hour: $[XX]
  - Observations: [Busy? Slow? Weather impact?]

Afternoon Location: [Where deployed]
  - Hours worked: [X:XX - X:XX]
  - Revenue: $[XXX]
  - Revenue/hour: $[XX]
  - Did we relocate as planned? [Yes/No]
  - Observations: [Busy? Slow? Event impact?]

=== CONDITIONS THAT DAY ===
Actual Weather:
  - Morning temp: [XX]°F
  - Afternoon temp: [XX]°F
  - Did it rain? [Yes/No, what time?]
  - Wind issues? [Yes/No]

Events:
  - Did predicted events happen? [Yes/No]
  - Surprise events we missed? [List]
  - Eastern Market operating? [Yes/No]

Competition:
  - Competitors spotted? [Where?]

=== PREDICTED VS ACTUAL ===

| Location | Predicted Score | Actual $/hr | Notes |
|----------|-----------------|-------------|-------|
| [Morning 1] | [XX] | $[XX] | |
| [Morning 2] | [XX] | $[XX] | |
| [Afternoon 1] | [XX] | $[XX] | |
| [Afternoon 2] | [XX] | $[XX] | |

Performance vs Expectation: [Better / As Expected / Worse]

=== CALIBRATION NOTES ===

Score Adjustments to Consider:
- [ ] [Location] base score seems [too high / too low] because [reason]
- [ ] [Modifier] effect seems [too strong / too weak] because [reason]

What would we do differently?
- [Note for future similar conditions]

Confidence in this week's data: [High / Medium / Low]
```

### Building the Calibration Dataset

After 4-8 weeks of reviews, analyze patterns:

1. **Revenue vs Score correlation**
   - Plot $/hr against predicted score
   - Strong correlation = scores are well-calibrated
   - Weak correlation = base scores need adjustment

2. **Location-specific patterns**
   - Does Eastern Market consistently over/underperform its score?
   - Does Navy Yard without games perform better/worse than predicted?

3. **Modifier validation**
   - Do weather modifiers match actual impact?
   - Are event modifiers (+50 for games) accurate?

4. **Time-of-day patterns**
   - Are morning/afternoon base score ratios correct?
   - Do relocations actually pay off?

### Score Adjustment Process

When you have enough data (4+ weeks):

1. Calculate average $/hr for each location
2. Rank locations by actual performance
3. Compare to base score rankings
4. Adjust base scores to match real-world ranking
5. Test adjusted scores for 2-3 weeks
6. Repeat

**Example adjustment:**
If Columbia Heights consistently earns $120/hr (ranking #3) but scores as #5, increase its base score to reflect reality.

### Review File Location

Save reviews to: `memos/reviews/review-YYYY-MM-DD.md`

After accumulating reviews, create a calibration summary: `memos/calibration-summary.md`
