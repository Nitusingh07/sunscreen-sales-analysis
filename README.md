# sunscreen-sales-analysis

Comprehensive Excel analysis of sunscreen market trends (Jan 2024 – Jul 2025) using data collected from Flipkart listings.

This repository contains the data, cleaned assets, exploratory analysis, summary outputs, and recommendations aimed at informing a product launch or portfolio decision for a sunscreen product (target launch: 2025). The analysis focuses on brand performance, price and rating trends, SPF distribution, pack sizes, and other attributes surfaced from online listings.

## Table of contents

- Project summary
- Data description
- Folder layout
- Analysis overview (data cleaning, EDA, methods)
- Key findings (high-level insights)
- Recommendations for launching a sunscreen product in 2025
- How to reproduce (Excel-focused instructions)
- Data limitations and assumptions
- Contract & success criteria
- Next steps and optional extensions
- License and contact

## Project summary

This is an Excel-first market analysis project that inspects Flipkart sunscreen listings from January 2024 through July 2025. The objective is to: identify market trends, brand winners, SPF and formulation patterns, pricing bands, and product features that correlate with higher ratings and visibility — and then translate those findings into actionable recommendations for launching a new sunscreen.

Key takeaways you can expect from this repository:
- Cleaned dataset(s) ready for pivots and charts
- Standardized fields (brand, SPF, price, ratings, pack size, product type, claims)
- Exploratory charts and summary tables (brand share, price distribution, SPF distribution, seasonality)
- Concise recommendations for product positioning, price, SPF target, and marketing approach

## Data description

- Source: Flipkart product listings scraped for sunscreen category (public-facing listing attributes such as brand, product title, price, rating, num_reviews, product description, SPF, and pack size).
- Time range: Jan 2024 – Jul 2025
- Types of fields (typical):
  - id / sku / url
  - brand
  - title
  - price (numeric, currency cleaned)
  - rating (numeric)
  - num_reviews (numeric)
  - spf (extracted numeric value when present, e.g., 30, 50)
  - product_type (e.g., lotion, gel, spray)
  - claims (e.g., 'non-greasy', 'water resistant')
  - pack_size (ml / g)
  - scraped_at (date)

Note: Because this is an Excel project using scraped listings, not all listings include every attribute (e.g., some items do not explicitly list SPF in the title or description). See the Limitations section for details.

## Folder layout

