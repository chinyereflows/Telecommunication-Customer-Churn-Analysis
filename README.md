# Telecommunication-Customer-Churn-Analysis
End-to-end churn analysis of 18,600+ telecom customer records built entirely in Microsoft Excel. Covers data cleaning in Power Query, customer segmentation, and an interactive two-page dashboard with regional slicers uncovering key churn drivers across tenure, contract type, support calls, and spending tiers.
## Background
A telecommunications business sought to leverage customer data to assess churn behavior, identify at-risk segments, and generate data-driven recommendations to improve customer retention, service quality, and product offerings.
## Business Questions
- What is the overall churn rate?
- Which customer segments are most likely to churn?
- Does tenure affect churn rate?
- What are the key customer demographic and behavioral patterns?
- Which service types are most preferred?
## Tools Used
- Microsoft Excel
- Pivot Tables
- Power Query 
## Dataset Description
This analysis is based on an AI-generated dataset of 20,000 rows and 13 columns, covering the following variables:
Customer ID, Region, Age, Tenure (Months), Contract Type, Internet Service, Payment Method, Monthly Charge, Data Usage, Support Calls, Late Payments, Satisfaction Score, and Churn status.

<img width="1356" height="539" alt="Screenshot 2026-03-20 203316" src="https://github.com/user-attachments/assets/71505500-0958-46a0-baef-1debe6a0b442" />

## Data Preparation
### Data Cleaning
The dataset was loaded into Power Query to begin the ETL (Extract, Transform, Load) process. Each column was examined to understand the nature of its contents and determine the appropriate cleaning procedure.
- Region: Rows with blank region values were removed, as the missing data could not be inferred or derived from existing variables. This step ensured clean geographic segmentation across four regions: West, North, East, and South.
- Age: Missing values were imputed using the column average. Prior to imputation, the data was examined for outliers that could skew the mean. Imputation was chosen over row deletion to preserve dataset size and minimize bias. This was implemented in Power Query using the formula:
  =if [age] = null then List.Average(List.RemoveNulls([age])) else [age]
- Contract Type: Inconsistent text entries were corrected using the Replace Values function. "Month to Month" was standardized to "Month-to-Month" to ensure consistency for accurate grouping and analysis.
- Internet Service: Similar text standardization was applied "fiber" was corrected to "Fiber" to maintain consistent categorization.
- Monthly Charge & Satisfaction Score: Blank cells in both columns were filled with their respective column averages to preserve dataset size and ensure complete records for analysis. This was implemented using the formula:
  =if [monthly_charge] = null then List.Average(List.RemoveNulls([monthly_charge])) else [monthly_charge]
### Feature Engineering
Conditional columns were created to group customers into meaningful segments for analysis:
- Tenure Group (based on tenure in months)
  - 1–12 months: New Customer
  - 13–24 months: Early Stage
  - 25–48 months: Established
  - ≥49 months: Loyal Customer
- Age Group (based on age)
  - 18–29: Young
  - 30–44: Middle-Aged
  - 45–59: Older
  - 60–75: Senior
  - 75+: Elderly
- Monthly Charge Tier (based on monthly spend)
  - <$75: Budget
  - $76–$150: Standard
  - $151–$250: High Value
  - $251–$350: Premium
  - $350: VIP
- Data Usage Tier (based on data consumption)
  - <100: Light User
  - 101–300: Moderate User
  - 301–600: Heavy User
  - 601–800: Power User
  - >800: Ultra User
- Satisfaction Rating (based on satisfaction score)
  - 1.0–1.9: 1 Star
  - 2.0–2.9: 2 Stars
  - 3.0–3.9: 3 Stars
  - 4.0–4.9: 4 Stars
  - 5.0: 5 Stars
  
Once all columns were created, the dataset was loaded back into Microsoft Excel via Close & Load into a structured table for further analysis. Duplicates were identified and removed using the Customer ID column as the unique key. After cleaning, 18,638 rows were retained, representing a 6.81% data loss attributable to missing or incomplete records.

<img width="1361" height="538" alt="customer segmentation" src="https://github.com/user-attachments/assets/fd940d75-a016-41e6-b40e-e7bed96a56da" />

## Data Analysis
Exploratory data analysis was conducted using Pivot Tables to uncover trends and patterns across key variables.
Churn rate was calculated using the formula:
Churn Rate = (Inactive Customers ÷ Total Customers) × 100
The following churn dimensions were analyzed: churn by tenure group, contract type, support call volume, satisfaction rating, monthly spend tier, data usage tier, and age group. Customer segmentation analysis was also conducted to profile demographic and behavioral patterns across the customer base.

