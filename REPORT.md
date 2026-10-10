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

The target variable is binary: 1 if a customer subscribes and 0 if they do not. Therefore, I will use logistic regression to predict the probability of subscription.

Since the bank needs to make the prediction before contacting a customer, I will exclude the duration feature, which measures how long the call lasted. Including it would create data leakage because that information would not be available when deciding whom to call.

For splitting the dataset, I plan to use a stratified train/test split, keeping a similar proportion of subscribers and non-subscribers in both sets. Although a time-based split would be more realistic for predicting future campaigns, the smaller dataset is randomly sampled and does not contain complete dates, making a reliable chronological split difficult. I will acknowledge this as a limitation.

For evaluation, I will focus on precision, recall, and the business cost of incorrect predictions, rather than accuracy alone. A false positive means the bank spends time contacting someone who does not subscribe, while a false negative means missing a potential customer. I will use these trade-offs to choose a decision threshold that balances unnecessary marketing costs against missed subscription opportunities.

## Data preparation & feature engineering

*What you engineered and why, and any data-quality decisions you made along
the way — e.g. "segment X had defective data, so I excluded it and used a
population-average default for scope Y at inference time; the impact of
that choice is Z."*

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
