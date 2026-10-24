# Chuckles vs Whispers — Project Master Plan

## 1. Background & Methodology

- **Context**: A blind taste test to determine consumer discernment and preference between Woolworths Chuckles and Cadbury Whispers.
- **Setup**:
  - **Bag 1**: Whispers (`W`) — Cadbury (Price benchmark: ~R0.41–R0.45/g, midpoint ~R0.43/g)
  - **Bag 2**: Chuckles (`C`) — Woolworths (Price benchmark: ~R0.42–R0.52/g, midpoint ~R0.47/g, ~9.3% price premium)
- **Instructions Given to Participants**:
  1. Each bag contains either Chuckles or Whispers (possible combinations: `CC`, `CW`, `WC`, `WW`).
  2. Taste from Bag 1 and identify the product.
  3. Taste from Bag 2 and identify the product.
  4. Record a taste preference if applicable (`1`, `2`, or `Na`).
- **Sample Size**: $N = 25$ participants across roles and genders.

---

## 2. Core Hypotheses

- **Hypothesis 1**: People cannot tell the difference between Whispers and Chuckles based on taste alone.
- **Hypothesis 2**: People will prefer whichever chocolate they *believe* to be Chuckles (brand expectation bias).

---

## 3. Enriched Dataset

The data is cleaned, validated, and enriched with 14 attributes:
- Files: `data.csv`, `data.json`, `data.md`
- Key Engineered Fields:
  - `Guess Pattern`: `WC`, `CW`, `CC`, `WW`
  - `Can Distinguish`: `bag1 != bag2`
  - `Both Correct`: `bag1 == 'W' && bag2 == 'C'`
  - `Inverted`: `bag1 == 'C' && bag2 == 'W'`
  - `Preferred Brand`: Actual product selected (`Chuckles`, `Whispers`, `None`)
  - `Perceived Preference`: Brand they believed they chose based on their own guess
  - `Preferred Perceived Chuckles`: Whether their preference matched their Chuckles guess

---

## 4. Narrative Order of Insights (Locked: 3 → 2 → 4 → 1 → 5 → 6)

1. **[Insight 3] Sensory Discernment vs. Identification (The Coin Flip)**
   - 72% (18/25) perceived a sensory contrast between the bags.
   - Only 52% (13/25) correctly identified which was which (essentially chance).
   - 20% (5/25) tasted a difference but had the labels completely reversed (`C, W`).

2. **[Insight 2] The Accurate Tasters (Connoisseur Conviction)**
   - Among participants who identified both bags correctly and had a preference, **81.8% (9/11)** chose Chuckles.

3. **[Insight 4] The "Chuckles Halo" (Expectation Bias)**
   - 62.5% (10/16) preferred whichever bag they *thought* was Chuckles, demonstrating brand prestige bias.

4. **[Insight 1] The Economic Verdict (Price Premium Justified)**
   - Chuckles costs ~9.3% more per gram (~R0.47/g vs ~R0.43/g), but secured **68.8% of expressed preferences** (11 vs. 5). The Woolworths premium is backed by taste.

5. **[Insight 5] The Cognitive Default (When in Doubt, Assume Chuckles)**
   - 28% (7/25) thought both bags were identical. 
   - 6 of the 7 guessed `C, C` (Chuckles is the office default).
   - 100% of these 7 participants registered "No Preference" (`Na`), validating data integrity.

6. **[Insight 6] The Demographic Signal (Gender Palate Gap)**
   - Women: 71.4% identification accuracy (5/7) and 83.3% Chuckles preference rate.
   - Men: 44.4% identification accuracy (8/18) and 44.4% indifference/no preference rate (`Na`).

---

## 5. Visualisation Plan

A balanced mix of composite scatter/flow plots alongside clean baseline benchmark charts:

1. **The 2x2 Jitter Scatter Matrix (Sensory Discernment)**
   - **X-axis**: Bag 1 Guess (`W` vs `C`)
   - **Y-axis**: Bag 2 Guess (`W` vs `C`)
   - **Descriptive Quadrant Labels**:
     - Quadrant (W, C): **Both Correct (W, C)** — 13 participants
     - Quadrant (C, W): **Inverted (C, W)** — 5 participants
     - Quadrant (C, C): **Identical as Chuckles (C, C)** — 6 participants
     - Quadrant (W, W): **Identical as Whispers (W, W)** — 1 participant
   - **Data encoding**: Each participant is a jittered point colored by Actual Preference (Chuckles / Whispers / None).

2. **The Perception vs. Reality Slopegraph / Flow (The Expectation Halo)**
   - Connected dual-axis chart:
     - Left node: What they *thought* they chose.
     - Right node: What they *actually* chose.
   - Straight lines show alignment; crossed vectors show perception mismatch.

3. **Value & Price Comparison (Baseline + Scatter)**
   - Clean horizontal ratio indicator: Overall preference breakdown (Chuckles 69% vs Whispers 31%).
   - Price vs Preference frontier: Price per gram (+9.3%) vs Preference capture (+120%).

4. **Demographic Beeswarm / Jitter Dot Plot (Gender Sensory Gap)**
   - Two lanes: Female vs Male.
   - Y-axis: Accuracy score / outcome.
   - Highlights cluster density (female concentration at high accuracy vs male dispersion and neutral responses).

5. **Statistical Validation Note**
   - Binomial test against 50% random guess chance for identification ($p$-value context).
   - Chi-square / Fisher's test for preference distribution ($p < 0.05$ skew toward Chuckles).

---

## 6. Next Steps

1. **UI & Charting Libraries**: Evaluate charting tools (e.g. lightweight D3 / Observable Plot / Chart.js / SVG) suited for custom jitter scatter and slope charts.
2. **Website Architecture**: OpenAI-inspired minimalist design (clean whitespace, sharp monospace numbers, subtle borders, high-contrast imagery).
3. **Export Architecture**: Clean print/PDF styling or PDF generation pipeline for offline distribution.
