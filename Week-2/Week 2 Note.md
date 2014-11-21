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

####More complicated way
library(knitr)
setwd(<working directory>)
knit2html("document.Rmd")
browseURL("document.html")

#####echo=FALSE, not showing code
#####results='hide',result hide
```{r simulation, echo=FALSE, results='hide'}
library(stats)
fit<-lm(Ozone ~ Wind+Solar.R+Temp, data = airquality)
summary(fit)

```

####inline code
```{r computetime, echo=FALSE}
time<-format(Sys.time(),"%a %b %d %X %Y")
rand<-rnorm(1)
```
The current time is `r time`.
My favorite random number is `r rand`.

####Incorporating graphics
Simulate some data
```{r simulatedata,echo=TRUE}
x<-rnorm(100);y<-x+rnorm(100,sd=0.5)
```
Scatterplot
```{r scatterplot,fig.height=4}
par(mar = c(5,4,1,1),las=1)
plot(x,y,main= 'my simulated data')
```

####Making table
```{r fitmodel}
library(datasets)
data(airquality)
fit<-lm(Ozone ~ Wind + Temp + Solar.R, data = airquality)
```
Table fo regresssion coefficients
```{r showtable, results='asis'}
library(xtable)
xt<-xtable(summary(fit))
print(xt,type="html")
```
####Setting global options
```{r setoptions,echo=FALSE}
opt_chunk$set(echo = FALSE, results = "hide")#doesn't work here, waiting for debugging
```
First simulate data
```{r simulatedata1, echo=TRUE}
x<-rnorm(100);y<-x+rnorm(100,sd = 0.5)
```
Scatter plot
```{r scatterplot1,fig.height=4}
par(mar = c(5,4,1,1),las = 1)
plot(x,y,main ="my first data")
```
####Options
#####Output
results: "asis"(don't postprocess results, show the raw resluts),"hide"
ecno:TRUE,FALSE
#####Figures
fig.height:numeric
fig.width:numeric
#####Caching computations
cache=TRUE
#####Cachiing caveats



