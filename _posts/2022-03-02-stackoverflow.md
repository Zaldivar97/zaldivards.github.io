---
layout: post
title: Education and salaries, a stackoverflow perspective
slug: education-and-salaries-a-stackoverflow-perspective
categories: analysis
published: true
related_image: /images/stackoverflow.png
---

Have you ever asked yourself what is the relation between education and salaries in the IT field, is there any incidence? I have.
Nowadays this is very interesting because most of the times a professional degree is often not necessary to reach a developer role in 
the top companies. You, your colleages and I may have different point of views about it. 

But, what do the data suggest about this? To going further with this broad question, I used Stackoverflow’s 2017 Annual Developer Survey.
I checked all the available data within the dataset and I came across with 3 questions that I think it would be interesting to answer.

## 1. What is the relation that has the parents' education on the education and salary of the respondents? 

Here you can see the proportion of respondents with their parents having a certain education. 

![First char](/images/stackoverflow2.png)

More than 60% have a professional degree either it is a bachelor's, master's or doctoral. However is interesting to note that 
High school has almost 16% of proportion.  

This is interesting but does not answer our question. Next, the dataset was aggregated by the parents' education to calculate
the respondents' average salaries based on that.

![Second char](/images/stackoverflow3.png)

As you can see, the parents' education has a clear relation in the respondents' salaries. The respondents present a higher salary 
when their parents have higher education. However, this means nothing about the respondents' salaries based on their education.

To answer this, the dataset was aggregated by the respondents' education to calculate thei avegare salaries based on it. Let's
check this out:

![Third char](/images/stackoverflow4.png)

This is interesting, take a look at the second element in the above chart...the second highest salary, with elementary school only!!
As we thought, a professional degree is often not necessary in the IT field. 

Furthermore, we can conclude that the parents' education has an impact on the respondents' education. Take a look at the below chart to make sure of it. 
The number of respondents with higher degrees(except for the Doctoral degree) is greater than the corresponding number of their parents.

![Fourth char](/images/stackoverflow5.png)

Another topic to take into account when analyzing different salaries is the job satisfaction based on it. So let's dive deeper about it.

## 2. Does overpayment increase the job satisfaction?

Here, three main things were really important to make any conclusion:
- Whether the respondents are overpaid
- Company type
- The importance for them of their functions in relation to their salaries. Specifically, the item in the survey is "*I don't really care what I work on, so long as I'm paid well*".

First, take a look to the job satisfaction based on overpayment answers(in the survey)

![Fifth char](/images/stackoverflow6.png)

Definitely, the people that are overpaid have higher job satisfaction. However, the people that is somewhat underpaid doesn't seem unsatisfied with their job. Furthermore, is interesting to note that the people which is greatly overpaid have a job satisfaction less than the one of the people who are neither underpaid nor overpaid. Could the type of company or the interest in what they work on influence on their job satisfaction?

To answer that I focused on the subset of respondents that are *greatly overpaid*. This is what I found about this subset's job satisfaction based on their **company type** and **the importance for them of their functions in relation to their salaries**:

|Based on company type|Based of functions importance|
|-------------------------|-------------------------|
|![Sixth char](/images/stackoverflow7.png)|![Seventh char](/images/stackoverflow9.png)|

Visuals of the above information

![Seventh char](/images/stackoverflow10.png)

Well, first of all, remember the above aggregates are based only on the data of the respondents who are greatly overpaid.
There's and interest pattern. The companies that have job satisfaction between 6.1 and 6.7 are NGOs or government companies. However we cannot conclude nothing from it, there's no clear evidence and the number of company types is **skewed**:

![Seventh char](/images/stackoverflow8.png)
 
On the other side you can take a look at the answers related with the workPayCare. The people who answered **Strongly disagree** have a job satisfaction of 6.36, the lowest! This means that there's a proportion of respondents within this subset that are not entirely satisfied with their functions within their companies, no matter if they are overpaid.

So, the job satisfaction level of the people who are greatly overpaid **may be** influenced by the work environment. Moreover, the repondents' functions within their companies may have another factor of influence.
