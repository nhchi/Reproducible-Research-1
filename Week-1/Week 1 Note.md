#####Steps in data analysis

######1. define the question
```
- Statistical methods development
- Danger zone
- Proper data analysis
```
######2. define the ideal data set
```
- Descriptive - a whole population
- Exploratory - a random sample with many variables measured
- Inferential - the right population, randomly sampled
- Predictive - a training data set and test data set from the same population
- Causal - data from a randomized study
- Mechanistic - data about all components of the system
```
######3. determine what data you can access
- Get free online
- Buy
- Respect teh terms of use
- Generate it yourself

######4. obtain the data
```
- Try to obtain the raw dat
- Be sure to reference the source
- Polite emails go a long way
- If you will load the data from an internet source, record the url and time accessed
```
######5. clean the data
```
- Raw data often needs to be processed
- If it is pre-processed, make sure you understand how
- Understand the source of the data(census, sample, convenience sample)
- May need reformining, subsampling
- Determine if the data are good enough
> library(kernlab)
> library(kernlab)
> data(spam)
> str(spam[,1:5])

######6. explortory data analysis
```
# subsampling data sep
> set.seed(3343)
> trainIndicator = rbinom(4601,size = 1, prob = 0.5)
> table(trainIndicator)
#trainIndicator
#   0    1 
#2351 2250
```
######7. statistical prediction/modeling
######8. interpret results
######9. challenge results
######10. synthesize/write up results
######11. create reproducible code
```
#####Possible resource to access data set
```
UCI Machine Lerning Reopsitory
Spambase Data Set for Email Spam/Ham
http://archive.ics.uci.edu/ml/datasets/Spambase
http://search.r-project.org/library/kernlab/html/spam.html
```


