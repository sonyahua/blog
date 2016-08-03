---
layout: post
title: Parametric vs. Non-Parametric Methods 101
date:   2016-06-09 12:00:00
tag: [statistics, archive]
---

<p>This particular post covers the basics of what people mean when they say <i>parametric </i> or <i>non-parametric</i> statistical methods. If you didn’t initially have a stats educational background (like me), you may have heard these words tossed around by interviewers or folks in the industry, but never had a sit down to learn about it. Today is the day to learn more! </p>

<p><b>Parametric Methods – </b>It is parametric if you make assumptions about the functional form or shape of your statistical model (otherwise known more technically as a function). After validating your assumptions, you estimate the parameters of your model. This is the most common method of elementary statistics. </p>

<p>An example of an assumption is that the model follows a <i>linear regression</i> and <i>normal distribution</i>. Your estimated parameters may be the coefficients in your model such as your beta’s. </p>

<p><b>Non-Parametric Methods –</b> It is non-parametric if you do not make any assumptions about the functional form of your model. You’ll instead estimate the function so it’s a close fit to your data points without being too fitted (a.k.a over-fitted). This allows you to explore many different shapes of your function, but you’ll often need a lot more data points and tweaking of the function in order to accurately estimate your model. </p>

<p>An example of a non-parametric method is <i>Spearman’s rank-order correlation</i> which does not need variables to be normally distributed or linearly related (more on Spearman later). </p>

<p>So which methods are simpler? Usually parametric methods since you’ve reduced the issue to estimating a small set of parameters as opposed to making no assumptions at all. However, there are general trade-offs for both.</p>

<h3>General tradeoffs:</h3>
•	Parametric tend to “over-simplify” the true form of your data.
•	Non-parametric, if fitted too closely to existing data, tends to suffer more when using the model to estimate new observations

•	Parametric can accept a smaller sample size but this introduces lower confidence intervals
•	Non-Parametric needs a larger sample size for higher confidence intervals

•	Both methods are susceptible to overfitting or inaccurate estimates if we over-simplify or over-accommodate the model and its data points
