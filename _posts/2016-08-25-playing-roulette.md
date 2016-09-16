---
layout: post
title: Let's Play Roulette! Comparing 1:1 to 2:1 Betting Strategy
date:   2016-08-25 12:00:00
tag: [statistics, archive, aug-2016]
---
<html>
<head><link rel="stylesheet" href="/css/main.css">
</head>
<body>
<p> I'm going to Vegas soon and one of my all-time favorite betting games is European Roulette. It's a simple game where the dealer spins the wheel and the ball will land on a number. Depending on which number(s) you bet on, you get a certain payout. Of course, the less probable numbers have higher payouts (i.e. betting on a number like 0) and more probable numbers have lower payouts (i.e. betting on all odd numbers)
<div align ="center"><img src="/images/postimages/roulette-board.jpg" id="resp-image"></div>
</p>

<p> Using R, just for kicks, I've simulated 2 scenarios of playing strategies that are frequent among conservative players: 1:1 betting strategy and 2:1 betting strategy (i.e. betting 1st 12 numbers and 2nd 12 numbers). Each scenario consists of 200 spins. <i>Assumptions: It's a fair Roulette wheel and that all spins' outcomes are mutually exclusive of each other. The player will employ the same betting strategy each spin and bet the same amount of money each time.</i>

<h2><u>Scenario 1: 1-to-1 Betting Strategy (Even vs. Odds, Red vs. Black)</u></h2>

<p>When you play red or black, odd or even, remember, the odds aren't quite 50-50 when you play these regions because the house claims "0" so your odds of winning is actually <b>46.37%, <font color="red">not </font>50%.</b> Suppose we bet $15 each spin:</p>
<table style="width:100%">
<tr><td><img src="/images/postimages/prob-win-1-1.png" style="width:90%"></td><td><img src="/images/postimages/runningbal1to1.png" style="width:90%"></td></tr></table>
<p>Yikes! The running total dollar balance of your bets rapidly decrease after the first few spins. There are some positive peaks followed by sharp decline in some cases. It seems in the long run, this is not a very good "winning" strategy at all! </p>

<h2><u>Scenario 2: 2-to-1 Betting Strategy (i.e. 1st 12 & 2nd 12 numbers)</u></h2>

<p>Let's say after losing very badly in Roulette using the 1:1 strategy, you decide to play it safer by playing <b>2:1</b> on <b>2 sets of numbers</b>, with $15 on each set of number. If you win, you win $15. If you lose, you lose $30 this time.

<div align ="center">
<img src="/images/postimages/roulette2to1.png" id="resp-image"></div>
<table style="width:100%">
<tr><td><img src="/images/postimages/prob-win-2-1.png" style="width:90%"></td><td><img src="/images/postimages/runningbal2to1.png" style="width:90%"></td></tr></table>

<p>Note, there are significantly more "positive" peaks than the 1:1 strategy, well into the 150th spin, before the running total balance becomes more negative. Even at a loss, the loss is not nearly as great as the 1:1 strategy (about -$100 vs. -$300). Still, it's not a "winning strategy" in the end. Hypothetically, the player can quit while s/he is on a winning streak, but that's only if s/he quits before s/he loses money again. However, this strategy does seem to have more running steam that the other one.</p> 

<p><b><i>How can we improve upon this betting strategy while still employing a 2:1 strategy? How would results look if the player "doubles" its bet after each loss? </i> </b></p>

<pre><code>
<h1># R Code by Sonya Hua</h1>
<cmt># roulette with 1:1 payout and betting strategy</cmt>

<cmt># simulate the spins 200 times</cmt>
sample.space <- c(1,0)
theta <- (.4637) <cmt>#probability</cmt>
N =200
flips <- sample(sample.space, size = N, replace =TRUE, prob= c(theta, 1-theta))
plot(cumsum(flips) / matrix(1:N),ylim=c(.0,1),ylab="Probability of Winning 1:1 bet", 
xlab="Spins",main="Probability of Winning 1:1 bet in Roulette")
dev.off

<cmt># determine running total $ balance of bets with $15 bets each time </cmt>
amtWon = rep(flips)
amtWon[flips == 1] = 15 <cmt># win $15 </cmt>
amtWon[flips ==0] = -15 <cmt># lose $15 </cmt>
amtWon
amtWon=as.numeric(amtWon)
cumsum(amtWon)
plot(cumsum(amtWon),ylab="Running $ Balance", xlab="Spins", 
main="Running $ Balance with 1:1 Roulette Strategy")

<cmt># roulette with almost 2/3 odds and 2 to 1 payout</cmt>

sample.space <- c(1,0)
theta <- (.3243 + .3243)
N =200
flips <- sample(sample.space, size = N, replace =TRUE, prob= c(theta, 1-theta))
plot(cumsum(flips) / matrix(1:N),ylim=c(.0,1),ylab="Probability of Winning 2:1 bet", 
xlab="Trials",main="Probability of Winning 2:1 bet in Roulette")

amtWon = rep(flips)
amtWon[flips == 1] = 15 <cmt># win $15 for each win </cmt>
amtWon[flips ==0] = -30 <cmt># lose $30 for each loss </cmt>
amtWon
amtWon=as.numeric(amtWon)
cumsum(amtWon) # create a cumulative running total
plot(cumsum(amtWon),ylab="Running $ Balance", xlab="Spins", 
main="Running $ Balance with 2:1 Roulette Strategy")

</pre></code>