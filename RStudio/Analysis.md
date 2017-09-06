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


The first thing that we wonder is, well, how have the ratings evolved over time? But before we do that, I'd like to look at how the how  the voting participation on IMDb has evolved over time. 



## Plots

### Episode Vote Number Plot

```R
ep_votes_plot<-ggplot(simp,aes(x=total_ep_num,y=num_votes))+geom_point()+ggtitle("Every Vote Counts",subtitle="IMDb Data Pulled Aug 31, 2017")+xlab("Episode Number")+ylab("Number of Votes For IMDb Score")+geom_smooth()
```

### Episode Rate Plot
```R
ep_rate_plot<-ggplot(simp,aes(x=total_ep_num,y=rating,factor=simp$season_num))+geom_point(aes(col=season_num))+geom_smooth(method='lm',se=FALSE)
labels<-+xlab("Episode Number")+ylab("IMDb Rating")+ggtitle("Scoring The Simpsons",subtitle="IMDb Data Pulled Aug 31, 2017")+labs(col="Season")
```
### 
