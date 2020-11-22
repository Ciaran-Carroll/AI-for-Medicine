# AI for Medicine - Course 2: AI for Medical Prognosis

## Week 2: Prognosis with Tree-based models

In the second week, we will build machine learning models with decision trees. We will use trees to model nonlinear relationships, which are commonly observed in medical data and apply them to the prognostic task of predicting mortality that is the chance of a patient dying. 

In practice, when we train machine learning models, one of the key challenges is how to handle missing data. We'll learn about a few ways of dealing with missing data in your machine learning pipelines. 

### Tree-based models 
*Decision Trees (DTs)* are a non-parametric supervised learning method used for classification and regression. Decision trees learn from data to approximate a sine curve with a set of if-then-else decision rules. The deeper the tree, the more complex the decision rules and the fitter the model.

Decision tree builds classification or regression models in the form of a tree structure. It breaks down a data set into smaller and smaller subsets while at the same time an associated decision tree is incrementally developed. The final result is a tree with decision nodes and leaf nodes. A decision node has two or more branches. Leaf node represents a classification or decision. The topmost decision node in a tree which corresponds to the best predictor called root node. Decision trees can handle both categorical and numerical data.

Reasons to use decision trees in medical applications:
- able to handle both continous nd categorical data
- interpretability
- and the speed at which we can train them

We will use trees to model nonlinear relationships, which is observed in medical data. And of course, we will build our first machine learning tree based models for the prognostic task of predicting short-term mortality for hospital patients. 

#### Decision trees and Random forests
Random Forests, a powerful classifier, that builds many decision trees to further improve predictive performance. Random forests have become a very popular out of the box learning algorithm, that has good predictive performance with relatively little tuning.

<b>How to fix overfitting with decision trees?</b> Depth max

Test if the decision tree is overly complex by looking at its performance on another set of data.

Overfitting occurs when the model fits the training data so closely that it doesn't generalise well to other samples or the real world. 

One way that we can combat overfitting is to control when we stop growing the trees. We can stop growing decision trees by setting the maximum depth a tree can grow to. 

Another popular way to combat overfitting is to build what's called a random forest. Random forests construct multiple decision trees and average their risk predictions. 

There are two key concepts in the training of a random forest: 

1. each tree in the forest is constructed using a random sample of the patients. 
2. the random forest algorithm also modifies the splitting procedure in the construction of decision trees such that it uses a subset of features when creating decision boundaries. 

With these two key concepts, a random forest algorithm learns to build multiple decision trees on given data. Random forest generally boost the performance over single trees.

Random forests are called an ensemble learning method because they use multiple decision trees to obtain better predictive performance than could be obtained from any of the decision trees alone. There are other popular algorithms that use ensembles including Gradient Boosting, XGBoost, and LightGBM which are also able to achieve high performance when working with structured data in medicine and in other domains

### Survival Data
In this lesson, we'll talk about survival data. In order to be able to model survival, we need to be able to represent the data in a form which we can process. The primary challenge is sensor data, which is a particular form of missing data that we'll look at. The missing data is common and an important issue to address while working with healthcare data.

<p align="center"><image src="Images/Recap%201.png"/></p>

New Test data got low performance is due to the distributions of data is different.

### Identifying missing data
Types of missing data:
- Missing data completely at random - the missingness is not dependent on anything.
- Missing data at random - the missingness is not dependent a condition (eg. over 40).
- Missing data not at random - the missingness is dependent on unavailable information.

Dropping missing data can lead to a bias model.

### Using imputation to handle missing data
Imputation means replaces missing data with an estimated value based on other available information. 

Types of imputation:
- Mean imputation
- Regression imputation

In mean imputation, we first look at all the observable values in our data set and we simply average them. 

Regression imputation has the opposite problem of mean imputation. A regression model is estimated to predict observed values of a variable based on other variables, and that model is then used to impute values in cases where the value of that variable is missing. Some regressive models might include using 'y = mx + c' to find relationship in the data to estimate the missing data.

<p align="center"><image src="Images/Recap%202.png"/></p>
