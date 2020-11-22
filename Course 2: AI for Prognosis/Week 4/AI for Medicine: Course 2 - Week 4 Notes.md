# AI for Medicine - Course 2: AI for Medical Prognosis

## Week 4: Build a risk model using linear and tree-based models
In week four, you will learn about strategies to build and evaluate survival models that allow you to compare the risks of individual patients. You will learn about two such models, the Cox proportional-hazards model and survival trees. Finally, you'll learn about a way to evaluate the prediction performance of the survival prediction models that you built. 

As we collect larger and larger medical datasets, machine learning will become an invaluable tool to learn the complex relationships and medical data, and to help us answer questions like, why some people survive longer than others? Or what is the patient's 10-year risk of heart attack? 

<b>Hazard fruncion</b>
<p align="center"><image src="Images/Hazard%201.png"/></p>

What's a patient's immediate risk of death if they make it to time t?

So this is what's called the hazard, and the hazard is represented by the Greek letter small Lambda. The hazard of t is the probability that the time to an event is at t, given it is at or after t. 

<p align="center"><image src="Images/iamge%202.png"/></p>

Now, the hazard function can be actually used to create the survival function. They're related, and we won't jump too much into their relationship. But all that's important to understand here is that there is a formula which allows us to go from the hazard to the survival. So we can use that formula to get the corresponding survival curve from the hazard curve. 

Cumulative Hazard - acuumulated hazard or risk up to time t

<p align="center"><image src="Images/Cumulative%20Hazard.png"/></p>

Survival Tree are like binary decison trees that can allow you to build models that capture nonlinear relationships in patient data.

What's thet patient;s accumulated hazard upto time t?

Nelson Aalen estimator - allows us to estimate the cumulative hazard of the population.

<p align="center"><image src="Images/Nelson%20Aalen%20estimator.png"/></p>

with d<sub>i</sub> the number of events at t<sub>i</sub> and n<sub>i</sub> the total individuals at risk at t<sub>i</sub>

Harrell's c-index
<p align="center"><image src="Images/Harrells%20C-index.png"/></p>

you'll learn about the Harrell's concordance index to evaluate the performance of survival models.
