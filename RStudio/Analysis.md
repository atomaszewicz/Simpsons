# Analyzing The Simpson's Quality

We have already cleaned the raw IMDb data in an excel spreadsheet and we will bring it into RStudio for analysis.

Begin by loading our favorite packages.

```{r}
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

We will use IMDb's breakdown of the voting demographics for their aggregated TV score by series and by episodes, found(here)[http://www.imdb.com/title/tt0096697/ratings?ref_=tt_ov_rt_]. I will start by doing the data on the series, and if I have time I can come back and analyze the changes in demographic by episode to get a better picutre of the evolution of the IMDb voting audience. 

The data (pulled September 6, 2017) sheds some light on what groups are voting the most, and how much they like the series. Males make up over 80% of the ratings, and they rate it an average of 8.8/10, a fifth of a point higher than females but the same as the rating over all demographics. The highest praise was given by the male 18-29 and male 30-44 demographics, who rated the series an average of  8.9/10. It is a bit suprising that the male portion of the "core" 18-29 demo has the same net opinion as the less-important male 30-44 demo, but when you remember that The Simpsons has been on air for 28 years, and that the latter group thus up alongside the show, it makes more sense. The lowest raiting is from the female 45+ demographic giving the show a 7.9/10, which is a suprisingly high rating since much of the show's appeal is subverting the norms of the shows the 45+ demographic grew up with (although I must note that both my 45+ parents enjoy the show).





## Plots

### Episode Vote Number Plot

```R
ep_votes_plot<-ggplot(simp,aes(x=total_ep_num,y=num_votes))+geom_point(aes(col=simp$season_num))+ggtitle("Every Vote Counts",subtitle="IMDb Data Pulled Aug 31, 2017")+xlab("Episode Number")+ylab("Number of Votes For IMDb Score")+geom_smooth(method='lm')+labs(col="Season")
```

### Episode Rate Plot
```R
ep_rate_plot<-ggplot(simp,aes(x=total_ep_num,y=rating,factor=simp$season_num))+geom_point(aes(col=season_num))+geom_smooth(method='lm',se=FALSE)
labels<-+xlab("Episode Number")+ylab("IMDb Rating")+ggtitle("Scoring The Simpsons",subtitle="IMDb Data Pulled Aug 31, 2017")+labs(col="Season")
```
### 
