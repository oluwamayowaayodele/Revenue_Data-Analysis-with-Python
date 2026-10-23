# Revenue Analysis in Python

**What drives revenue from new users in their first week, and does it differ by gender and country?**

An exploratory and statistical analysis of user activity and revenue data for a consumer product, built in Python. It covers data cleaning, descriptive statistics, visualisation, hypothesis testing and a regression model to predict first-week revenue.

**Status:** analysis and prediction complete; significance of country as a predictor being finalised.

## Data

Two tables, joined on `UserId`:

- **Users:** registration date, date of birth, gender and country.
- **Activity:** daily revenue per user.

After merging, the dataset has 22,642 activity records across 5,797 users.

## Approach

1. **Preparation:** merged the tables, converted date fields to proper date types and checked for missing values.
2. **Data quality:** the null check showed no missing genders, but the `Gender` column contained blank strings. I stripped the whitespace and assigned those records the most common gender (male), following the rule set for the analysis.
3. **Descriptive analysis:** revenue per user, comparing mean and median, plus the shape of the revenue distribution.
4. **First-week revenue:** calculated days since registration for each activity record and isolated revenue from each user's first seven days.
5. **Segment comparison:** average revenue by gender and country, visualised to show where the gender gap is largest.
6. **Hypothesis testing:** checked normality with Shapiro-Wilk before choosing a test. The data is heavily skewed, so I used a Mann-Whitney U test rather than a t-test.
7. **Modelling:** linear regression predicting first-week revenue from gender, age group and country.

## Key findings

| Question | Result |
| --- | --- |
| Female users | 1,412 of 5,797 users (about 24%) |
| Mean vs median revenue per user | Mean 512.69, median 80.00 |
| Average first-week revenue per user | 200.25 |
| Largest male–female revenue gap | US: men average 192.82, women 71.59 (a gap of 121.24) |
| Is the gender difference statistically significant? | **No.** Mann-Whitney U, p = 0.23 at α = 0.05 |
| Predicted first-week revenue for a US woman aged 30–35 | 65.61 (linear regression on gender, age group and country) |
| Is country a significant predictor of revenue? | *In progress* |

## What this means

- **A few users drive most of the revenue.** The mean is more than six times the median, so a small group of high spenders accounts for a large share of the total. Averages alone would overstate what a typical user is worth, which matters for forecasting and for setting acquisition costs.
- **The gender gap looks large but isn't statistically reliable.** Men spend more on average, especially in the US, but across all users the difference isn't significant. It shouldn't drive targeting decisions without more evidence.
- **The gap varies by country.** Men outspend women most in the US, then Germany and the UK. In France the two are roughly equal, and in the "Other" group women spend slightly more. Country-level analysis tells a different story from the overall average.

## Limitations

- Assigning blank genders to the most common value, as the analysis rule required, slightly inflates the male count.
- The revenue distribution is heavily skewed. A linear regression on raw revenue will be sensitive to outliers, so a log transformation or a non-parametric model would be worth testing.
- The data contains no information on product, channel or marketing, which limits how much of the revenue difference can be explained.

## Tools

Python · pandas · NumPy · seaborn · Matplotlib · SciPy

## Files

- `Revenue_Analysis.ipynb`: the full analysis with code, outputs and charts.
