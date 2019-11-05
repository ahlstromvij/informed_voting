# Two Models of Informed Voting

This repository contains a Jupyter Notebook with two multinomial logistic models, used to simulate how people in the UK would vote in a UK General Election, were they fully informed. The models are based on a British Election Study data set (Fieldhouse et al. 2018) from a face-to-face, post-election survey using an address-based random probability sample of eligible voters living in 468 wards in 234 Parliamentary Constituencies in England, Scotland, and Wales, for a total sample of 2,194 respondents. The full data set can be accessed at https://www.britishelectionstudy.com/data-object/2017-face-to-face/.

The notebook is in six sections, as follows:

## 1. Data Preparation
This section reads in the (cleaned up) data and recodes a number of ordinal and nominal variables. The one-hot-encoding of the latter makes clear their keys; for the remaining variables, keys are included in comments, and also in the `pandas_profiling` summary at the top of the section. The section also generates the train and test sets for the two models: a demographic model which, as the name suggests, only contains demographic variables; and an EU vote model, that also includes how people voted in the 2016 EU referendum.

## 2. Two Multinomial Logistic (Softmax) Models
This section fits the two multinomial models above on the BES data, using `LogisticRegression` from Scikit-Learn, and also makes a prediction on one observation from the data set for purposes of illustration, as well as plots the result.

## 3. Model Evaluation
This section calculates the log loss for the two models. We see two things: first, both models perform better than two dumb models, used as benchmarks. Second, the more complex model has a lower log loss (although not by a wide margin), which makes sense given that how people voted in the EU referendum vote is likely a highly predictive variable. However, as far as model selection is concerned, this fact should be interpreted with care, and here's why: 

The simulations in the next section in effect model a counterfactual: how each observed individual would have voted, were they fully informed. For several highly predictive variables - e.g., how they would've voted in the EU referendum - those variables might have taken on different values, were the individuals involved more informed (i.e., they might have voted differently and held different views). For that reason, there's a case for not including them in the model, and for going for the demographic model in particular. That's also what we do in Section 4.

## 4. Simulation of Fully Informed (Reported) Vote
This section simulates the fully informed (reported) preference for a single individual, by way of illustration. The maximum ability value is identified and ascribed to that individual, at which point the (revised) probability distribution across the electoral options (including abstaining) are calcuated, using the demographic model. Finally, that distribution is plotted graphically, to visualise it.

## 5. Difference Between Actual and Fully Informed Vote
One way to look directly at individual-level information effects is by comparing a person's actual vote with the probabilities ascribed to her across all electoral options, as given by the model. That's what's done in this section, again for the first observation, by way of illustration. That difference is also plotted, to visualise the difference.

## 6. Aggregate Difference Between Actual and Fully Informed Votes
This section calculates and visualises aggregate information effects by first calculating the distribution of support for the entire sample, calculating the distribution under the assumption of a fully informed sample, and finally plots both of those distributions, as well as their difference, to visualise the aggregate information effect in the sample.
