# The Simpsons

As The Simpsons embark's on it's 29th season in a month's time (a seaons during which it will surpass Gun Smoke's record-holding 635 episodes) I took the opportunity to look at how the quality (or at least the IMDb score) has evolved throughout the show's nearly three decade run. 

## Voting

Before we get into how the show is rated, I think it is important to understand who is voting for the IMDb ratings.

First the voting on the series as a whole. [On IMDb](https://www.imdb.com/title/tt0096697/ratings?ref_=tt_ov_rt_) The Simpsons gets an 8.8/10, making it the 54th highest rated series on IMDb. It is mostly voted on by males, who account for 80% of the votes. 30-45 year-old males seem to like the show the best, rating it 8.9. Those under 18 make up less than half a percent of the total votes, though they still rate it quite highly 8.7. The group that gives the show the lowest rating is women 45 years and older, who give it a 7.9/10.

Now the voting by episode. We notice a clear downward trend, which amounts to the show losing 2 votes every episode. This is likely a result of the [show's decreasing audience](https://en.wikipedia.org/wiki/The_Simpsons#Reception_and_achievements), but probably also a factor of the show's nearly 30-year run meaning the early episodes have been replayed more (and thus have been seen and voted-on more).

![ep_votes_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_votes_plot2.png?raw=TRUE)

It's worth noting that decreasing numbers of ratings doesn't mean a decrease in audience, the longer something has been out, the more chance there is for someone to have seen it and thus rate it. So let's investigate how the IMDb rating changed by episode. 

## Scoring

The average episode score on IMDb is 7.4 with a standard deviation of 0.75. This contrasts with the 8.8/10 rating for the series overall. Seeing as the opinion of an average episode is significantly lower than of the series overall, we get our first hint that the show's quality hasn't been consistant. As most Simpsons fans will tell you, the show isn't what it once was, let's see if the IMDb scores reflect this. 

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plot.png?raw=TRUE)

Early growth, a peak, a drop, and a plateau: the IMDb ratings mimic the decline in rating over time seen above. This shape helps explain why so few under 18 have watched the show: during their lifetime, the show has been of much lower quality. But when was it it's best? Searching Google one can find list after list of "Top X Best/Worst Simpsons Episodes", so let's settle it the best way we know how, by the numbers.

We see that the most highly-rated episode is the episode ["Homer's Enemey"](http://simpsons.wikia.com/wiki/Homer%27s_Enemy), which is about an outsider pointing out the absurdities in the show's premise. It serves as a nod of self-awarness to the audience as well as a reminder to it's [obsessive fans](https://deadhomersociety.com/2010/08/02/animation-showcase-homer-goes-to college/) that it's just a show afterall. This episode would not make my top 10, but fans evidently like the show taking a break from wacky adventures to look inwards. Other episodes with ratings above 9.0 include ["You Only Move Twice"](http://simpsons.wikia.com/wiki/You_Only_Move_Twice) where Homer is unknowingly hired by a Bond Villain, ["Treehouse of Horror V"](http://simpsons.wikia.com/wiki/Treehouse_of_Horror_V) the fifth Halloween special, and ["Who Shot Mr. Burns? Part One"](http://simpsons.wikia.com/wiki/Who_Shot_Mr._Burns%3F_(Part_One)) a murder mystery where everyone in town is a suspect. We note that all these episodes are between seasons 5 through 9.

On the other end of the spectrum, the lowest-rated episode is the Season 23 ["Lisa Goes Gaga"](http://simpsons.wikia.com/wiki/Lisa_Goes_Gaga) with a 4.3/10, which features Lady Gaga helping Lisa with her self esteem. Other low-rated episodes include ["All Singing All Dancing"](http://simpsons.wikia.com/wiki/All_Singing,_All_Dancing) a musical episode, and an episode where [Moe's washrag tells it's life's story](http://simpsons.wikia.com/wiki/Moe_Goes_from_Rags_to_Riches). 

With 600+ episodes you're bound to have a few stinkers, but what I'm trying to study here is less a few crummy scripts, but more how the show has evolved. One of the most contentious pieces of the show's evolution is it's peak in quality, dubbed "The Golden Age".


## Golden Years

The exact beginning and ending of the "Golden Age" is a hotly debated topic amongst fans, but the general concensus is that it starts around season 2 or 3 and ends around season 11 or 12 ([here is one artist's opinion](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/1467480120160.jpg)). To quantify the period we can look at the IMDb scores and find the max the peak but how do quantify when it started and when it ends? Let's start by looking at the average score for each season.

Initially I chose the series average of 7.4 as the cutoff for the Golden Age, but I don't think a season being above average captures the idea of the Golden Age. We recall the structure of the show's ratings over time being a rise, peak, fall and plateau. It so happens that seasons 2-8 have an average rating of above 8.0, season 1 & 9-16 averages are above 7.0 but below 8.0, and seasons 17-28 are in the range 6.5-7.0. Since I like whole numbers I'll choose to classify the Golden Age as a season whose average episode score is 8.0 or more. With this criteria we're left with seasons 2-8  being the show at it's peak. 

![avg_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/avg_rating_plot.png?raw=TRUE)

These 6 seasons is when then show was in peak form, still finding it's footing before, and losing it's edge after. But how does quality fluctuate during this "Golden Age"?

![gold_rate1](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate1.png?raw=TRUE)

The trend curve shows that the IMDb score doesn't fluctuate that much during the 6 golden seasons. The difference between the max and min of the regression is less than 2/5 of a point. Lastly, the average "Golden Age" episode rating is 8.2, which has a zscore just above 1 compared to the series average of 7.4. So it seems the "Golden Age" is real, the show did have 6 seasons where the episodes were fairly consistent in quality. 

## Treehouse of Horror

On the topic of higher-than-average quality, The Simpson's annual "Treehouse of Horror" (ToH) episodes are some of my personal favorites, and with Halloween only a couple weeks away what better time to find out if these episodes are truly great or I'm clouded by the fun of the spooky atmosphere.

For the past 27 Halloweens The Simpsons has aired a triplet of shorts that pay homage to, or parody, films, television shows, comics, and of course episodes of [The Twilight Zone](https://www.youtube.com/watch?v=SFokFDyDGgs). These episodes allow the writers to break the show's [canon](https://en.wikipedia.org/wiki/Canon_(fiction)) and write the characters in fantastic situations. 

As we saw earlier "Treehouse of Horror V", which is rated 9.1, is one of the series highest scoring episodes, while the worst ToH episode, and the only installment with a score lower than the season's average, is the 22nd installment of the Halloween special, which scores 6.6.

There are 9 seasons in which the Treehouse of Horror is the highest-rated episode, and only 2 that fall at or below the median. Looking at them as a whole all the ToH episodes have an mean rating of 7.6 (compared with the series mean of 7.4). They are therefore mostly great episodes, but still fluctuate in quality with of the show as it changes through writers and directors. 

![treehouse_boxplot](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/treehouse_boxplot.png?raw=true)



## Conclusion

The Simpsons exploded onto TV's in the late 90's, where it stirred up as much fandom as it did controversy. 28 seasons later it's format and style has been copied so many times it's hard to appreciate how cutting-edge it was. The show is such a staple of our culture that "The Simpsons did it" is a phenomon [pointed out by the show South Park](https://en.wikipedia.org/wiki/Simpsons_Already_Did_It) where writers subconciously copy plot elements from the show and where social media pages posting 20 year-old [screenshots](https://www.instagram.com/thesimpsonsig/) or [quotes](https://twitter.com/SimpsonsQOTD) have hundreds of thousands of followers.

The show has gone through hundreds of writers, animators, show runners, and directors, many of whom have gone on to have great careers (including everyone's favorite [orange-haired late night host](http://1075koolfm.com/wp-content/uploads/2017/05/Conan-1.jpg)). Being such a strong breeding ground for young talent has not afforded long-term staff and losing a large portion of your staff every year certainly doesn't help stability. While constantly losing your best talent makes it difficult to keep your show's quality consistent, I don't think that is the main reason behind the show's decline. 

In my mind The Simpsons was so ground-breaking that it couldn't possibly have stayed that way forever. It was such a popular and influential show that eventually the landscape of television would adjust to it. On top of that, with 600+ scripts in it's wake, it is understandably difficult to create fresh and new ideas with the same old characters. 

However much the quality has dropped and however few fans that remain, it's hard to imagine a day where The Simpsons is taken off the air. A lot of fans complain that it should've been axed a long time ago, but I think they'll shed a tear when (soon) the world's longest running show has it's curtain call. Then again, they may never [stop the simpsons](https://www.youtube.com/watch?v=CZYNwzeqVUA).