<img width="1347" height="539" alt="churn analysis" src="https://github.com/user-attachments/assets/370f09b0-609a-449e-a41b-6d6c494a1c3d" />
<img width="1361" height="538" alt="customer segmentation" src="https://github.com/user-attachments/assets/c3ef3b83-6d4e-4f83-9347-411f80d82dcb" />

## Dashboard
A two-page interactive dashboard was built entirely in Microsoft Excel using Pivot Charts, with wireframing completed in Microsoft PowerPoint. Slicers were incorporated to enable dynamic filtering of dashboard results by region, allowing stakeholders to explore churn patterns at a geographic level.

<img width="968" height="519" alt="dashboard churn" src="https://github.com/user-attachments/assets/3654f61e-56f8-41ef-8f7f-39cdc583f138" />
<img width="961" height="518" alt="dashboard churn 2" src="https://github.com/user-attachments/assets/200ec48c-784b-4ee7-9cde-8a9bd2283393" />

## Insights, Observations, and Recommendations 
### Overall Churn Rate
The telco recorded an overall churn rate of 8%, indicating that 1 in 12 customers has switched to a competitor or discontinued service — a meaningful retention challenge that warrants strategic intervention.
### Churn by Tenure
Loyal customers recorded the highest churn rate at 9.03%, making them the most at-risk segment on a proportional basis, a counterintuitive finding that suggests long-term customers may be experiencing unmet expectations or have been overlooked by retention efforts. Established customers, despite carrying the lowest churn rate at 7.64%, recorded the highest absolute volume of churned customers. Given their tenure length, each lost established customer likely represents a significant revenue impact, making this segment a dual priority for both investigation and proactive retention.
### Churn by Contract Type
Month-to-month customers churn at 12.14%, compared to 1.39% for one-year and 1.07% for two-year contract holders — making them approximately 9x more likely to churn than one-year customers and 11x more likely than two-year customers. This sharp disparity confirms that contract length is a strong predictor of retention, as longer commitments create switching friction and reflect higher upfront customer investment. The business should prioritize converting month-to-month customers to longer-term contracts through targeted incentives such as discounted annual plans or loyalty rewards, as even a modest shift in contract mix could materially reduce overall churn.
### Churn by Support Call Volume
Churn rate escalates sharply with support call frequency — 3.88% for customers with 1–2 calls, 14.66% for 3–5 calls, and 46.84% for those with 6 or more calls. This strong correlation identifies unresolved or recurring service issues as a critical churn driver. It is worth noting that causality may run in both directions: poor service quality may increase call volume, but highly dissatisfied customers already intending to leave may also reach out more frequently before churning. Regardless of direction, customers logging 3 or more support interactions represent a high-risk cohort requiring proactive intervention. The business should investigate whether elevated call volumes reflect systemic product issues, service gaps, or complaint resolution failures — and establish an early warning system to flag and engage at-risk customers before they reach the critical threshold.
### Churn by Monthly Spend Tier
Churn rate demonstrates a clear inverse relationship with monthly spend — declining from 8.94% for standard customers to 6.25% for premium and 0% for VIP customers. Since budget and standard-tier customers constitute the majority of the customer base, their elevated churn rates represent the greatest volume of lost customers and the highest aggregate revenue risk. This pattern suggests that lower-spend customers are more price-sensitive and more susceptible to competitive offers. The business should explore targeted retention strategies for these tiers, including loyalty incentives, personalised offers, or competitive pricing adjustments. The 0% VIP churn rate is a notable finding that warrants further investigation — understanding the factors driving VIP loyalty, whether service quality, product value, or relationship management, could yield a replicable retention model applicable across lower tiers.
### Customer Segmentation Overview
Middle-aged and young customers constitute the largest share of the customer base, reflecting a predominantly working-age demographic that is likely digitally active and responsive to data-driven engagement strategies. Moderate and light data users account for 63.53% and 33.97% of the customer population respectively, together representing nearly the entire base and suggesting that heavy or ultra data offerings may be underutilised. Budget and standard-tier customers dominate the spending distribution, while VIP customers represent the smallest segment — reinforcing the earlier finding that the lower-spend majority carries the greatest retention risk by volume.


Analysis conducted in Microsoft Excel using Power Query for data preparation and Pivot Tables for exploratory analysis. Dashboard developed natively in Microsoft Excel.
