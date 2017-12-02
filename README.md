# The Simpsons

As The Simpsons embark's on it's 29th season in a month's time (a seaons during which it will surpass Gun Smoke's record-holding 635 episodes) I took the opportunity to look at how the quality (or at least the IMDb score) has evolved throughout the show's nearly three decade run. 

## Voting

To fully understand the IMDb ratings, we will look who was submitting these votes in an effort to give some context to the scores. Scraping the user data for each episode proved quite difficult, so instead we will look at the [demographic breakdown for the series overall](http://www.imdb.com/title/tt0096697/ratings?ref_=tt_ov_rt_).

The series is mostly voted on by Males aged 18-45, with the 30-45 portion being the demographic that likes the show the best (they rate it 8.9/10) and the 18-29s rate the series the same as the overall (8.8/10). Men & Women under 18 make up less than half a percent of the total votes (we will come back to this later) though they still rate it 8.7, but the group that rates the show the lowest is Women 45+ who give it a measly 7.9/10.

So we understand the demographic groups that are doing the most voting, but how has the macro-view voting population changed over the show's run?

![ep_votes_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_votes_plot2.png?raw=TRUE)

We notice a clear downward trend, which amounts to the show losing 2 votes every episode. This is likely a result of the [show's decreasing audience](https://en.wikipedia.org/wiki/The_Simpsons#Reception_and_achievements), but probably also a factor of the show's nearly 30-year run meaning the early episodes have been replayed more (and thus have been seen and voted-on more) than recent ones.

## Scoring

The average episode score is 7.4 with a standard deviation of 0.75. This contrasts with the 8.8/10 rating for the series overall, which makes it the 54th highest rated show on IMDb. Seeing as the opinion of an average episode is significantly lower than of the series overall, we get our first hint that the show's quality hasn't been consistant. As most Simpsons fans will tell you, the show's quality has ebbed and flowed over the years, so let's see if the IMDb scores reflect this. 

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plot.png?raw=TRUE)

Early growth, a peak, a drop, and a plateau: the IMDb ratings mimic the decline in viewers is real to imply that the quality of the show has decreased from it's peak (this is the point where Simpsons fans DM me saying "DUH!"). This shape helps explain why so few Under 18s, have watched the show: since they were mature enough for the program it has been of quite low quality. But when was it it's best? Searching Google one can find endless pages of "Top X Best/Worst Simpsons Episodes", so let's settle it the best way we know how, by the numbers.

We see that the most highly-rated episode is the episode ["Homer's Enemey"](http://simpsons.wikia.com/wiki/Homer%27s_Enemy), which is about an outsider pointing out the absurdities in the show's premise. It serves as a nod of self-awarness to the audience as well as a reminder to it's [obsessive fans](https://deadhomersociety.com/2010/08/02/animation-showcase-homer-goes-to college/) that it's just a show. This episode would not make my top 10, but fans evidently like the show taking a break from wacky adventures and looking inwards. Other episodes with ratings above 9.0 include ["You Only Move Twice"](http://simpsons.wikia.com/wiki/You_Only_Move_Twice) where Homer is unknowingly hired by a Bond Villain, ["Treehouse of Horror V"](http://simpsons.wikia.com/wiki/Treehouse_of_Horror_V) the fifth Halloween special, and ["Who Shot Mr. Burns? Part One"](http://simpsons.wikia.com/wiki/Who_Shot_Mr._Burns%3F_(Part_One)) a murder mystery where everyone in town is a suspect. We note that all these episodes are between seasons 5 through 9, and that they all have a zscore of over 2.

On the other end of the spectrum, the lowest-rated episode is the Season 23 ["Lisa Goes Gaga"](http://simpsons.wikia.com/wiki/Lisa_Goes_Gaga) with a 4.3/10, which features Lady Gaga helping Lisa with her self esteem. Other low-rated episodes include ["All Singing All Dancing"](http://simpsons.wikia.com/wiki/All_Singing,_All_Dancing) a musical episode, and an episode where [Moe's washrag tells it's life's story](http://simpsons.wikia.com/wiki/Moe_Goes_from_Rags_to_Riches). These episodes have a zscore in the range of -2 to -4.

We note that the zscores for the worst episodes are larger (in magnitude) than the best episodes. With 600+ episodes you're bound to have a few stinkers; what I'm trying to study here is less a few crummy scripts, but more how the show has evolved. One of the most pieces of the show's evolution is the peak, also known as "The Golden Age".


## Golden Years

The exact beginning and ending of the "Golden Age" is a hotly debated topic amongst fans, but it is usually thoght of as starting around season 2 or 3 and ending around season 11 or 12 ([here is one artist's opinion](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/1467480120160.jpg)). This "Golden Age" corresponds to the peak we saw in the plot of IMDb scores, but how do quantify when it started and when it ends? 

![avg_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/avg_rating_plot.png?raw=TRUE)

Seasons 2-8 have an average rating of above 8.0, season 1 & 9-16 averages are above 7.0, and seasons 17-28 are in the range 6.5-7.0. We decide, somewhat arbitrarily, to cut off the "Golden Age" at an average score of 8.0, which gives us seasons 2 through 8. 

These 6 seasons is when then show was in peak form, still finding it's footing before, and the show losing it's edge after. But how does quality fluctuate during this period?

![gold_rate1](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate1.png?raw=TRUE)

The trend curve shows that the IMDb score doesn't fluctuate that much during the "Golden Age", the difference between the max and min of the regression is less than 2/5 of a point (with a linear regression this difference shrinks to 0.07 points). Lastly, the average "Golden Age" episode rating is 8.2, which has a zscore just above 1 compared to the series average of 7.4. So it seems the "Golden Age" is real, the show did have 6 seasons where the episodes were fairly consistent in quality. 

## Treehouse of Horror

On the topic of higher-than-average quality, The Simpson's annual "Treehouse of Horror" episodes are some of my personal favorite episodes, and with Halloween only a couple weeks away, what better time to find out if these episodes are truly great, or I'm clouded by the fun of the spooky atmosphere.

For the past 27 Halloweens The Simpsons has aired a triplet of shorts that pay homage to, or parody, films, television shows, literature, EC Comics, and of course episodes of [The Twilight Zone](https://www.youtube.com/watch?v=SFokFDyDGgs). These episodes allow the writers to break the show's [canon](https://en.wikipedia.org/wiki/Canon_(fiction)) and imagine the characters in new ways, but with all the fantastic animation, keeping it inline with the show's atmosphere, and keeping the gore to censor-satisfying levels they often end up being quite difficult and stressful for the staff<sup> [4] </sup>. However, these are some of the most fun episodes, and the insane skills of the animators and writers are showcased as they raise the bar year after year.

The Treehouse of Horror (ToH) episodes score slightly above average with a mean of 7.6 compared with the series 7.4, the "Golden Age" ToH episodes average 8.5, compared with the 6-season average of 8.2. The season-normalized scores tell us that the Halloween specials are 4% better than an average episode that season. 

As we saw earlier is "Treehouse of Horror V", which is rated 9.1, is one of the series highest scoring episodes, but the worst ToH episode, and the only installment with a score lower than the season's average, is the 22nd installment of the Halloween special, which scores 6.6, with a zscore of -1 for the series, and -0.2 for that season. 

So the Treehouse Episodes seem to be a bit, but not significantly, better than average episodes. This makes sense in hindsight, as they are still a product of the season's staff, and likely don't get *that* much more attention than other episodes. 
