# The Simpsons

As The Simpsons embark's on it's 29th season in a month's time (a seaons during which it will surpass Gun Smoke's record-holding 635 episodes) I took the opportunity to look at how the quality (or at least the IMDb score) has evolved throughout the show's nearly three decade run. 

## Voting

Over 80% of the votes are from Males, with the Male 18-29 and 30-45 year old demographics alone making up almost two thirds of the total votes, while combined Male & Female under 18 demo makes up less than half a percant of the votes (we wil see later that this group discovered the show after it's decline in quality). Men rate the series 8.8/10 while Women rate it 8.6/10. 30-44 years old men give the series a 9.1, the highest rating among all demographics, while Women 45+ give it the lowest rating, a 7.9/10.


![ep_votes_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_votes_plot2.png?raw=TRUE)

We notice a clear downward trend, which amounts to the show losing 2 votes every episode. This is likely a result of the [show's decreasing audience](https://en.wikipedia.org/wiki/The_Simpsons#Reception_and_achievements), but probably also a factor of the show's nearly 30-year run meaning the early episodes have been replayed more (and thus have been seen and voted-on more) than recent ones.

## Scoring

The average episode score is 7.4 with a standard deviation of 0.75. This contrasts with the 8.8/10 rating for the series overall, which makes it the 54th highest rated show on IMDb. Seeing as the opinion of an average episode is significantly lower than of the series overall, we get our first hint that the show's quality hasn't been consistant. As most Simpsons fans will tell you, the show's quality has ebbed and flowed over the years, so let's see if the IMDb scores reflect this. 

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plot.png?raw=TRUE)

Early growth, a peak, a drop, and a plateau: the IMDb ratings mimic the decline in viewers is real to imply that the quality of the show has decreased from it's peak (this is the point where Simpsons fans DM me saying "DUH!"). But when was it it's best? 

With a quick Google search, one can find endless pages of "Top X Best/Worst Simpsons Episodes", so let's settle it the best way we know how, by the numbers.

We see that the most highly-rated episode is the episode ["Homer's Enemey"](http://simpsons.wikia.com/wiki/Homer%27s_Enemy), the premise of which is an outsider pointing out the absurdities in the show's premise. It serves as a nod of self-awarness to the audience as well as a reminder to it's [obsessive fans](https://deadhomersociety.com/2010/08/02/animation-showcase-homer-goes-to college/) that it's just a show. This episode would not make my top 10, but fans evidently like the show taking a break from wacky adventures and looking inwards. Other episodes with ratings above 9.0 include ["You Only Move Twice"](http://simpsons.wikia.com/wiki/You_Only_Move_Twice) where Homer is unknowingly hired by a Bond Villain, ["Treehouse of Horror V"](http://simpsons.wikia.com/wiki/Treehouse_of_Horror_V) one of the classic Halloween episodes (which features homages to ["The Shining"](https://en.wikipedia.org/wiki/The_Shining_(film)) and ["Soylent Green"](https://en.wikipedia.org/wiki/A_Sound_of_Thunder)), and ["Who Shot Mr. Burns? Part One"](http://simpsons.wikia.com/wiki/Who_Shot_Mr._Burns%3F_(Part_One)) a murder mystery where everyone in town is a suspect. We note that all these episodes are between seasons 5 through 9, and that they all have a zscore of over 2 (with respect to the series average).

On the other end of the spectrum, the lowest-rated episode is the Season 23 ["Lisa Goes Gaga"](http://simpsons.wikia.com/wiki/Lisa_Goes_Gaga) with a 4.3/10, which features Lady Gaga helping Lisa with her self esteem. Other low-rated episodes include ["All Singing All Dancing"](http://simpsons.wikia.com/wiki/All_Singing,_All_Dancing) a musical episode, and an episode where [Moe's washrag tells it's life's story](http://simpsons.wikia.com/wiki/Moe_Goes_from_Rags_to_Riches). These episodes have a zscore in the range of -2 to -4 (with respect to the series average & variance). 

We note that the zscores for the worst episodes are larger (in magnitude) than the best episodes. With 600+ episodes you're bound to have a few stinkers; what I'm trying to study here is less a few crummy scripts, but more how the show has evolved. A good place to start is at the show's peak, often refered to as the "Golden Age".


## Golden Years

The "Golden Age" is generally thought of as the period betwen seasons 2 and 10, though this is debated to no end amongst fans. This "Golden Age" corresponds to the peak we saw in the plot of IMDb scores, but how do quantify when it started and when it ends? 

![avg_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/avg_rating_plot.png?raw=TRUE)

Seasons 2-8 have an average rating of above 8.0, season 1 & 9-16 averages are above 7.0, and seasons 17-28 are in the range 6.5-7.0. We decide, somewhat arbitrarily, to cut off the "Golden Age" at an average score of 8.0, which gives us seasons 2 through 8. 

So season 2-8 is when the show was in peak form, with the show still finding it's footing in the first season, and the show losing it's edge after season 8. But how does quality fluctuate during this period?

![gold_rate1](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate1.png?raw=TRUE)

The regression shows that the IMDb score in the "Golden Age" doesn't change that much: the difference between the max and min of the regression are less than 2/5 of a point apart (with a linear regression this difference shrinks to 7/100 of a point). It is worth noting that despite the previous plot showing us that season 5 had the highest average score, the regression peaks at the season 6-season 7 border.

Lastly, the average "Golden Age" episode rating is 8.2. So it seems the "Golden Age" is real, the show did have 6 seasons where the episodes were fairly consistent in quality. 

On the topic of higher-than-average quality, The Simpson's annual "Treehouse of Horror" episodes are some of my personal favorite episodes (remember that Treehouse of Horror V is one of the highest-rated episodes), and with Halloween only a couple weeks away, what better time to find out if these episodes are truly above average, or I'm clouded by the fun of the spooky atmosphere.
