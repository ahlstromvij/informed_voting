# Three Models of Informed Voting

This repository contains a Jupyter Notebook with three multinomial logistic models, used to simulate how people in the UK would vote in a UK General Election, were they fully informed. The models are based on a British Election Study data set (Fieldhouse et al. 2018) from a face-to-face survey using an address-based random probability sample of eligible voters living in 468 wards in 234 Parliamentary Constituencies in England, Scotland, and Wales, for a total sample of 2,194 respondents. The full data set can be accessed at https://www.britishelectionstudy.com/data-object/2017-face-to-face/.

The notebook is in six sections, as follows:

## 1. Data Preparation
This section reads in the (cleaned up) data and recodes a number of factor variables. See the bottom of this document for the variable keys. This section also defines the materials for the three models: a demographic model which, as the name suggests, only contains demographic variables; an EU vote model, that also includes how people voted in the 2016 EU referendum; and an immigration attitude model, that also includes respondents' answer to the question whether too many immigrants have been let into the country.

## 2. Three Multinomial Logistic (Softmax) Models
This section fits the three multinomial models above on the BES data, using `LogisticRegression` from Scikit-Learn, and also makes a prediction on one observation from the data set for purposes of illustration.

## 3. Model Evaluation
This section calculates the log loss for the three models. We see two things: first, each model performs better than two dumb models, used as benchmarks. Second, the more complex the model, the lower the log loss (although not by a wide margin), which makes sense given that the more complex models involve more predictive variables (here: EU referendum vote, and immigration policy attitude). However, as far as model selection is concerned, this fact should be interpreted with care, and here's why: 

The simulations in the next section in effect model a counterfactual: how each observed individual would have voted, were they fully informed. For several highly predictive variables - e.g., how they would've voted in the EU referendum, or their views on immigration - those variables might have taken on different values, were the individuals involved more informed (i.e., they might have voted differently and held different views). For that reason, there's a case for not including them in the model, and for going for the demographic model in particular. That's also what we do in Section 4.

## 4. Simulation of Fully Informed (Reported) Preferences
This sections how to simulate the fully informed (reported) preference for a single individual. The maximum ability value is identified and ascribed to that individual, at which point the (revised) probability distribution across the electoral options (including abstaining) are calcuated, using the demographic model. Finally, that distribution is plotted graphically, to visualise it.

## 5. Difference Between Actual and Fully Informed Vote
One way to look directly at individual-level information effects is by comparing a person's actual vote with the probabilities ascribed to her across all electoral options, as given by the model. This is done in this section, again for the first observation, by way of illustration. That difference is also plotted, to visualise the difference.

## 6. Aggregate Difference Between Actual and Fully Informed Votes
This section calculates and visualises aggregate information effects by first calculating the distribution of support for the entire sample, calculating the distribution under the assumption of a fully informed sample, and finally plots both of those distributions, as well as their difference, to visualise the aggregate information effect in the sample.

## Variable keys
The keys for the factor variables used in the models are as follows:

```
euVote:  
0 = leave  
1 = did not vote  
2 = remain  
  
partyIdentity:  
0 = CONS  
1 = GREEN  
2 = LABOUR  
3 = LIB DEM  
4 = NO PARTY  
5 = PLAID  
6 = SNP  
7 = UKIP  
  
UnionMember:  
0 = no  
1 = yes  
  
income:  
1 = Under GBP 2,600  
2 = GBP 2,600 - GBP 5,199  
3 = GBP 5,200 - GBP 10,399  
4 = GBP 10,400 - GBP 15,599  
5 = GBP 15,600 - GBP 20,799  
6 = GBP 20,800 - GBP 25,999  
7 = GBP 26,000 - GBP 31,199  
8 = GBP 31,200 - GBP 36,399  
9 = GBP 36,400 - GBP 39,999  
10 = GBP 40,000 - GBP 44,999  
11 = GBP 45,000 - GBP 49,999  
12 = GBP 50,000 - GBP 59,999  
13 = GBP 60,000 - GBP 74,999  
14 = GBP 75,000 - GBP 99,999  
15 = GBP 100,000 or more  
  
livingSituation:  
1 = Own home outright  
2 = Own home on mortgage  
3 = Rented from local authority  
4 = Rented from private landlord  
5 = It belongs to a Housing Association  
  
gender:  
1 = male
2 = female  
  
religion:  
0 = no  
1 = yes  
  
age:  
1 = 18-24  
2 = 25-34  
3 = 35-44  
4 = 45-54  
5 = 55-64  
6 = 65-74  
7 = 75-84  
8 = 85+  
  
ethnicGroup:  
0 = asian  
1 = black  
2 = mixed  
3 = other  
4 = white  
  
education:  
0 = No qualification  
1 = Clerical or professional qualification  
2 = GCSE at D or below, or equivalent  
3 = GCSE at C or above, or equivalent  
4 = A-level or equivalent  
5 = HNC/HND  
6 = University/poly diploma  
7 = First degree  
8 = Postgraduate degree  
  
workStatus  
0 = Unemployed/not working  
1 = Retired  
2 = Student  
3 = Part-time  
4 = Full-time  
  
maritalStatus:  
1 = Married  
2 = Living with partner  
3 = Single  
4 = Widowed  
5 = Separated  
6 = Divorced  
  
region:  
0 = East Midlands  
1 = Eastern  
2 = London  
3 = North East  
4 = North West  
5 = Scotland  
6 = South East  
7 = South West  
8 = Wales  
9 = West Midlands  
10 = Yorkshire & Humber 
```
