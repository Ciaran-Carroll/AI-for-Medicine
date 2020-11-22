# AI for Medicine - Course 2: AI for Medical Prognosis

## Week 3: Survival Models and Time
In week three, you learn about survival models. 

Say a patient has a particular type of cancer and you'd like to estimate the probability of their surviving one year or two years, or five years, or even longer. This is when you use a survival model. It allows you to model to time to an event. 

In this case, the patients possible death. These models helped us answer patient questions like, how likely am I to survive the next five years or the next 10 years? Survival models are also used to model the time from treatment to recurrence. So questions like, how likely am I to get a recurrence of this cancer in one-year or in two years. 

### Survival estimates
#### Survival models 
This week we will talk about survival models. Survival models are a special model where we care about the time to the occurrence of an event, such as the time from treatment to recurrence, or the time from diagnosis to death. This is a common question that doctors want to answer for their patients, such as, how likely am I to survive the next five years or the next 10 years? We'll look at how survival models are an extension of the prognostic models we've already looked at. Finally, we will look at how we can use survival data to build the survival models.

#### Survival function
In this lesson, we'll look at at the survival function, a key tool in survival analysis, which will help us answer the probability of survival past anytime t.

- S(t) = Pr(T > t) - the probability that time is greater than some quantity, and that is called the survival function. The survival function is a function that's defined for every time point t. 

<b>What is the probability of survival past any time t?</b>

Right Censoring - the time to event is only known to exceed a certain value (eg. 5+ years).

<b>Kaplan Meier Estimate</b> - allows us to get a survival function that we estimate from a population.

<p align="center"><img src="Images/Kaplan%20Meier.png"></p>

with t<sub>i</sub> a time when at least one event happened, d<sub>i</sub> the number of events (e.g., deaths) that happened at time t<sub>i</sub>, and n<sub>i</sub> the individuals known to have survived (have not yet had an event or been censored) up to time t<sub>i</sub>.

The key thing about this model is that the survival function that we estimate is applied to all the patients in the population, it isn't specific to a particular patient.
