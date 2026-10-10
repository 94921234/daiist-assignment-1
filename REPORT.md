# Assignment 1 Report

*Delete this italic guidance as you fill in each section. You'll be asked to
defend any of this without your code in front of you — write only what you
can actually explain.*

- **Name**: Ignacio Ascanio Aliño
- **Student ID**: 18719
- **Email**: iascanio.ieu2022@student.ie.edu
- **Group**: [BBADBA 5B]

## Dataset

I chose the Bank Marketing dataset from the UCI Machine Learning Repository. It contains information from direct marketing campaigns conducted by a Portuguese bank, mainly through phone calls, with the goal of getting customers to subscribe to a term deposit.

I am using the bank-additional.csv version, which has 4,119 rows and 21 columns. Each row represents a customer contact during a marketing campaign. There are 20 input features, including customer information (age, job, education), previous marketing interactions, and economic indicators. The last column, y, is the target variable, indicating whether the customer subscribed to a term deposit (yes or no).

I chose this dataset because I am interested in finance and wanted to work on a realistic banking problem. It also contains both numerical and categorical variables, which makes it interesting for feature engineering and preprocessing. Finally, the dataset is small enough to train multiple models efficiently while still being large enough to compare their performance.

## Business / real-life framing

I am working as a data analyst for a bank that wants to make its marketing campaigns more efficient. Instead of calling every potential customer, the bank wants to identify which customers have a higher probability of subscribing to a term deposit. This could help the marketing team prioritize customers, reduce unnecessary calls, and potentially increase the return on its campaigns.

The target variable is binary: 1 if a customer subscribes and 0 if they do not. Therefore, I used logistic regression to predict the probability of subscription.

Since the bank needs to make predictions before contacting customers, I excluded `duration`, which measures how long a call lasted. Including it would create data leakage because that information would not be available when deciding whom to call.

I split the dataset into 70% training, 15% validation, and 15% testing, using stratified sampling to preserve the proportion of subscribers and non-subscribers. Although a chronological split would better represent future campaigns, the smaller dataset does not contain complete dates, making this difficult. This is a limitation of my approach.

For evaluation, I compared accuracy, precision, recall, F1-score, and ROC-AUC against a naive baseline. Since the dataset is imbalanced, I focused on precision and recall rather than accuracy alone.

I also evaluated different decision thresholds using hypothetical assumptions of €5 per call and €50 per successful subscription. I selected a threshold of 0.10 because it maximized the estimated net value on the validation set among the thresholds tested. These financial estimates are illustrative and do not establish the causal impact of making a call.

## Data preparation & feature engineering

During data exploration, I found that the dataset had no standard missing values (`NaN`), but several categorical features contained `"unknown"`. Instead of removing those observations, I kept `"unknown"` as a separate category to avoid losing potentially useful data.

I also discovered that `pdays = 999` indicates no recorded previous campaign contact, rather than 999 actual days. To represent this information more clearly, I created four features:

- **`previously_contacted`:** Indicates whether `pdays` is different from 999.
- **`days_since_previous`:** Preserves actual days since previous contact, replacing 999 with 0.
- **`has_previous_contacts`:** Indicates whether the customer has any recorded previous interactions (`previous > 0`).
- **`has_any_loan`:** Indicates whether the customer has at least one confirmed housing or personal loan.

I removed the original `pdays` column after transforming it and excluded `duration` to prevent data leakage. I also used `StandardScaler` for numerical features and `OneHotEncoder` for categorical features, fitting both transformations only on the training set.

To evaluate the impact of feature engineering, I compared logistic regression using the original features against the engineered features on the same validation set. The engineered model improved accuracy from **89.97% to 90.29%**, recall from **22.06% to 25%**, and F1-score from **0.3261 to 0.3617**.

Although these improvements were relatively small, they suggest that the engineered features helped the model identify more potential subscribers. I therefore kept them in my final model.

## Modeling: three implementations, one model

*Which model (linear or logistic regression) and why. A results table
comparing scikit-learn, the manual PyTorch loop, and the standard
torch.nn.Module/torch.optim workflow, on the same test set, against the
naive baseline. Do the three agree? If not, why not?*

## Limitations & next steps

*Real limitations you found, and concretely how you'd address each one with
more time or data — not generic hedging.*

## Generative AI use disclosure

*Per the syllabus AI Policy: what you used and how, or "no AI content used."*
