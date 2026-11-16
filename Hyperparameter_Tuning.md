Hyperparameter Tuning and Model Selection

Supplementary Material — AIDEM 2026

Paper: Enhancing Financial Crisis Prediction Using Generative Adversarial Networks

Authors: Mathurin Aime Mekam Pouatcha, Salvatore Rinzivillo, and Francesca Naretto

 # 1. Hyperparameter Optimization Strategy

Hyperparameters were selected exclusively within the 1870–2007 training period using expanding-window, time-ordered cross-validation. In each validation split, the model was trained on earlier years and evaluated on a subsequent, non-overlapping period, ensuring that future observations were not used to predict the past.

All preprocessing operations were fitted separately within each training fold. Model hyperparameters and classification thresholds were selected using only the cross-validation predictions, while the 2008–2020 test period remained untouched until the final out-of-sample evaluation.

# 2. Classification Model Configurations

Support Vector Machine (SVM)

The optimal specification employed a radial basis function (RBF) kernel with a regularization parameter of C = 10 and a scaling parameter determined automatically from the data.

Extreme Gradient Boosting (XGBoost)

The best-performing configuration consisted of:

- Number of trees: 600
- Learning rate: 0.01
- Maximum tree depth: 3
- Subsampling ratio: 0.7
- Column-sampling ratio: 0.7

These subsampling parameters provide additional regularization to reduce overfitting while maintaining predictive accuracy.

LASSO

The optimal specification employed L1-penalized logistic regression with:

- Regularization parameter: C = 10
- Optimization algorithm: liblinear

Logistic Regression (Logit)

The benchmark Logit model was estimated using its standard specification and therefore did not require extensive hyperparameter tuning.

# 3. TimeGAN Hyperparameter Optimization

Given that TimeGAN constitutes the central methodological contribution of this study, additional tuning was performed for the generative model.

A grid-search procedure was conducted across alternative recurrent network architectures, batch sizes, and training horizons.

| Hyperparameter | Configurations evaluated |
|---|---|
| Network architecture | GRU, LSTM-LN |
| Batch size | 32, 64, 128 |
| Training epochs | 100, 1,000, 6,000 |
| Total configurations | 18 |

Among the eighteen TimeGAN configurations evaluated, the specification combining the LSTM-LN architecture with a batch size of 128 and 100 training epochs produced the strongest forecasting performance.

# 4. Selected TimeGAN Configuration

| Hyperparameter | Selected value |
|---|---|
| Architecture | LSTM with Layer Normalization (LSTM-LN) |
| Batch size | 128 |
| Training epochs | 100 |

This configuration was selected as the preferred TimeGAN specification and employed throughout the remainder of the analysis.

# 5. Reproducibility

Hyperparameter selection was conducted using temporally ordered training and validation samples. The out-of-sample evaluation period was excluded from model selection to avoid look-ahead bias.

The configurations documented here correspond to those reported in Section 2.4 of the manuscript.
