# Predictive Modelling Using Social Profile in Online P2P Lending Market
It is very important that borrowers pay the loans. We study the borrower-,loan- and group- related determinants of performance predictability in an
online P2P lending market by conceptualizing financial and social strength to predict borrower rate and whether the loan would be timely paid. We tried to create a model that determines the risk of the debt using the given data.
## Dataset Structure
Original dataset contains 113,937 loans with 81 variables on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, and many others. Our label is LoanStatus. 
The data was offered by Technocolabs for a project . You can find it here : https://raw.githubusercontent.com/Technocolabs100/Predictive-Modelling-Using-Social-Profile-in-Online-P2P-Lending-Market-CODETCS56EA/main/prosperLoanData.csv?token=GHSAT0AAAAAABWHOOFHA6AN2UVIEHGP2WDCYX2GTGQ
## Data Assessing and Cleaning
We can use histograms and barplots to get an idea of how some of the key variables are distributed
![image](https://user-images.githubusercontent.com/82694608/184637852-d253ba0a-3e63-422b-afca-2629a73eeaae.png)
The median income of potential borrowers is pretty healthy at $56,000/year. The median credit score is pretty close to 700, and in fact almost half (~47%) of the records have a credit score of 700 or higher. Mind, this is using the lowest credit score reported, as given by the variable CreditScoreRangeLower. The median interest, at 18.4%, seems really high but since the loans are typically for relatively short terms (see below) it might turn out to be not too onerous on borrowers. A $6,500 loan (the median amount requested) at 18.4% paid over 3 years will pay about $2,000 in interest in addition to the principal.

Variables related to credit utilization: 

![image](https://user-images.githubusercontent.com/82694608/184637980-9ae308a3-8341-4102-907a-1e8a886d072b.png)
![image](https://user-images.githubusercontent.com/82694608/184638193-c1c3b430-f2ad-4145-89f4-4482041002fa.png)

About 75% of loans are 3-year loans. Similarly, about 75% of applicants have no delinquencies on their current accounts, which we would expect, and about 75% of them have had their credit pulled two or fewer times in the last 6 months. Home ownership is evenly split among applicants.

We dropped variables which haven't effect for result like Memberkey , loankey and other. Moroever,I also dropped some columns that similar to others because of we found high correlation between Propesrating (alpha) Propesrating (numeric) and Propescore columns which contains  98% similarity. we kept Propesrating (numeric) and filled this columns missing values with GreditGrade variables. we decided to drop columns which have more than 40
% nan values due to it was tough to fill this columns mising values. As as result, 56 columns was leaved from 81.

## Predictors
We  based our choice of predictors based on several factors.One is our familiarity with the data we expect income and credit score to be good predictors of a borrower’s ability to repay a loan. We will leave out predictors that are likely to be heavily correlated with another we did include.
We also used ExtraTreesClassifier to see which features are more important for our label
![image](https://user-images.githubusercontent.com/82694608/184638917-17836380-2cba-4fd8-8dc2-99540c460cdd.png)

Term:The length of the loan expressed in months.
Prosper Score:A custom risk score built using historical Prosper data. The score ranges from 1-10, with 10 being the best, or lowest risk score.
Occupation:The Occupation selected by the Borrower at the time they created the listing
Employment Status Duration:The length in months of the employment status at the time the listing was created.
EmploymentStatus:The employment status of the borrower at the time they posted the listing.
Amount Delinquent:Dollars delinquent at the time the credit profile was pulled.
Debt To Income Ratio: The debt to income ratio of the borrower at the time the credit profile was pulled.
Loan Current Days Delinquent:The number of days delinquent. 
Loan Original Amount:The origination amount of the loan.
LP Customer Principal Payments:Pre charge-off cumulative principal payments made by the borrower on the loan. 

## Model Building
Metrics considered for Model Evaluation
Accuracy , Precision , Recall and F1 Score

Accuracy: What proportion of actual positives and negatives is correctly classified?

Precision: What proportion of predicted positives are truly positive ?

Recall: What proportion of actual positives is correctly classified ?

F1 Score : Harmonic mean of Precision and Recal

Random Forest Classifier

The random forest is a classification algorithm consisting of many decision trees. It uses bagging and features randomness when building each individual tree to try to create an uncorrelated forest of trees whose prediction by committee is more accurate than that of any individual tree.
Bagging and Boosting: In this method of merging the same type of predictions. Boosting is a method of merging different types of predictions. Bagging decreases variance, not bias, and solves over-fitting issues in a model. Boosting decreases bias, not variance.
Feature Randomness: In a normal decision tree, when it is time to split a node, we consider every possible feature and pick the one that produces the most separation between the observations in the left node vs. those in the right node. In contrast, each tree in a random forest can pick only from a random subset of features. This forces even more variation amongst the trees in the model and ultimately results in lower correlation across trees and more diversification.

## Deployment
### Heroku
We create django web application and We deploy our app to Heroku.com. In this way, we can share our app on the internet with others. We prepared the needed files to deploy our app sucessfully:

Procfile: contains run statements for app file and setup.sh.

setup.sh: contains setup information

requirements.txt: contains the libraries must be downloaded by Heroku to run app file successfully

RF_model.pkl : contains our RandomForestClassifier model that built by modeling part.


https://fast-badlands-61570.herokuapp.com/

