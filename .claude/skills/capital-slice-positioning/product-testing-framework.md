# Product Testing Framework

This framework helps Capital Slice test product variables (slice size, shape, pricing, etc.) to optimize gross profit and margins.

---

## Part 1: Conversion Rate Estimation

### The Conversion Funnel

Not everyone at a location will buy pizza. Understanding conversion helps predict actual sales.

```
FOOT TRAFFIC (people passing by)
        ↓ × Hunger Rate
POTENTIAL FOOD BUYERS (people looking to eat)
        ↓ × Pizza Selection Rate
POTENTIAL PIZZA BUYERS (people who want pizza)
        ↓ × Capture Rate
YOUR CUSTOMERS (people who buy from you)
```

### Estimated Conversion Rates by Location Type

| Location Type | Hunger Rate | Pizza Rate | Capture Rate | Net Conversion |
|---------------|-------------|------------|--------------|----------------|
| Sports event crowd | 60% | 30% | 50% | ~9% |
| Convention attendees | 70% | 25% | 40% | ~7% |
| Residential neighborhood | 20% | 30% | 70% | ~4.2% |
| Tourist destination | 40% | 25% | 40% | ~4% |
| Market/flea market | 30% | 20% | 60% | ~3.6% |
| Nightlife area | 50% | 35% | 30% | ~5.3% |
| Waterfront leisure | 35% | 20% | 35% | ~2.5% |

**Example calculation:**
- Eastern Market foot traffic: 5,000 people
- Hunger rate: 30% → 1,500 looking to eat
- Pizza rate: 20% → 300 want pizza
- Capture rate: 60% → **180 customers**

### Conversion Rate by Location

| Location | Est. Foot Traffic | Conversion | Est. Customers |
|----------|-------------------|------------|----------------|
| Eastern Market (morning) | 5,000 | 3.6% | 180 |
| Dupont Circle | 3,000 | 4% | 120 |
| National Mall (afternoon) | 10,000 | 4% | 400 |
| Georgetown Waterfront | 4,000 | 2.5% | 100 |
| Arena (game day) | 18,000 | 9% | 1,620 |
| Convention Center (event) | 8,000 | 7% | 560 |
| Columbia Heights | 2,000 | 4.2% | 84 |

**Note:** These are estimates. Validate with actual sales data using the Post-Saturday Review.

### Tracking Actual Conversion

Add this to your Post-Saturday Review:

```
CONVERSION TRACKING - [DATE]

Location: [_____________]
Hours: [__:__ - __:__]

Estimated foot traffic: [____] (use Google Popular Times or observation)
Actual customers served: [____]
Actual conversion rate: [____%]

Compare to estimate: [Higher / As Expected / Lower]
Notes: [Why might this differ?]
```

---

## Part 2: Product Variable Testing

### Variables to Test

| Category | Variable | Test Options | Impact On |
|----------|----------|--------------|-----------|
| **Size** | Slice size | Small / Standard / Large / XL | Volume, revenue, food cost |
| **Shape** | Slice shape | Triangle / Square / Strip | Perceived value, portability |
| **Pricing** | Base price | $4 / $5 / $6 / $7 | Volume, revenue, margin |
| **Pricing** | Premium upcharge | +$1 / +$1.50 / +$2 | Uptake, margin |
| **Combos** | Slice + drink | $7 / $8 / $9 | Basket size, margin |
| **Combos** | 2-slice deal | $8 / $9 / $10 | Volume, ticket size |
| **Toppings** | Premium options | Truffle / Burrata / Prosciutto | Uptake, margin |
| **Presentation** | Plating | Paper / Branded box / Eco plate | Perceived value, cost |

### Test Design Template

