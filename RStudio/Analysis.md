# Analyzing The Simpson's Quality

We have already cleaned the raw IMDb data in an excel spreadsheet and we will bring it into RStudio for analysis.

Begin by loading our favorite packages.

```R
install.packages("xlsx") 
install.packages("ggplot2")
install.packages("reshape2")
require("xlsx")
require("ggplot2")
require("reshape2")
```

Now we load it isn't a table in R

```R
simp<-read.xlsx("simpsons.xlsx",2)
```

We quickly solidify the order of the seasons as R sometimes factors them weirdly.
```R
simp$season_num<-factor(simp$season_num)
```


The first thing that we wonder is, well, how have the ratings evolved over time? Have they gone up or down i.e. do people percieve the show as getting better or worse? That isn't the whole story however, as *who* is voting is a very important aspect. 

## Voting

We will use IMDb's breakdown of the voting demographics for their aggregated TV score by series and by episodes, found [here](http://www.imdb.com/title/tt0096697/ratings?ref_=tt_ov_rt_). I will start by doing the data on the series, and if I have time I can come back and analyze the changes in demographic by episode to get a better picutre of the evolution of the IMDb voting audience. 

The data (pulled September 6, 2017) sheds some light on what groups are voting the most, and how much they like the series. Overall the series recieved a score of 8.8/10, which makes it the 54th highest rated show in IMDb. Males make up over 80% of the ratings, and they rate it an average of 8.8/10, a fifth of a point higher than females. In fact, in every age demographic, males rate the series higher. Males voted over four and half times more than females, and each age demographic is largely dominated by men. The smallest demographic is the under 18's, who make up less than one percent of the score (this is the group that discovered the show after it's decline. We will come back to this later). The two groups that rated it the most are the male portion of the 18-29 and 30-45 year old demographics. Combined they make up almost two thirds of the votes, with the 18-29 males voting about 15% more than the 30-45 males.

These two groups also rated the series the highest, giving it an average score of 8.9/10. It is a bit suprising that the male portion of the "core" 18-29 demo has the same net opinion as the less-important male 30-44 demo, but when you remember that The Simpsons has been on air for 28 years, and that the latter group thus up alongside the show, it makes more sense. In fact these two groups voted a similar amount, with the 18-29 having about 15% more votes. The lowest raiting is from the female 45+ demographic, who give the show a 7.9/10, which is a suprisingly high rating since much of the show's appeal is subverting the norms of the shows that the 45+ demographic grew up with.

Now that we've seen who is voting for the series, let's look at how the number of votes changes throughout the series.

![ep_votes_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_votes_plot.png?raw=TRUE)

Seeing at the earlier seasons have been out for ~20 years more than the earlier episodes, it is only natural that more people have seen them, explaining the downward-trend in number of ratings. However, I don't want to discount the possibility that this downward trend is, at least in part, caused by the show's audience decreasing (we will come back to this in the viewership section). We also note that the ~4000 vote point at the beginning is the first episode (after a cursory look on IMDb, it seems that show's first episodes often have ave a large number of votes).

We can now look at how how the seasons were voted on average.

```R
#Create a new dataframe to store the average number of votes, and ratings for each season
season_avg<-data.frame(season_num=1:28)
for(i in 1:28){
  season_avg$num_votes[i]<-mean(subset(simp$num_votes,simp$season_num==i))
  season_avg$rating[i]<-mean(subset(simp$rating,simp$season_num==i))
}
```


## Scoring
I've made you wait long enough so let's get straight into it. How has the IMDb score for episodes changed over the years?

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plots.png?raw=TRUE)

Early growth, a peak, then a drop to a plateau. The early episodes hover mostly between 7.5-9, while the later episodes sit in the 6.5-7.5 range. Therefore it does seem as if the quality has decreased throughout the years, to which many of the shows fans will say "DUH!".

With a quick Google search, one can find endless pages with "Top X Best Simpsons Episodes", BThe next question on my mind is another much-discussed topic amongst the shows loyal fanbase: The best (and worst) episode.

```R
simp[which.max(simp$rating),]
    total_ep_num season_num ep_num imdb_num       ep_name rating num_votes
176          176          8     23     8.23 Homer's Enemy    9.3      2693
```

Oddly enough we see that the most highly-rated episode is one whose premise is an hard-working outsider pointing out the absurdities in the show's premise. It serves as a nod of self-awarness to the audience as well as a reminder to it's obsessive fans that it's just a show. This episode would not make my top 10, but fans evidently like the show taking a break from wacky adventures and looking inwards.