Repository top-level folders (what you'll find here):

- `raw data/` — original scraped exports (CSV / Excel) as collected from Flipkart.
- `cleaned data/` — cleaned and standardized datasets used for analysis (format suitable for Excel pivots and charts).
- `output/` — pivot tables, charts, summary tables, and final CSV/Excel summary files generated during the analysis.
- `PPT/` — presentation slides summarizing the analysis and recommendations.
- `DASHBOARD SCREENSHOT/` — screenshots or images of dashboards or Excel charts used in the story.

Files you should look for first:
- `cleaned data/` — open the cleaned workbook(s) to start exploring the pivots and charts.
- `PPT/` — the slide deck provides a narrative view of key insights and recommended actions.

## Analysis overview

Work performed (step-by-step):

1. Data ingestion
	- Collected raw listing exports from Flipkart (one or more CSV/XLSX files) covering Jan 2024–Jul 2025.
2. Standardization & cleaning
	- Normalized brand names (merged common misspellings and case differences).
	- Extracted numeric SPF values from title/description strings and created an `spf` column.
	- Converted price fields to numeric values in a single currency and removed non-numeric characters.
	- Parsed and standardized pack sizes (ml / g) into a numeric `size_ml` field where possible.
	- Handled missing / null values: kept a record of rows with important missing attributes for sensitivity checks.
3. Enrichment (light)
	- Derived price per ml, price band (cheap / mid / premium) for comparative analysis.
4. EDA and visualizations (Excel)
	- Brand market share by count of listings and by average rating.
	- Price distribution and median price by brand and SPF band.
	- SPF distribution and share by brand and product type.
	- Ratings vs price, and ratings vs SPF analyses to detect correlations.
	- Time-series/seasonality checks using `scraped_at` (monthly volume and average price trends).
5. Output
	- Pivot tables, charts, and a slide deck summarizing the insights and go-to-market recommendations.

## Key findings (examples — please verify in the `PPT/` and `output/` for exact numbers)

- Brands with the highest listing volume often occupy the low-to-mid price band. High average rating brands may have fewer SKUs but higher price points.
- SPF distribution commonly clusters around SPF 30 and SPF 50; premium SKUs commonly advertise higher SPF or additional claims (PA++++ / broad spectrum).
- Price per ml varies widely across product types (sprays often cheaper per ml, premium lotions command higher per-ml price).
- Ratings moderately correlate with price and number of reviews — higher-priced items that invest in marketing/reviews often show higher ratings.

These are high-level findings; exact statistics and charts appear in `output/` and `PPT/`.

## Recommendations for launching a sunscreen product (2025)

The recommendations below synthesize observed listing patterns and competitive positioning. Tailor them to your brand, manufacturing costs, and distribution strategy.

1. SPF & claims
	- Target SPF 50 as a primary SKU: SPF 50 appears frequently and is perceived as a premium / high-value offering in many markets.
	- Add clear broad-spectrum and PA ratings if possible; list 'non-greasy' and 'fast-absorbing' claims prominently (these cluster with higher ratings in some segments).
2. Packaging & sizes
	- Offer a 50 ml travel-size and a 100 ml daily-use SKU. Price per ml analysis shows consumers buy both convenience and economy packs.
3. Pricing
	- Launch with a mid-premium price band: price slightly above mass-market players but below market-leading premium brands to capture quality-conscious buyers.
	- Use introductory discounts and bundles to drive initial review volume (reviews were a strong correlate of ranking and purchase intent in the data).
4. Distribution & marketing
	- Prioritize Flipkart listing optimization (high-quality images, standard keywords, explicit SPF/PA labeling, verified reviews).
	- Advertise with sampling or influencer seeding to increase review counts quickly; review counts and good ratings strongly influence visibility.
5. Product claims and formulation
	- Emphasize non-oily / quick-absorbing formulations for urban, daily-use consumers; consider a mattifying formulation for oily skin.
6. Metrics to monitor
	- Listing impressions & conversion (if available), average rating, number of reviews, price per ml, churn of SKUs, and month-over-month listing velocity.

## How to reproduce (Excel-first instructions)

Follow these steps to reproduce the core analysis using the files in the repository:

1. Open `cleaned data/` workbook(s) in Excel.
2. Refresh or create pivot tables using these suggested pivot configurations:
	- Brand vs count of SKUs (rows: Brand; values: Count of id)
	- Brand vs average rating (rows: Brand; values: Average of rating; filters: price_band)
	- SPF vs count (rows: spf; values: Count of id)
	- Price band vs average price per ml (rows: price_band; values: Average of price_per_ml)
3. Create charts from pivot tables (bar charts for distributions, line charts for monthly trends).
4. For time-series: group `scraped_at` by Month in the pivot to produce monthly trend lines for listing counts and average prices.
5. If you prefer Python for reproducibility, export cleaned CSVs from `cleaned data/` and run analyses in a notebook (not provided here but easy to add).

Tips for Excel:
- Use Data -> Text to Columns and simple formulas (e.g., REGEXEXTRACT if using newer Office365) to extract SPF from titles.
- Create a calculated field for price_per_ml = price / size_ml.

## Contract (inputs / outputs / error modes)

- Inputs: raw scraped listing files from Flipkart (CSV/XLSX). Expected fields: brand, title, price, rating, num_reviews, description, scraped_at.
- Outputs: cleaned dataset(s) in `cleaned data/`, pivot tables and charts in `output/`, and a summary slide deck in `PPT/`.
- Error modes: missing SPF in many titles, inconsistent brand naming, price strings with non-numeric characters, missing size information.

Success criteria for this analysis:
- Cleaned dataset with normalized brand and numeric price/size/SPF fields.
- Reproducible Excel pivot tables that generate the charts in `output/`.
- Concise recommendations in `PPT/` that are supported by at least one data-driven chart in `output/`.

## Edge cases & limitations

- Scraped listing data is not the same as sales data: listing counts do not equal velocity or revenue.
- Some attributes (SPF, size, claims) are inconsistently reported and may require manual verification.
- Ratings and review counts can be biased by promotion and review solicitation — interpret correlations carefully.
- Market dynamics change rapidly; data until July 2025 may not capture late-2025 shifts in competitive behavior or supply-chain changes.

## Next steps (optional extensions)

- Collect sales or rank data (if available) to move from listing-level insights to demand estimation.
- Add a Python or R notebook for reproducible EDA and automated report generation.
- Build a small dashboard (Power BI / Tableau / Excel) for interactive filtering by brand, SPF, and price band.
- Run sentiment analysis on reviews/descriptions to extract common positive/negative themes.

## How I verified changes

- This README is authored to summarize and synthesize the work stored in this repository: cleaned datasets, outputs, and slides. For numbers and plots, consult the files in `output/` and `PPT/` for the precise charts used to draw recommendations.

## License

See `LICENSE` at the repository root for license details.

## Contact

If you want changes to this README, more thorough reproducible scripts (Python/R), or assistance converting the Excel analysis into an automated pipeline, open an issue or contact the repository owner.

---

Generated/updated: 2025-10-30

