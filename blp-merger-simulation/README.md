# Pizza Delivery Market: BLP Demand Estimation, Merger Simulation, and Regulation Counterfactual

Structural IO analysis of a differentiated-products market. I estimate a random-coefficients logit (BLP) demand and supply model with [`pyblp`](https://pyblp.readthedocs.io/), then use it to measure market power, simulate a four-firm merger, and evaluate a 35-minute delivery-time cap.

## Why this project

Pricing questions such as "what happens to prices if two competitors combine?" or "how much margin does a brand have?" cannot be answered by regression alone, because prices and demand are determined together. This project uses a structural model to recover consumer preferences and firm costs, then re-solves the market equilibrium under new conditions.

## Methods

* **Demand:** random-coefficients logit with price sensitivity interacted with consumer income; price instrumented with BLP-style instruments
* **Supply:** Bertrand-Nash pricing by multi-product firms; marginal cost linear in wages, rating, and delivery time
* **Estimation:** two-step GMM (Halton integration, 50 draws per market)
* **Counterfactuals:** merger simulation (ownership change, re-solved equilibrium) and a regulation scenario (product characteristic change, re-solved equilibrium)

## Key results

| Metric | Result |
|---|---|
| Average own-price elasticity (market 1) | -2.74 |
| Average cross-price elasticity | 0.05 |
| Average markup (Lerner index) | 0.37 (inverse-elasticity benchmark: 0.365) |
| Pre-merger average HHI | 1,884 |
| Merger: change in HHI | +2,576 (all 20 markets become highly concentrated) |
| Merger: markup change, merged firm vs. rivals | +0.087 vs. +0.008 |
| Merger: profit change per product, merged firm vs. rivals | +$6,318 vs. +$15,676 |
| Merger: change in consumer surplus | -$668K per market (about -13%) |
| Delivery cap: price change, capped products | -$0.31 |
| Delivery cap: change in consumer surplus | +$316K per market (about +6%), positive in all 20 markets |
| Diversion to outside good vs. to each rival (market 1) | 50.7% vs. 2.1% |

**Takeaways**

* Demand is elastic, but most lost customers leave the market rather than switch brands.
* Estimated markups line up with the theoretical inverse-elasticity rule.
* The merger raises prices mainly for the merging firm's products, harms consumers in every market, and benefits rivals more than the merging firm (free-riding on the merged firm's price increase).
* A 35-minute delivery cap raises consumer surplus in every market (about +6%), mainly through faster delivery and lower prices, though the cost savings it implies are likely optimistic.

## Repository structure

```
.
├── pizza_delivery_blp_analysis.ipynb   # full analysis with outputs
├── data/
│   ├── products_pizza.csv              # 500 products, 20 markets, 6 firms
│   └── agents_pizza.csv                # 20,000 simulated consumers
├── requirements.txt
└── README.md
```

## How to run

```bash
pip install -r requirements.txt
jupyter notebook pizza_delivery_blp_analysis.ipynb
```

## Notes

* Data are simulated and were provided for a graduate Industrial Organization course (Econ 452, UCLA Master of Quantitative Economics). This project began as a course team project.
* Tools: Python, pyblp, pandas, NumPy, Matplotlib