Other episodes with ratings above 9.0 include ["You Only Move Twice"](http://simpsons.wikia.com/wiki/You_Only_Move_Twice) where Homer is unknowingly hired by a Bond Villain, ["Cape Feare"](http://simpsons.wikia.com/wiki/Cape_Feare) a remake of ["Cape Fear"](https://en.wikipedia.org/wiki/Cape_Fear_(1962_film)) where The Simpsons enter a witness protection program after Bart receives death threats from his nemsis Sideshow Bob, ["Treehouse of Horror V"](http://simpsons.wikia.com/wiki/Treehouse_of_Horror_V) one of the classic Halloween episodes (which features homages to ["The Shining"](https://en.wikipedia.org/wiki/The_Shining_(film)), ["A Sound of Thunder"](https://en.wikipedia.org/wiki/A_Sound_of_Thunder), and ["Soylent Green"](https://en.wikipedia.org/wiki/A_Sound_of_Thunder)), ["Who Shot Mr. Burns? Part One"](http://simpsons.wikia.com/wiki/Who_Shot_Mr._Burns%3F_(Part_One)) a murder mystery where everyone in town is a suspect, and ["The City of New York vs. Homer Simpson"](http://simpsons.wikia.com/wiki/The_City_of_New_York_vs._Homer_Simpson) where Homer fights parking tickets in the Big Apple. Note that all these episodes are between seasons 5 through 9.

On the other end of the spectrum, the lowest-rated episode is the Season 23 ["Lisa Goes Gaga"](http://simpsons.wikia.com/wiki/Lisa_Goes_Gaga) with a 4.3/10 which features Lady Gaga helping Lisa with her self esteem. Other low-rated episode include ["All Singing All Dancing"](http://simpsons.wikia.com/wiki/All_Singing,_All_Dancing) a musical episode, an episode where [The Simpsons go to Jerusalem](http://simpsons.wikia.com/wiki/The_Greatest_Story_Ever_D%27ohed) and Homer defiles various holy sites, a couple of clip show episodes and an episode where [Moe's washrag tells it's life's story](http://simpsons.wikia.com/wiki/Moe_Goes_from_Rags_to_Riches).

## Golden Years

With 600+ episodes, you're bound to have a few stinkers, but what I'm trying to study here is less a few crappy scripts, but more how the show has evolved. So let's jump into a much debated topic among Simpsons fans: "The Golden Age" i.e. when it was at it was it's best. Thankfully we already made our `season_avg` dataframe with the ratings averaged over season, so we can easily plot the average rating of each season.

![avg_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/avg_rating_plot.png?raw=TRUE)

We see that seasons 2-8 have an average rating of above 8.0, season 1 & 9-16 averages are above 7.0 and seasons 17-28 are in the range 6.5-7.0. This fits with the widely-accepted idea that seasons 2-8 is where the show was in peak form, with the show still finding it's footing in the first season, and the show losing it's edge after season 8. 

Let's take a closer look at this "Golden Age" of seasons 2-8. 

```R
#Let's create a data frame to make this a little easier
gold_age<-subset(simp,season_num<=8 & season_num>=2)
```

![gold_rate2](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate2.png?raw=TRUE)

The regression shows that the IMDb score in the "Golden Age" doesn't change that much: the difference between the max and min of the regression are less than 2/5 of a point apart (with a [linear regression](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/gold_rate.png?raw=TRUE) this difference shrinks to 7/100 of a point  ). It is worth noting that despite the previous plot showing us that season 5 had the highest average score, the regression peaks at the season 6-season 7 border.

## Treehouse of Horror

As I'm writing this Halloween is only a couple weeks away, so I thought I'd take a look at The Simpsons "Treehosue of Horror" Halloween specials. For the last 27 years (this tradition was introduced in Season 2) The Simpsons has aired spooky episodes featuring 3 segments paying homage to, or parodying, various  films, television shows, literature, plays, EC Comics, and of course, episodes of [The Twilight Zone](https://www.youtube.com/watch?v=SFokFDyDGgs). These episodes allow the writers to break the [canon](https://en.wikipedia.org/wiki/Canon_(fiction)) of the show, but are often extremelly difficult for both the writers and animators <sup> [1] </sup>


```R
#We create a new column in simp that highlights the "Treehouse of Horrors" episodes 
#grepl(x,y) gives a boolean depending on whether it finds the string 'x' in position 'y'
simp$spooky<-grepl("Treehouse",simp$ep_name)
halloween<-subset(simp,spooky==TRUE)
```

## Plots

### Episode Vote Numbers

```R
ep_votes_plot<-ggplot(simp,aes(x=total_ep_num,y=num_votes))+geom_point(aes(col=simp$season_num))+ggtitle("Every Vote Counts",subtitle="The Simpsons")+xlab("Episode")+ylab("Number of Votes for IMDb Score")+labs(col="Season")
```

### Episode Ratings
```R
ep_rate_plot<-ggplot(simp,aes(x=total_ep_num,y=rating,factor=simp$season_num))+geom_point(aes(col=season_num))+geom_smooth(se=FALSE,method=lm,col="grey45")+xlab("Episode")+ylab("IMDb Rating")+ggtitle("Settling the Score",subtitle="The Simpsons")+labs(col="Season")
```
### Season Average Ratings
```R
avg_rating_plot<-ggplot(season_avg,aes(x=season_avg$season_num,y=season_avg$rating))+geom_col()+coord_cartesian(ylim=c(6.5,8.5))+geom_hline(yintercept=8,col="RED",linetype="dashed")+geom_hline(yintercept=7,col="RED",linetype="dashed")+scale_x_continuous(breaks=c(2,4,6,8,10,12,14,16,18,20,22,24,26,28))+xlab("Season")+ylab("Average IMDb Score")+ggtitle("The Golden Years",subtitle="The Simpsons")
```

### golden age

```R
gold_rate<-ggplot(gold_age,aes(x=total_ep_num,y=rating,col=season_num))+geom_point()+geom_smooth(method='lm',se=TRUE)+ggtitle("Staying Golden",subtitle="The Simpsons 'Golden Era'")+xlab("Episode")+ylab("IMDb Rating")+geom_segment(aes(x=14,y=8.16,xend=178,yend=8.16),col="RED",linetype="dashed")+annotate("text",x=175,y=8.5,col="RED",label="Δy=0.07")+geom_segment(aes(x=14,y=8.37,xend=178,yend=8.37),col="RED",linetype="dashed")+geom_segment(aes(x=178,y=8.16,xend=178,yend=8.37),col="RED",arrow=arrow(ends="both",type="open",length=unit(0.24,"cm")))+labs(col="Season")

```

# Footnotes 

<sup> [1] </sup>: Reiss, Mike (2002). The Simpsons season 2 DVD commentary for the episode "Treehouse of Horror" (DVD). 20th Century Fox.
