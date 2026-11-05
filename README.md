
# King County Housing — Exploratory Data Analysis (EDA)

An exploratory data analysis of the King County housing dataset (Seattle and surrounding areas, May 2014 – May 2015), tailored to provide data-driven buying strategies and real estate recommendations for our target client persona.

## Dataset at a Glance
* **Size:** 21,373 different houses (21,550 sales; 177 houses were sold twice, and only the latest sale is kept when counting houses).
* **Price distribution:** 93% of the houses sold for under $1M, and almost half sold for $250k–$500k.
* **Low-budget floor:** only 19 houses (0.1%) sold below $100k, so for low-budget clients we recommend planning at least $100k.
* **Use of the data:** our company's past sales, used to understand the market, not as listings Thomas can buy.

---

## Team Members
* **Parand Khajehpour**
* **Rabih**
* **Gülşah Bayhan Ara**

---

## Client Persona: Thomas Hansen
* **Profile & Goal:** Thomas is looking for a home in King County for a family of seven (himself, his wife, and five children).
* **Budget Constraint:** Very limited budget of up to **$250k**. We analysed the $100k–$250k range; the most options are between **$200k and $250k**.
* **Key Preferences:** Needs sufficient living space (at least three bedrooms, ideally 3–4), wants the best space per dollar, prioritizes a dense and social neighborhood for his kids, and is open to older or lower-grade properties requiring cosmetic updates.
---

## Hypotheses & Key Findings

### H1: Bedroom Count & Price Reality (5–6 vs. 3–4 Bedrooms)
* **Hypothesis:** Moving from 3–4 to 5–6 bedrooms raises the median price by about 25%, so a seven-person home on a low budget is hard to find.
* **Finding:** **Confirmed.** County-wide, 5–6 bedroom homes have a median price of **$637k**, which is **32% higher** than 3–4 bedroom homes (**$482k**). Large homes are also rare: 1,831 houses (8.6%) have 5–6 bedrooms, against 16,558 (77.5%) with 3–4.
* **Within the budget:** Between $100k and $250k only about 50 homes have 5–6 bedrooms (11 of them under $200k). In the same range there are **1,656** homes with 3–4 bedrooms: 58 at $100k–150k, 369 at $150k–200k and 1,229 at $200k–250k.
* **Takeaway:** Thomas should target **3–4 bedroom properties** with a budget of **$200k–$250k**, where he has almost three times as many options as under $200k (1,229 against 427).

### H2: Location, Social Neighborhood & Quality Trade-Offs
* **Hypothesis:** Certain zip codes offer an optimal balance of affordable 3+ bedroom listings, high community density (Social Score), and acceptable build quality.
* **Finding:** **Confirmed.** When filtering for 3+ bedroom homes priced between $200k and $250k, listings cluster heavily in specific suburban areas. Social scores and building conditions show no drastic deviations across the top hubs.
* **Recommended Zip Codes:**
  1. **98023:** 132 listings | Median Price: $230k | Social Score: 62.5 | Condition: 3.49 / Grade: 7.10
  2. **98042:** 105 listings | Median Price: $225k | Social Score: 64.3 | Condition: 3.81 / Grade: 6.81
  3. **98001:** 96 listings | Median Price: $224k | Social Score: 59.9 | Condition: 3.50 / Grade: 6.96

### H3: Timing & Seasonality Analysis
* **Hypothesis:** Buying in the winter months (Dec–Feb) offers a 5–8% price discount compared to the peak summer season (May–Jul).
* **Finding:** **Confirmed.** The peak season median price is **$465,000**, dropping to **$430,000** during winter, with an annual low of **$426,000** in February.
* **Result:** A statistically verified **7.5% price reduction**, translating to approximately **$15,000 – $18,000 in direct capital savings** for Thomas's budget tier.
* **Visual Integrity:** Visualized using an honest zero-based Y-axis to prevent artificial slope exaggeration and preserve objective data reporting.

---

## Actionable Recommendations for Thomas Hansen

1. **Target 3–4 Bedrooms:** Focus searches on 3–4 bedroom configurations to maximize available inventory while remaining within budget.
2. **Focus on Top 3 Zip Codes:** Prioritize properties in **98023**, **98042**, and **98001** for the highest supply and favorable lot-density metrics.
3. **Time the Purchase in Winter:** Enter negotiations and submit offers between **December and February** to capture the ~7.5% seasonal discount.
4. **Accept Necessary Trade-Offs:** Target homes built between 1960–1980 with construction grades 6–7; allocate seasonal savings toward essential cosmetic repairs and moving costs.

---

## Data Limitations

* **Single-Year Horizon:** Dataset covers sales only from May 2014 to May 2015; true multi-year seasonality cannot be completely decoupled from annual macro trends.
* **Inventory Constraints:** While winter provides favorable pricing, overall market listings decline during colder months, limiting total simultaneous choices.
* **Proxy Metrics:** "Social neighborhood" is estimated using neighborhood lot sizes (`sqft_lot15`) due to the absence of public transit, school district, and crime rate features in the dataset.


---

## Repository Structure

```text
├── 04_eda.ipynb                     # Master notebook combining data prep, H1, H2, and H3
├── 08_H1.ipynb                      # Hypothesis 1: Bedroom distributions and pricing
├── 08_H2.ipynb                      # Hypothesis 2: Geographic filtering, zip code selection, and social scores
├── 08_H3.ipynb                      # Hypothesis 3: Seasonality, timing analysis, and zero-based visual
├── cleandataset.csv                 # Cleaned King County dataset
├── pyproject.toml / uv.lock         # Project dependencies managed via uv
└── README.md                        # Project documentation and summary
