# Telecom Churn Retention Proof of Concept

Machine-learning proposal for "Company A", an anonymous telecom operator (GCI World 2026 Winter final assignment).

**Idea:** customers whose handset is about 300 days old or older leave far more often (56.3% vs 39.4%). Rank customers by churn risk and offer the riskiest 20% a handset upgrade before they leave, with a 10% holdout group to measure the real effect.

## Key results (30,000 held-out customers)
| Model | Accuracy | AUC |
|---|---|---|
| Majority-class guess | 0.504 | 0.500 |
| Logistic Regression | 0.598 | 0.635 |
| Random Forest | 0.620 | 0.674 |
| XGBoost (tutorial baseline) | 0.636 | 0.694 |
| **XGBoost (engineered features)** | **0.639** | **0.697** |

- Contacting the top 20% by risk reaches 30% of all leavers (lift 1.49x).
- Illustrative impact: about $242k net profit per 100,000 customers vs $65k for random targeting.
  This uses **assumed** inputs (35% margin, 15% offer success, $15 per contact, 12 months retained); ARPU ($58.47) comes from the data.
- Caveat: the dataset has about 50% churn, far above real monthly telecom churn, so a pilot A/B test is recommended first.

## Project layout
```
churn_retention.ipynb   full analysis: EDA, features, 5 models, business case
figures/                charts exported by the notebook
data/telecom/           put Client.csv and Record.csv here (not included)
requirements.txt
```

## Run it
```bash
pip install -r requirements.txt
# copy Client.csv and Record.csv into data/telecom/
jupyter notebook churn_retention.ipynb
```

## Data
The two CSV files come from the course and are not included in this repository.

## References
- STL Partners, "Telco economics: The price of loyalty" https://stlpartners.com/research/telco-economics-the-price-of-loyalty/
- "Customer Churn in Mobile Markets: A Comparison of Techniques", arXiv:1607.07792
- Profit by Pakistan Today, 20 Jan 2026 https://profit.pakistantoday.com.pk/2026/01/20/pakistans-mobile-subscriber-base-tops-200-million-by-end-of-2025-pta-data-shows/
- PhoneWorld, June 2026 market share https://www.phoneworld.com.pk/jazz-telenor-lose-mobile-market-share-as-zong-and-ufone-gain-in-june-2026/
- GCI World 2026 Winter tutorial notebook (course material)

Built with assistance from Claude (generative AI); analysis can be reproduced from the notebook.
