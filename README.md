# B2B Marketplace Scraper & EDA

![Colab Badge](https://colab.research.google.com/assets/colab-badge.svg) [![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

End-to-end project scraping and analyzing data from IndiaMART Export (B2B marketplace). Focuses on 3 product categories: **Industrial Machinery (CNC Machines)**, **Electronics (Mobile Phone Accessories)**, and **Textiles Machinery**. Uses pre-fetched real data (30 listings) for robustness and ethics—avoids live scraping blocks while demonstrating ETL + EDA.

## Overview
- **Part A (Data Collection)**: Manually fetched 30 listings (USD prices, company details, export locations) from IndiaMART's export portal. Structured as JSON/CSV for modularity.
- **Part B (Exploratory Data Analysis)**: Pandas for stats, Seaborn/Matplotlib for visuals. Uncovers price distributions, regional trends (USA dominance), and keyword patterns.
- **Key Insights** (from EDA):
  - **Pricing**: CNC/Textiles avg ~$10K+ USD (high-value industrial) vs. Accessories ~$5 USD (volume consumer). Outliers in machinery suggest custom exports.
  - **Exports**: USA in ~80% listings—hypothesis: Strong US-India trade post-2025 deals.
  - **Keywords**: 'machine' (20x), 'textile' (8x), 'mobile' (8x)—signals sector focus.
  - **Anomalies/Gaps**: ~7% null prices (quote-only); no ratings (future: Profile scraping). 28/30 records clean post-ETL.

## Project Structure
```
b2b-marketplace-scraper/
├── B2B_marketplaces.ipynb          # Runnable notebook: Data load + full EDA
├── scraped_data.csv                # Raw data (30 records)
├── scraped_data.json               # Raw data (JSON format)
├── scraped_data_clean.csv          # Cleaned data (28 records, numeric prices)
└── full_eda_visuals.png            # 9 EDA charts (boxplots, heatmaps, etc.)
```

## Files
- **`B2B_marketplaces.ipynb`**: Core notebook. Loads data, runs stats/visuals. Outputs CSVs/PNG.
- **`scraped_data.csv/json`**: Raw exports (product_name, price, company, location list, url).
- **`scraped_data_clean.csv`**: Processed (dropped nulls, numeric conversions).
- **`full_eda_visuals.png`**: Combined plots: Price boxplots by category, export bars, keyword trends, correlations.

Sample Data Preview (Cleaned CSV head):
| category                | product_name                          | price   | company                          | location                  | url                                      |
|-------------------------|---------------------------------------|---------|----------------------------------|---------------------------|------------------------------------------|
| CNC Machine             | Best In Class CNC Machines            | 21560.77| Monotech Engineers Private Limited| ['USA', 'Nepal', 'Sri Lanka']| https://export.indiamart.com/...id=...  |
| CNC Machine             | Nesting CNC Router Machine            | 23807.63| Jai Industries                   | ['USA', 'Nepal', 'Sri Lanka']| https://export.indiamart.com/...id=...  |
| Mobile Phone Accessories| Metal Embossed Mobile Phone...        | 5.67    | Ravi Exports                     | ['USA', 'UK', 'Canada']    | https://export.indiamart.com/...id=...  |

## How to Run
### In Google Colab (Recommended)
1. Open [B2B_marketplaces.ipynb](https://colab.research.google.com/github/abhishekspaswan/b2b-marketplace-scraper/blob/main/B2B_marketplaces.ipynb).
2. Run all cells (Runtime > Run all)—no extra setup.
3. Download outputs: Files panel > Right-click CSVs/PNG.

### Locally (Jupyter/VS Code)
1. Clone repo: `git clone https://github.com/abhishekspaswan/b2b-marketplace-scraper.git`.
2. Install deps: `pip install pandas matplotlib seaborn lxml`.
3. Open notebook: `jupyter notebook B2B_marketplaces.ipynb`.
4. Run cells—generates files in current dir.

**Expected Outputs**:
- Console: Stats tables (e.g., avg price $9,845 USD).
- Files: Updated CSVs/JSON + PNG with 9 plots (e.g., violin densities, scatter correlations).

## Tech Stack
- **Language**: Python 3.12.
- **Data**: Pandas (ETL, stats).
- **Visuals**: Matplotlib/Seaborn (9 charts: boxplots, bars, violins, pie, heatmap).
- **Ethics**: Pre-fetched (manual export)—respects ToS; limited to top results per category.

## Challenges & Extensions
- **Robustness**: Pre-fetch handles 403 blocks; modular class for live scraping (add Selenium).
- **Creativity**: 3 categories for multi-faceted analysis; keyword mining via regex/Counter.
- **Future**:
  - Live scraper: Integrate requests/BeautifulSoup with proxies.
  - Advanced: NLP (NLTK for sentiment), ML (price prediction via scikit-learn).
  - Pipeline: Airflow for ETL scheduling.

## License
MIT License—feel free to fork/use. See [LICENSE](LICENSE) (add if needed).

**Author**: Abhishek Paswan (@abhishekspaswan). Questions? Open an issue or DM on GitHub/X. Star if helpful! ⭐
