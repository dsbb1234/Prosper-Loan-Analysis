# Prosper-Loan-Analysis
### Investigation Overview This project looks at data for the Prosper Funding, LLC, a company linking investors to people in need of personal loans. The loans are unsecured. Prosper does not fund the loans themselves. Prosper offers a way to have multiple investors fund individual loans by providing a piece of the funding. Investors are able to view individual loans on their website, see details regarind the total amount the borrower is requesting, view the identified loan risk and borrower APR. According to their website, the typical return on investment is about 5.3%. (This information was obtained on Prosper's website: https://www.prosper.com)

When initially looking at the data, I noticed the dataset provided information regarding loans that are charged off. I am choosing to focus this analysis on loans that are charged-off and what factors may be present in that subset of loans.

As this data was not part of a randomized experiment, findings are not assumed to have causality.

### Dataset Overview
The dataset contains 113,937 rows of data and 81 columns of information, including borrower information, credit rating, amount borrowed, Loan Annual Percentage Rate (APR), information about loan losses, loan status, number of investors and loan funding and was provided to Udacity in support of the Data Analyst Nanodegree Program (Source: https://www.google.com/url?q=https://s3.amazonaws.com/udacity-hosted-downloads/ud651/prosperLoanData.csv&sa=D&ust=1554486256021000).

The dataset included the Prosper Loan Data in a .csv file and a data dictionary (Source: https://www.google.com/url?q=https://docs.google.com/spreadsheet/ccc?key%3D0AllIqIyvWZdadDd5NTlqZ1pBMHlsUjdrOTZHaVBuSlE%26usp%3Dsharing&sa=D&ust=1554486256024000).  

### Prosper Data Set Structure

There are 113,937 rows of data, consisting of 3 boolean variables, 32 floating variables, 27 integer variables, 5 date/time, and 13 object variables. The data provides information about the borrower, including credit scores, number of outstanding loans, location of the borrower and member information Key Financial metrics related to the loan , including Borrower APR, Amount Borrowed, Monthly Loan Payments
Metrics related to borrower fiscal health, including account inquiries, number of missed payments and Information regarding number of investors, investment from friends, amount invested, and percent funded to name a few.

### Data Wrangling
Using a variety of data wrangling techniques, we evaluated the file, discovering a number of opportunities to improve the quality and tidyness of the data.  The following issues were found with the Prosper data set:

#### Quality Issues
* ListingNumber should be object
* ListingCreationDate should be type "datetime "
* ClosedDate should be "datetime"
* ProsperRating should be int64
* LoanOriginationDate should be datetime
* ProsperRating (Numeric) and ProsperRating (Alpha) have spaces in the variable names. Remove the spaces and parentheses. Use underscores.
* EmploymentStatusDuration should be int64 rather than float64.
* CreditScoreRangeLower and CreditScoreRangeUpper should be int64 rather than float64.
* FirstRecordedCreditLine should be datetime.
* TotalProsperLoans, TotalProsperPaymentsBilled, OnTimeProsperPayments, ProsperPaymentsLessThanOneMonthLate and ProsperPaymentsOneMonthPlusLate should be int64.
* LoanNumber should be string.
* TotalTrades, TradesOpenedLast6Months should be int64.
* CurrentCreditLines, OpenCreditLines, TotalCreditLinespast7Years, CurrentDelinquencies, PublicRecordsLast7Years, PublicRecordsLast10Years, and PublicRecordsLast12Months should be int64.
* DateCreditPulled should be datetime.
* ListingCategory (numeric) should be a category and eliminate the parentheses. Remove the numeric and replace the values with the categories they actually represent( 0 - Not Available, 1 - Debt Consolidation, 2 - Home Improvement, 3 - Business, 4 - Personal Loan, 5 - Student Use, 6 - Auto, 7- Other, 8 - Baby&Adoption, 9 - Boat, 10 - Cosmetic Procedure, 11 - Engagement Ring, 12 - Green Loans, 13 - Household Expenses, 14 - Large Purchases, 15 - Medical/Dental, 16 - Motorcycle, 17 - RV, 18 - Taxes, 19 - Vacation, 20 - Wedding Loans)

#### Tidyness Issues
* Remove ProsperRatingNumeric as ProsperRatingAlpha contains the category information

 Using a combination of programmatic and manual techniques, the data was cleaned and saved as loan_master.csv. 

### Main features of the dataset, driving my interest

I first became interested in the chargeoff category when conducting an initial look at the loan status. Chargedoff is the third largest category, behind loans that are current and those that completed. I am particularly interested in diving into loan chargeoff and in identifying what other factors are present in customers who's loans resulted in chargeoff.

### Plan to approach analyzing the data
There are a number of variables in the dataset that can support the investigation. We can start by looking at the status of each loan, seeing which loans have the largest categories. We can look at the types of loans that exist in the chargeoff category. We can look at the distribution of data in that category. We will examine the relationship between variables using bivariate and multivariate analysis.

## Summary of Findings

The following findings were identified in the dataset.  They are separated into univariate, bivariate, and multivariate:

### Univariate Exploration

The following items were of interest:
* The distribuion of Original Loan Amounts in the charge-off category appears to be fairly left skewed, with most of the loans falling below $10,000 per loan.
* There were a number of loans at the higher APRs at 30, approximately 35 and around 38 percent.
* Current is the largest loan status category. Completed loans are the next largest category. The borrowers of these loans have completed their payments back to Prosper and their investors. The third largest category is Chargedoff and is the area of study in this analysis.
* Approximately $100M in loan amounts that were chargedoff.
* The largest group of loans that resulted in chargeoff were in the "Not Available" category (not assigned to a particular category). It was followed by Debt Consolidation, Business Loans, Other and Home Improvement.

Prosper's rating system identifies the level of risk associated with a loan in that rating category on an annual basis: AA = 0 - 1.99%, A = 2.0 - 3.99%, B = 4 - 5.99%, C = 6 - 8.99%, D = 9 - 11.99%, E = 12 - 14.99%, and HR = >= 15.00%. Rating D has the largest amount of loans. A and AA rated loans are the smallest group that received loans.
Looking on Prosper Loan's website, current APRs for the loan categories are as follows (depending on term of loan): AA - 5.99 - 8.73% A - 10.88 - 12.68% B - 13.02 - 17.10% C - 16.32 - 25.63% D - 21.24 - 30.08% E - 26.00 - 34.74% HR - 31.72 - 35.97%

* The largest number of chargeoffs appear to have occurred in California, followed by Florida, Georgia, Illinois, Texas, New York, Maryland, Ohio, Michigan and North Carolina (in descending order).
* The largest number of loans appear to be in the $5,000 and lower category.
The distribution of original loan amounts in the chargeoff category appears to be left skewed and may appear to be multimodal.
* Performing the log10 transformation, we were able to see the distribution appeared multimodal.
* The distribution of Borrower Annual Percentage Rate also appears to be multimodal, with higher count of loans at 30%, around 35% and around 38% annual percentage rates.

I decided to do a log transformation on the data to see if the Loan Original Amount was approximately log normal distributed. If I reduced the bins to 7, Original Loan Amount appears to be log normally distributed, however, if I use a larger number of bins (14), the diestibution appears to be multimodal. I believe that the smaller number of bins hides characteristics of the data and that the distribution is multimodal. This will be explored further in the bivariate exploration using Loan Origination Amount and looking at loan type.

### Bivariate Exploration

It was interesting to see:
* Loans that ended in chargeoff did not seem to have a much larger Borrower APR than other categories of loans. 
* Borrowers with a Prosper Rating of D, E or HR were more likely to have loans resulting in chargeoff.
* The violin plots of Original Loan Amount by Listing Category confirmed that number of the listing categories are skewed and multimodal for Original Loan Amount. Left skewed categories include all of the categores except Green Loans, Baby/Adoption and Boat. Green Loans and Baby/Adoption are multimodal, but, not left or right skewed. Boat appears to be right skewed.
* For the most part, the majority of the loans appear to be for less that $10,000.
* Boat Loans, Wedding Loans, Business, Debt Consolidation seemed to be the listing categories with the larger loans that were charged off.
* The majority of loans falling into chargeoff had extremely high interest rates. In most of these categories, the interquartile range was in excess of 20% Annual Percentage Rate. This is consistent with what we observed on Prosper's website: https://www.prosper.com/loans/rates-and-fees/?refac=CANMB&refmc=6YRANV&refd=prosperblog.
* The  interquartile range seems to be shifted slightly lower for Borrower APR in the chart showing showing all categories of loans, however, there is not a significant shift. 
* Looking at the interquartile ranges for Borrower APR by Prosper Rating, Loan Risk (also known as Prosper's borrower Risk Rating) is the primary factor in determining what Borrower APR is assigned to the loan.
* The largest group of chargeoff loans is for those who are identified as employed, followed by those identifed as working full-time.
* Within the employed and full-time categories, the D rating appears to be the highest. E and HR also appear to be high in almost every loan category for loans that resulted in chargeoff.

Did you observe any interesting relationships between the other features (not the main feature(s) of interest)?
Initially I was wondering if loans had a different interest rate by category, but, that did not seem to be the case. Looking at violin and box plots of loans by listing category, the distributions did not seem to be visually significantly different, sending me to look for another cause. It is clear from the Box Plot of Prosper Rating and Borrower APR that the level of Borrower Risk identified Prosper determines where the Borrower APR is likely to be set.

### Multivariate Exploration

The following findings were of revealed as a result of this investigation:
* The Annual Percentage Rate is higher for smaller loan sizes. Also, there is an decrease in variability of the interest rate as the size of the loan increases.
* Borrower APR appeared to increase in all categories from 2007 to 2011. It appeared to decline after 2011 decline for all but 2 categories of employment status (Not Employed and Part Time). Employed and Retired appear to have been added as employment status categories in 2010. Also, Emloyment Status appears to not have been tracked as separate categories prior to 2007.

The following iteractions between features were interesting:

* Prosper Score and Borrower APR are negatively correlated, meaning as the Prosper Score decreases, the Borrower APR increases. The strength is considered moderate. A correlation is considered as moderate if the correlation is greater than 0.4 and less than 0.7.
* Lender Yield and Borrower APR have a very strong positive correlation.
* Lender Yield also has a strong positive correlation with Estimated Loss.
* Credit score has a negative correlation to Borrower APR and the strength is very weak. A correlation is considered very weak if it is less than 0.3 and none as it approaches 0.0.
* The Prosper Score has a slightly larger positive correlation to Credit Score (Upper and Lower), but at 0.318, it is considered Weak.
* There is a strong positive correlation between Estimated Loss and Lender Yield, meaning we expect to see a higher loss at the higher lender yield.
* It is also interesting that the total number of investors in a loan tends to fall between less than 50 and 150. The highest number of investors appears in the 13% to 27% Lender Yield and at an estimated loss between 5 to 10%.
* It is also interesting that a number of investors were willing to invest in a loan with an estimated loss greater than 35% at a lender yield of approximately 34%.

## Key Insights for Presentation

This analysis focused on Prosper loans that resulted in charged-off and what factors may be present in that subset of loans.

We hope to answer the following questions:

1) Where does chargeoff fall in the loan status categories?
2) What types of loans fall within the chargeoff category.  What are the largest loan types?
3) What Borrower Risk loans have falling in the chargeoff category?
4) How does the Borrower's Annual Percentage Rate correspond to Borrower Risk?
5) How does the Borrower's Employment Status correspond to Borrower Risk?
6) How do Prosper Score, Borrower APR, Credit Score interact with each other?
7) How does Estimated Loss, Lender Yield and the number of investors interact with each other? 

