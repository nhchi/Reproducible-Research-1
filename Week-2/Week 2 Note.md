####First markdown code

My first mark
=========================================
what what what

```{r}
library(datasets)
data(airquality)
summary(airquality)
```

```{r}
pairs(airquality)
```

####Regression model
```{r}
library(stats)
fit<-lm(Ozone ~ Wind+Solar.R+Temp, data = airquality)
summary(fit)

```
####List
* First
* Second

