Analysis.md


Wallet Score Analysis (ML-based)
After processing ~100K transaction records and assigning wallet-level credit scores, we analyzed the behavior across score ranges and clusters.


Score Distribution Analysis


Overview:
The histogram shows the frequency of wallet scores on the x-axis (Score: 0–1000) and the number of wallets in each score bin on the y-axis.



Key Observations:
Dominant Peak at ~500:
A sharp spike is visible around score = 500.
This suggests that a large number of wallets received a default or base score with minimal variation—likely due to limited transaction activity or neutral behavior.
Over 2,000 wallets fall into this bucket, which might be the result of the base\_score logic assigning 500 as the starting point.



Secondary Cluster around 950–1000:
A notable number of wallets achieved very high scores.
These users likely have strong DeFi behavior: consistent deposits, repayments, and no liquidations.
This group may represent the most trustworthy and active wallets.



Sparse Distribution Below 400:
Very few wallets have scores <400.
This could include wallets that experienced liquidations, borrowed heavily without repaying, or had risky ratios.



Long Tail from 600–900:
There's a gradual spread of scores in the upper-mid range, reflecting a spectrum of responsible behaviors.
These users likely show some positive signs (e.g., repayments, deposits) but not consistently enough to score 900+.



Insights \& Implications:


Base Score Bias:
The scoring function may be heavily influenced by the default base value (500). Consider fine-tuning the base\_score() logic or introducing penalties/incentives earlier in the pipeline.


Model Refinement:
The jump between 500 and other score buckets suggests that the RandomForestRegressor model might be learning a plateau around that point. Adding more granular features could help.


User Segmentation:
This plot supports cluster-based segmentation:
Low-score wallets: Risky or inactive
Middle cluster (~500): Neutral or low-activity
High-score wallets: Reliable DeFi participants



Wallet Count by Score Range (Visual Estimate)
Score Range	   Approximate Wallet Count	Notes
0–100	~10	Almost          negligible
100–200	~15	           Very few
200–300	~15	           Very few
300–400	~25	          Slight increase
400–500	~2200+        Huge spike (peak)
500–600	~300	          Drop after the spike
600–700	~150	          Moderate cluster
700–800	~75	          Fewer wallets
800–900	~40	         Tapering off
900–1000	~300	         Second noticeable concentration





Interpretation


Most wallets (≈ 70–75%) have scores between 400–600, with a strong peak near 500.

A secondary group of high-scoring wallets appears near 900–1000.

Very few wallets are in the 0–300 range, implying few highly risky users.

The distribution suggests a conservative scoring model, where most users land in a mid-range score unless penalized heavily (e.g., liquidation).