```
PRODUCT TEST DESIGN

Test Name: [____________________]
Variable Being Tested: [____________________]
Hypothesis: [What do you expect to happen?]

CONTROL (A):
- Description: [Current standard]
- Price: $[___]
- Food cost: $[___]
- Margin: $[___] ([___%])

TEST (B):
- Description: [New variation]
- Price: $[___]
- Food cost: $[___]
- Margin: $[___] ([___%])

Test Duration: [___] Saturdays
Test Location(s): [____________________]
Sample Size Goal: [___] sales per variation

Success Criteria:
- [ ] Maintain volume within [___%] of control
- [ ] Increase margin by at least $[___] per unit
- [ ] Customer feedback positive

How to Run:
- [ ] Truck A runs Control, Truck B runs Test (same location type)
- [ ] Or: Week 1 Control, Week 2 Test (same location)
- [ ] Track separately in POS/records
```

---

## Part 3: Running Experiments

### A/B Test Protocol

**Option 1: Split by Truck (Same Day)**
- Truck A: Control (standard slice, $5)
- Truck B: Test (large slice, $6)
- Both at similar location types
- Compare end-of-day results

**Option 2: Split by Week (Same Location)**
- Week 1: Control
- Week 2: Test
- Same location, similar weather/events
- Compare week-over-week

**Option 3: Customer Choice Test**
- Offer both options simultaneously
- "Regular slice $5 or Large slice $7"
- Track which customers choose
- Calculate blended margin

### Minimum Sample Size

For reliable results:
- **Quick directional read:** 50+ sales per variation
- **Confident decision:** 200+ sales per variation
- **Statistical significance:** 500+ sales per variation

### Control for Variables

When comparing results, ensure similar:
- [ ] Weather conditions
- [ ] Location type
- [ ] Time of day
- [ ] Event presence
- [ ] Day of week

If conditions differ, note them and adjust interpretation.

---

## Part 4: Margin Impact Calculations

### Basic Margin Formula

```
Gross Margin = Selling Price - Food Cost
Gross Margin % = (Selling Price - Food Cost) / Selling Price × 100
```

### Margin Comparison Template

```
MARGIN ANALYSIS - [Test Name]

                        CONTROL         TEST            DIFFERENCE
Selling Price           $[___]          $[___]          $[___]
Food Cost               $[___]          $[___]          $[___]
Gross Margin/Unit       $[___]          $[___]          $[___]
Gross Margin %          [___%]          [___%]          [___%]

Units Sold              [___]           [___]           [___%] change
Total Revenue           $[___]          $[___]          $[___]
Total Food Cost         $[___]          $[___]          $[___]
Total Gross Profit      $[___]          $[___]          $[___]

VERDICT: Test [WINS / LOSES / INCONCLUSIVE]
```

### Example: Slice Size Test

```
MARGIN ANALYSIS - Large Slice Test

                        STANDARD        LARGE           DIFFERENCE
Selling Price           $5.00           $7.00           +$2.00
Food Cost               $1.25           $1.75           +$0.50
Gross Margin/Unit       $3.75           $5.25           +$1.50
Gross Margin %          75%             75%             0%

Units Sold              100             85              -15%
Total Revenue           $500            $595            +$95
Total Food Cost         $125            $149            +$24
Total Gross Profit      $375            $446            +$71 (+19%)

VERDICT: Large slice WINS despite 15% volume drop
         $71 more profit on same shift
```

### Break-Even Analysis

When testing a price increase, calculate: how much volume can you lose and still win?

```
Break-Even Volume Drop = 1 - (Old Margin / New Margin)

Example: $5 slice (margin $3.75) vs $6 slice (margin $4.50)
Break-Even = 1 - (3.75 / 4.50) = 1 - 0.833 = 16.7%

You can lose up to 16.7% of volume and still make more profit.
```

---

## Part 5: Decision Framework

### When to Adopt a Change

| Result | Volume Impact | Margin Impact | Decision |
|--------|---------------|---------------|----------|
| Volume up, margin up | Win | Win | **ADOPT immediately** |
| Volume down <10%, margin up >15% | Small loss | Big win | **ADOPT** |
| Volume down 10-20%, margin up >25% | Moderate loss | Big win | **ADOPT with monitoring** |
| Volume down >20%, margin up | Big loss | Win | **Test more / Reconsider** |
| Volume down, margin down | Loss | Loss | **REJECT** |
| Volume up, margin down | Win | Loss | **Calculate total profit** |

