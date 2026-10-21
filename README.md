# Does Rarity Predict Price? A Pokémon TCG Analysis

## The Question

Official card rarity is supposed to signal value — but does it actually predict market price, and does that relationship hold consistent across 25+ years of the game's history? This project analyzes 2,459 cards spanning 11 eras (Base Set through the 2025 Mega Evolution series) to find out.

## Why This Project

Pokémon cards are a genuinely active, high-volume secondary market with messy, real-world data — inconsistent rarity naming across eras, missing prices, multiple currencies, and 25 years of changing game design. It's a good stand-in for the kind of "clean question, messy data" problem that comes up constantly in real analyst work, without relying on an overused public dataset.

## Data Source & Method

- **Source:** [TCGdex API](https://tcgdex.dev) — free, no key required, pulled live via Python.
- **Sample:** 2,459 cards across 11 representative sets, one to two per era, from Neo (2000) through Mega Evolution (2025).
- **Cleaning:** Collapsed 16 raw rarity labels (e.g., "Holo Rare VMAX," "Rare Holo LV.X," "Secret Rare") into a 5-tier ordinal scale (1 = Common, 5 = Top Chase) to make rarity comparable across eras with completely different naming conventions.
- **Pricing:** Used TCGPlayer market price (USD) where available, falling back to Cardmarket average (EUR) for the small number of cards missing TCGPlayer data.
- **Tools:** Python, pandas, matplotlib/seaborn, statsmodels.

## Key Findings

**1. Rarity tier predicts price — but far more weakly than expected.**
A model using rarity tier and illustrator together explained only ~21% of price variation (R² = 0.207). Most of what drives a card's price isn't captured by its official rarity or who drew it.

**2. Rarity's predictive power is dramatically stronger for vintage cards than modern ones.**
A regression testing rarity tier against card age found each rarity tier step is worth **+$25 on average for modern cards, but +$87 for vintage cards (Neo/e-Card/EX era)** — a statistically significant 3.4x difference (p < 0.001). In other words, "Rare" meant something very different in 2000 than it does in 2025.

**3. Vintage "Rare" cards often outvalue modern "Secret Rare" cards.**
A 25-year-old card from the game's basic Rare tier frequently sells for more than a brand-new top-chase rarity — strong evidence that age and scarcity are doing more work than the rarity system itself.

**4. The biggest price outliers are consistently iconic, fan-favorite Pokémon** (Charizard, the original legendary birds, Eeveelutions) — a pattern visible across every tier and era, but one this project deliberately did not attempt to formally quantify, since "popularity" has no clean, objective data source. Left as an open question rather than forced into the model.

## Limitations

- Rarity tier groupings involve subjective judgment calls (e.g., LV.X cards were the top chase rarity in their own era, but were grouped with V/VMAX/Double Rare here for cross-era consistency).
- Price data has extreme skew (a handful of $1,000+ outliers); a log-transformed price model would be a more statistically rigorous next step.
- Only 1-2 sets were sampled per era rather than the full card pool, for practical pull-time reasons.

## How to Run

```bash
git clone https://github.com/DylanDaGoat1/pokemon-tcg-analysis.git
cd pokemon-tcg-analysis
python3 -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
```

Then open `pull_data.ipynb` in Jupyter or VS Code and run all cells.