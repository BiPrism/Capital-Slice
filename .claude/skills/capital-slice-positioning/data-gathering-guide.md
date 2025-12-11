# Data Gathering Guide

This guide outlines how to collect the weekly data needed for positioning decisions.

---

## Step 1: Weather Forecast

### Required Data Points
- **Date:** Target Saturday
- **Temperature:** High and low
- **Precipitation:** Probability by time window
- **Conditions:** Sunny, partly cloudy, cloudy, rain, etc.
- **Wind:** Speed in mph

### Data Sources

**Primary: National Weather Service (Free, No API Key)**
- URL: `https://forecast.weather.gov/MapClick.php?lat=38.9072&lon=-77.0369`
- Provides hourly forecasts for Washington DC

**Alternative: OpenWeather**
- URL: `https://openweathermap.org/city/4140963` (Washington DC)
- API available for programmatic access

**Alternative: Weather.com**
- URL: `https://weather.com/weather/tenday/l/Washington+DC`

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

### Teams to Check

| Team | Sport | Venue | Impact Location |
|------|-------|-------|-----------------|
| Washington Nationals | MLB | Nationals Park | Navy Yard |
| Washington Wizards | NBA | Capital One Arena | Arena |
| Washington Capitals | NHL | Capital One Arena | Arena |
| Washington Mystics | WNBA | Capital One Arena | Arena |
| DC United | MLS | Audi Field | Navy Yard area |

### Data Sources

**ESPN Schedules:**
- Nationals: `https://www.espn.com/mlb/team/schedule/_/name/wsh`
- Wizards: `https://www.espn.com/nba/team/schedule/_/name/wsh`
- Capitals: `https://www.espn.com/nhl/team/schedule/_/name/wsh`
- Mystics: `https://www.espn.com/wnba/team/schedule/_/name/wsh`
- DC United: `https://www.espn.com/soccer/team/fixtures/_/id/13884`

**Team Websites:**
- Nationals: `https://www.mlb.com/nationals/schedule`
- Wizards: `https://www.nba.com/wizards/schedule`
- Capitals: `https://www.nhl.com/capitals/schedule`

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

### Data Sources

**Walter E. Washington Convention Center:**
- Events Calendar: `https://eventsdc.com/venue/walter-e-washington-convention-center`
- Check for Saturday events with expected attendance

### What to Look For
- Major conventions (5,000+ attendees)
- Trade shows
- Consumer shows
- Note: Smaller events (<2,000) may not justify positioning

### Convention Data Template

```
CONVENTION CENTER - Saturday [DATE]

Event: [EVENT NAME or "No Major Event"]
Expected Attendance: [NUMBER or N/A]
Hours: [START - END or N/A]

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