### Total Profit Decision

When volume and margin move opposite directions:

```
Total Profit = Units Sold × Gross Margin per Unit

Control: 100 units × $3.75 = $375
Test: 120 units × $3.25 = $390

Even though margin dropped, total profit increased. ADOPT.
```

### Consider Non-Financial Factors

- Customer satisfaction / feedback
- Operational complexity (harder to make?)
- Brand positioning (premium vs value?)
- Staff preference (easier to prepare?)

---

## Part 6: Test Ideas to Start

### High-Potential Tests (Low Risk, High Reward)

| Test | Why | Expected Impact |
|------|-----|-----------------|
| **$1 price increase** | Simple, no cost change | +$1 margin if volume holds |
| **Premium topping upcharge** | Optional, customers self-select | +$1-2 on ~20% of orders |
| **Combo with drink** | Increases basket size | +$2-3 margin, moves drinks |
| **Branded box at Georgetown** | Perceived value in upscale area | Justify $1 premium |

### Medium Tests (Moderate Complexity)

| Test | Why | Expected Impact |
|------|-----|-----------------|
| **Large slice option** | Some customers want more | Higher ticket, similar % margin |
| **Square slices at conventions** | Easier to eat while standing | Differentiation, same cost |
| **2-for-$X deal** | Volume driver | Lower margin %, higher total |

### Advanced Tests (Require More Setup)

| Test | Why | Expected Impact |
|------|-----|-----------------|
| **Location-based pricing** | Georgetown vs Columbia Heights | Capture willingness to pay |
| **Time-based pricing** | Premium at game time | Capture peak demand |
| **Limited-time special** | Create urgency | Test new flavors risk-free |

---

## Part 7: Test Tracking Log

Keep a running log of all tests:

```
TEST LOG - Capital Slice

| Date | Test Name | Variable | Result | Decision | Notes |
|------|-----------|----------|--------|----------|-------|
| [DATE] | Large Slice | Size | +19% profit | ADOPTED | Now standard at Arena |
| [DATE] | $6 Price | Price | -25% volume | REJECTED | Too aggressive |
| [DATE] | Combo Deal | Bundle | +$2.50 avg ticket | ADOPTED | All locations |
```

---

## Part 8: Integrating with Positioning

### Location-Specific Product Strategy

Based on Customer Fit profiles, consider different product strategies:

| Location | Demo | Suggested Product Strategy |
|----------|------|---------------------------|
| Eastern Market | Foodies | Premium toppings, quality positioning |
| Arena | Sports fans | Large slices, combo deals, speed |
| Convention Ctr | Business | Professional presentation, premium price |
| National Mall | Tourists/families | Classic flavors, kid-size option |
| Columbia Hts | Neighborhood | Value pricing, loyalty program |
| Georgetown | Upscale | Branded box, premium price, shareable |

### Pricing by Location

Consider testing location-based pricing:

| Location Type | Suggested Price Point | Rationale |
|---------------|----------------------|-----------|
| High-income (Georgetown, Dupont) | $6-7 | Low price sensitivity |
| Tourist (Mall, Arena) | $5-6 | Captive but budget-aware |
| Residential (Columbia Hts) | $4-5 | Price-sensitive regulars |
| Event (Convention, Game) | $6-7 | Convenience premium |

---

## Quick Start Checklist

Ready to start testing? Here's your first week:

1. [ ] Pick ONE variable to test (suggest: price or slice size)
2. [ ] Design the test using the template above
3. [ ] Run for 2 Saturdays minimum
4. [ ] Track results in the Margin Analysis template
5. [ ] Make decision using the Decision Framework
6. [ ] Log results in Test Tracking Log
7. [ ] Move to next test

**Start simple. One variable at a time. Let data guide decisions.**
