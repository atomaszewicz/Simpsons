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

![ep_votes_plot](https://github.com/atomaszewicz/Simpsons/blob/master/RStudio/Plots/simp_votecount_sept6.png?raw=TRUE)

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

![ep_rate_plot](https://raw.githubusercontent.com/atomaszewicz/Simpsons/master/RStudio/Plots/ep_rate_plot.png?raw=TRUE)

As I expected, the show exhibits a classic structure for long-running series: drastic early show growth, reaching a maximum, then a slow fall to below the first few seasons' scores. There is often much discussion about the "Golden Age" of The Simpsons, i.e. when it was at it's very best. Looking out our `season_avg` dataframe seasons 2-8 all have an average rating of above 8.0, season 1 & 9-16 are above 7.0 and seasons 17-28 are in the range 6.5-7.0.






## Plots

### Episode Vote Number Plot

```R
ep_votes_plot<-ggplot(simp,aes(x=total_ep_num,y=num_votes))+geom_point(aes(col=simp$season_num))
labels<-ggtitle("Every Vote Counts",subtitle="IMDb Data Pulled Aug 31, 2017")+xlab("Episode Number")+ylab("Number of Votes For IMDb Score")+labs(col="Season")
```

### Episode Rate Plot
```R
ep_rate_plot<-ggplot(simp,aes(x=total_ep_num,y=rating,factor=simp$season_num))+geom_point(aes(col=season_num))+geom_smooth(se=FALSE,method=lm,col="grey45")
labels<-xlab("Episode Number")+ylab("IMDb Rating")+ggtitle("Scoring The Simpsons",subtitle="IMDb Data Pulled Aug 31, 2017")+labs(col="Season")
```
### 
