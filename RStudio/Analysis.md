# Analyzing The Simpson's Quality

Having cleaned the raw IMDb data in Excel, we can bring it into RStudio for analysis, but first we load a couple packages.

```R
install.packages("xlsx") 
install.packages("ggplot2")
require("xlsx")
require("ggplot2")
```

Now we load the xlsx into R as a dataframe.

```R
simp<-read.xlsx("simpsons.xlsx",2)
```

We quickly solidify the order of the seasons as R sometimes factors them weirdly.

```R
simp$season_num<-factor(simp$season_num)
```

The first thing that we wonder is how the IMDb ratings have evolved over the show's 28 seasons? However, since the ratings on IMDb are submitted by users, and knowing about the show's [declining audience](https://en.wikipedia.org/wiki/The_Simpsons#Reception_and_achievements), it is important to look at how the voting for these scores has evolved. 

## Voting

To get an idea of who is voting for the IMDb scores, we will use the breakdown of the voting demographics [provided by IMDb](http://www.imdb.com/title/tt0096697/ratings?ref_=tt_ov_rt_) <sup>[1]</sup>. I will start by looking at the voting by demographic on the series overall, and if I have time I will come back and analyze the changes in demographic by episode.

Males make up over 80% of the ratings, and they rate it an average of 8.8/10, a fifth of a point higher than females. In fact in every age demographic males rate the series higher. Further, males voted over four times more than females. The smallest demographic is the under 18's, who make up less than one percent of the score (this is the group that discovered the show after it's decline). The two groups that voted the most are the male portions of the 18-29 and 30-45 year old demographics, and combined they make up almost two thirds of the votes.

Now that we've seen who is rating the series, let's visualize how the votes per episode changed throughout the series.

![ep_votes_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_votes_plot2.png?raw=TRUE)

The downward trend is probably correlated with the [show's decreasing audience](https://en.wikipedia.org/wiki/The_Simpsons#Reception_and_achievements), but also likely a factor of the shows nearly 30-year run meaning the early episodes have been replayed a lot and thus have been seen more.

Of the ten most-reviewed episodes, seven have a score greater or equal to 9, with two of the exceptions being the series' first two episodes and the third being the first "Treehouse of Horror" Halloween special. Further, all but four of the 15 episodes with a score of 9 and over received more than 2000 votes. These figures hint at a consensus among fans on the best episodes, but in what seasons are they?

## Scoring

The average episode score is 7.4 with a standard deviation of 0.75 <sup> [3] </sup>. Rating the series as a whole it receives an 8.8/10 <sup>[1]</sup> <sup>[2]</sup> which makes it the 54th highest rated show in IMDb. However the mean isn't the whole story as most Simpsons fans will tell you, the show's quality has ebbed and flowed over the years. Let's see if the IMDb scores reflect this. 

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plot.png?raw=TRUE)

Early growth, a peak, a drop, and a plateau. The early episodes hover mostly between 7.5-9, while the later episodes sit in the 6.5-7.5 range. So the IMDb ratings do reflect this 'decline' is real (this is the point where Simpsons fans DM me saying "DUH!"). There are a few distinct regions to this plot, most importantly the peak aka the "Golden Age" (we will come back to this later). First we want to look at the highest highs, and the lowest lows.

With a quick Google search, one can find endless pages of "Top X Best/Worst Simpsons Episodes", so let's settle it the best way we know how, by the numbers.

Oddly enough we see that the most highly-rated episode is the episode ["Homer's Enemey"](http://simpsons.wikia.com/wiki/Homer%27s_Enemy), the premise of which is an outsider pointing out the absurdities in the show's premise. It serves as a nod of self-awarness to the audience as well as a reminder to it's [obsessive fans](https://deadhomersociety.com/2010/08/02/animation-showcase-homer-goes-to college/) that it's just a show. This episode would not make my top 10, but fans evidently like the show taking a break from wacky adventures and looking inwards.

Other episodes with ratings above 9.0 include ["You Only Move Twice"](http://simpsons.wikia.com/wiki/You_Only_Move_Twice) where Homer is unknowingly hired by a Bond Villain, ["Cape Feare"](http://simpsons.wikia.com/wiki/Cape_Feare) a remake of the 1962 film ["Cape Fear"](https://en.wikipedia.org/wiki/Cape_Fear_(1962_film)) where The Simpsons enter a witness protection program after Bart receives death threats from his nemsis Sideshow Bob, ["Treehouse of Horror V"](http://simpsons.wikia.com/wiki/Treehouse_of_Horror_V) one of the classic Halloween episodes (which features homages to ["The Shining"](https://en.wikipedia.org/wiki/The_Shining_(film)) and ["Soylent Green"](https://en.wikipedia.org/wiki/A_Sound_of_Thunder)), and ["Who Shot Mr. Burns? Part One"](http://simpsons.wikia.com/wiki/Who_Shot_Mr._Burns%3F_(Part_One)) a murder mystery where everyone in town is a suspect. We note that all these episodes are between seasons 5 through 9, and that they all have a zscore of over 2 (with respect to the series average).

On the other end of the spectrum, the lowest-rated episode is the Season 23 ["Lisa Goes Gaga"](http://simpsons.wikia.com/wiki/Lisa_Goes_Gaga) with a 4.3/10, which features Lady Gaga helping Lisa with her self esteem. Other low-rated episodes include ["All Singing All Dancing"](http://simpsons.wikia.com/wiki/All_Singing,_All_Dancing) a musical episode, an episode where [The Simpsons go to Jerusalem](http://simpsons.wikia.com/wiki/The_Greatest_Story_Ever_D%27ohed) and Homer defiles various holy sites, and an episode where [Moe's washrag tells it's life's story](http://simpsons.wikia.com/wiki/Moe_Goes_from_Rags_to_Riches). These episodes have a zscore in the range of -2 to -4 (with respect to the series average & variance). 

We note that the zscores for the worst episodes are larger (in magnitude) than the best episodes. With 600+ episodes you're bound to have a few stinkers; what I'm trying to study here is less a few crummy scripts, but more how the show has evolved. A good place to start is at the show's peak, often refered to as the "Golden Age".

## Golden Years

The "Golden Age" is generally thought of as the period betwen seasons 2 and 10, though this is debated to no end amongst fans. First, let's make a new dataframe with all the season's average scores so we can analyze if this so-called "Golden Age" is a reality, or a figment of nostalgia.

```R
#Create a new dataframe to store the average number of ratings for each season
season_avg<-data.frame(season_num=1:28)
for(i in 1:28){
    season_avg$rating[i]<-mean(subset(simp$rating,simp$season_num==i))
}
```

![avg_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/avg_rating_plot.png?raw=TRUE)

We see that seasons 2-8 have an average rating of above 8.0, season 1 & 9-16 averages are above 7.0 and seasons 17-28 are in the range 6.5-7.0. This fits with the widely-accepted idea that seasons 2-8 is where the show was in peak form, with the show still finding it's footing in the first season, and the show losing it's edge after season 8. 

Let's take a closer look at this "Golden Age" of seasons 2-8. 

```R
#Let's create a data frame to make this a little easier
gold_age<-subset(simp,season_num<=8 & season_num>=2)
```

![gold_rate1](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate1.png?raw=TRUE)

The regression shows that the IMDb score in the "Golden Age" doesn't change that much: the difference between the max and min of the regression are less than 2/5 of a point apart (with a linear regression this difference shrinks to 7/100 of a point). It is worth noting that despite the previous plot showing us that season 5 had the highest average score, the regression peaks at the season 6-season 7 border. The reason for this is the nature of the 'rolling average'-based LOESS regression, where the neighburing points help determine the value of the regression for a given point. 

Lastly, the average "Golden Age" episode rating is 8.2. So it seems the "Golden Age" is real, the show did have 6 seasons where the episodes were fairly consistent in quality. 

On the topic of higher-than-average quality, The Simpson's annual "Treehouse of Horror" episodes are some of my personal favorite episodes (remember that Treehouse of Horror V is one of the highest-rated episodes), and with Halloween only a couple weeks away, what better time to find out if these episodes are truly above average, or I'm clouded by the fun of the spooky atmosphere.

## Treehouse of Horror

For the past 27 Halloweens The Simpsons has aired a triplet of shorts that pay homage to, or parody films, television shows, literature, EC Comics, and of course, episodes of [The Twilight Zone](https://www.youtube.com/watch?v=SFokFDyDGgs). These episodes allow the writers to break the show's [canon](https://en.wikipedia.org/wiki/Canon_(fiction)) and imagine the characters in new ways, but with all the fantastic animation, keeping it inline with the show's atmosphere, and keeping the gore to censor-satisfying levels they often end up being quite difficult and stressful for the staff<sup> [4] </sup>. However, these are some of the most fun episodes, and the insane skills of the animators and writers are showcased as they raise the bar year after year.

To begin we create a data frame with only these Treehouse episodes. Since the quality fluctuates throughout the year we normalize the scores by seasons i.e. we will see if the average Treehouse's IMDb score is higher than that season's average score.


```R
#We create a new column in simp that highlights the "Treehouse of Horror" episodes 
#grepl(x,y) gives a boolean depending on whether it finds the string 'x' in position 'y'
#we loop through the episode names and add a new column for whether it is a "Treehouse ..." episode
simp$spooky<-grepl("Treehouse",simp$ep_name)
#Then we create a new dataframe with only the Treehouse Episodes
halloween<-subset(simp,spooky==TRUE)

#Let's look at both the ratio and difference
#We will loop over season, but note that the halloween dataframe first element is in season 2
for(i in 2:28){
     halloween$rate_diff[i-1]<-halloween$rating[i-1]-season_avg$rating[i]
     halloween$rate_ratio[i-1]<-halloween$rating[i-1]/season_avg$rating[i]
}
```

The ToH episodes score slightly above average, with a mean of 7.6 compared with the series 7.4, and the "Golden Age" ToH episodes average 8.5, compared with the 6-season average of 8.2. The season-normalized scores tell us that the Halloween specials are 4% better than an average episode that season. 

As we saw earlier is "Treehouse of Horror V", which is rated 9.1, is one of the series highest scoring episodes, but the worst ToH episode, and the only installment with a score lower than the season's average, is the 22nd installment of the Halloween special, which scores 6.6, with a zscore of -1 for the series, and -0.2 for that season. 

![treehouse_boxplot](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/treehouse_boxplot.png?raw=true)



So the Treehouse Episodes seem to be a bit, but not significantly, above average. This makes sense in hindsight, as they are still a product of the season's staff, and likely don't get *that* much more attention than other episodes. 



## Plots

### Episode Vote Numbers

```R
ep_votes_plot<-ggplot(simp,aes(x=total_ep_num,y=num_votes))+geom_point(aes(col=simp$season_num))+ggtitle("Every Vote Counts",subtitle="The Simpsons, Votes for IMDb Rating")+xlab("Episode Number")+ylab("Number of Votes")+labs(col="Season")+geom_segment(aes(x=55,y=3945,xend=7,yend=4087),col="RED",arrow=arrow(type="open",length=unit(0.24,"cm")))+annotate("text",x=90,y=3930,label="First Episode",col="RED",size=3)
```

### Episode Ratings
```R
ep_rate_plot<-ggplot(simp,aes(x=total_ep_num,y=rating))+geom_point(aes(col=season_num))+geom_smooth(se=TRUE,method=loess)+xlab("Episode Number")+ylab("IMDb Rating")+ggtitle("Settling the Score",subtitle="The Simpsons")+labs(col="Season")
```
### Season Average Ratings
```R
avg_rating_plot<-ggplot(season_avg,aes(x=season_avg$season_num,y=season_avg$rating))+geom_col()+coord_cartesian(ylim=c(6.5,8.5))+geom_hline(yintercept=8,col="RED",linetype="dashed")+geom_hline(yintercept=7,col="RED",linetype="dashed")+scale_x_continuous(breaks=c(2,4,6,8,10,12,14,16,18,20,22,24,26,28))+xlab("Season Number")+ylab("IMDb Rating")+ggtitle("The Golden Years",subtitle="The Simpsons, Season Averages")
```

### golden age

```R
gold_rate<-ggplot(gold_age,aes(x=total_ep_num,y=rating,col=season_num))+geom_point()+geom_smooth(method='loess',se=TRUE)+ggtitle("Staying Golden",subtitle="The Simpsons \"Golden Age\" Score Evolution")+xlab("Episode Number")+ylab("IMDb Rating")+geom_segment(aes(x=14,y=8.01,xend=178,yend=8.01),col="RED",linetype="dashed")+annotate("text",x=175,y=8.5,col="RED",label="Δy=0.37")+geom_segment(aes(x=14,y=8.38,xend=178,yend=8.38),col="RED",linetype="dashed")+geom_segment(aes(x=178,y=8.01,xend=178,yend=8.38),col="RED",arrow=arrow(ends="both",type="open",length=unit(0.24,"cm")))+labs(col="Season")
```

### Horror Bar
```R
horror_bar<-ggplot(subset(season_avg,season_num>=2),aes(x=season_num,y=rating))+geom_col()+coord_cartesian(ylim=c(6.5,9.2),xlim=c(2,28))+scale_x_continuous(breaks=c(5,10,15,20,25))+geom_line(data=halloween,aes(x=season_num,y=rating),col="orange")+xlab("Season Number")+ylab("IMDb Rating")+ggtitle("Scared Jagged",subtitle="The Simpsons")+annotate("text",x=10.5,y=8.75,label="Treehouse of Horror",col="orange")+scale_color_discrete(guide=FALSE)+annotate("text",x=12,y=8.3,label="Season Average",col="grey30")
```

# Footnotes 

<sup> [1] </sup>
i pulled on September 6, 2017, and it has certainly changed since.



<sup> [2] </sup>
This is IMDb's weighted average, the arithmetic mean is 8.7.

<sup> [3] </sup>
I will use this throughout for various subsets, so I will explicitly show the method once. Sample standard deviation calculated in the [normal way](https://wikimedia.org/api/rest_v1/media/math/render/svg/00eb0cde84f0a838a2de6db9f382866427aeb3bf)

```R
#First find the estimated mean
rate_mean<-mean(simp$rating)

#Then set the sum to zero and loop over the ratings for all the episodes
sum=0
for(i in 1:nrow(simp)){
  sum<-sum+(simp$rating[i]-rate_mean)^2
}

#Now put the sum into the formula for sample standard deviatiog
std_dev<-(sum/(nrow(simp)-1))^(1/2)

#Now we can see the value
std_dev
[1] 0.7509323
```
Now you can calculate the z-score for various points.

<sup> [4] </sup>: Reiss, Mike (2002). The Simpsons season 2 DVD commentary for the episode "Treehouse of Horror" (DVD). 20th Century Fox.