## Key Findings:

Chargeoffs represent the third largest loan status category, behind Current and Completed. This group represents about 8% of all Prosper Loans. The largest group of loans that resulted in chargeoff were in the Not Available category (not assigned to a particular category). It was followd by Debt Consolidation, Business Loans, Other and Home Improvement. Boat Loans, Wedding Loans, Business, Debt Consolidation seemed to be the listing categories with the larger loans that were charged off.

Prosper Risk Rating D has the largest amount of loans, followed by C, E and B (in descending order). AA rated loans are the smallest group that received loans. These loans have the lowest risk.

Risk is the primary factor in determining what Borrower APR is assigned to the loan. The AA Prosper Rating has the lowest risk and has a median interest rate near 10%. As risk increases, so does the median interest rate. The highest interest rates were assigned to the HR category. The majority of Borrower Annual Percentage Rates for loans falling into the chargeoff status fell between 10% and approach 40%.

The largest group of chargeoff loans is for borrowers identified as employed, followed by those identifed as working full-time. Within the employed and full-time categories, the D rating appears to be the highest. E and HR also appear to be high in almost every loan category for loans that resulted in chargeoff.

The study found the following relationships between the numeric variables:

Posper Score and Borrower APR are negatively correlated. The strength is considered moderate.
Borrower APR and Lender Yield have a strong positive correlation.
Lender Yield and Estimated Loss also have a strong positive correlation.
Credit score has a negative correlation to Borrower APR and the strength is very weak. A
The Prosper Score has a slightly larger positive correlation to Credit Score (Upper and Lower), but at 0.318, it is considered Weak.
There is a strong positive correlation between Estimated Loss and Lender Yield, meaning we expect to see a higher loss at the higher lender yield.
It is also interesting that the number of investors tends to fall between less than 50 and 150.
The highest number of investors appears in the 13 % to 27 % Lender Yield and at an estimated loss between 5 to 10%.
It is also interesting that a number of investors were willing to invest in a loan with an estimated loss greater than 35 % at a lender yield of approximately 34 %.
As this data was not part of a randomized experiment, findings are not assumed to have causality.
