####Steps in data analysis

######1. define the question
- Statistical methods development
- Danger zone
- Proper data analysis

######2. define the ideal data set
- Descriptive - a whole population
- Exploratory - a random sample with many variables measured
- Inferential - the right population, randomly sampled
- Predictive - a training data set and test data set from the same population
- Causal - data from a randomized study
- Mechanistic - data about all components of the system

######3. determine what data you can access
- Get free online
- Buy
- Respect teh terms of use
- Generate it yourself

######4. obtain the data
- Try to obtain the raw dat
- Be sure to reference the source
- Polite emails go a long way
- If you will load the data from an internet source, record the url and time accessed

######5. clean the data
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
> trainSpam = spam[trainIndicator == 1,]
> testSpam = spam[trainIndicator == 0,]
# half is train data, the orther is test data
```
- Look a summaries of the data
- Check of missing data
- Creat exploratory plots
- Perform exploratory analyses(e.g clustering)
```
> names(trainSpam)# column names
 [1] "make"              "address"           "all"              
 [4] "num3d"             "our"               "over" 
 
> table(trainSpam$type)
nonspam    spam 
   1357     893 
   
> head(trainSpam)# frequency
   make address  all num3d  our over remove internet order mail
2  0.21    0.28 0.50     0 0.14 0.28   0.21     0.07  0.00 0.94
6  0.00    0.00 0.00     0 1.85 0.00   0.00     1.85  0.00 0.00
8  0.00    0.00 0.00     0 1.88 0.00   0.00     1.88  0.00 0.00
9  0.15    0.00 0.46     0 0.61 0.00   0.30     0.00  0.92 0.76
10 0.06    0.12 0.77     0 0.19 0.32   0.38     0.00  0.06 0.00
13 0.00    0.69 0.34     0 0.34 0.00   0.00     0.00  0.00 0.00
> plot(trainSpam$capitalAve ~ trainSpam$type) # data distribution is skewed 

> plot(log10(trainSpam$capitalAve+1) ~ trainSpam$type)# using log function

> plot(log10(trainSpam[,1:4]+1))# relationship between predictions, pairs of plots

> hCluster = hclust(dist(t(trainSpam[,1:57])))# hierarchical cluster analysis
> plot(hCluster)# useful for skewed data, but need transfermation

> hClusterUpdated = hclust(dist(t(log10(trainSpam[,1:55]+1))))
> plot(hClusterUpdated)

 ```
######7. statistical prediction/modeling
- Informed by the results of exploratroy analysis
- Exact methods depend on the question of interest
- Tranformation/processing should be accounted for when necessary
- Measures of uncertainty should be reported
```
trainSpam$numType = as.numeric(trainSpam$type)-1
costFunction = function(x,y) sum(x !=(y>0.5))
cvError = rep(NA,55)
library(boot)
for(i in 1:55){
  lmFormula = reformulate(names(trainSpam)[i],response ='numType')
  glmFit = glm(lmFormula, data = trainSpam,family = "binomial")
  cvError[i] = cv.glm(trainSpam, glmFit, costFunction, 2)$delta[2]
}

# Which predictor hsa minimum cross-validatied error?
names(trainSpam)[which.min(cvError)]

# Use the best model from the group
predictionModel = glm(numType ~ charDollar, family = 'binomial',data = trainSpam)

# Get predictions on the best set
predictionTest = predict(predictionModel,testSpam)
predictedSpam = rep("nonSpam", dim(testSpam)[1])

# Classify as "spam" for those with prob>0.5
predictedSpam[predictionModel$fitted.0.5] = "spam"

# Classification table
table(predictedSpam,testSpam$type)

# predictedSpam nonspam spam
# nonSpam    1431  920

# error rate
(61+458)/(1346+458+61+449)
# [1] 0.2242869
```

######8. interpret results
- Use the appropriate language
  - describes
  - correlates with/associated with
  - leads to/causes
  - predicts
- Give an explanation
- Interpret coefficients
- Interpret measures of uncertatinty

######9. challenge results
- Challenge all steps:
  - Question
  - Data source
  - Processing
  - Analysis
  - Conclusions
- Challenge measures of uncertanity
- Challenge choices of terms to include in models
- Potential alternative analyses

######10. synthesize/write up results
- Lead with the question
- Summarize the analyses into the story
- Don't inculde every analysis, include it
  - If it is needed for the story
  - If it is needed to address a challenge
- Order analyses according to the story, rather than chronologically
- Include "pretty" figures that contribute to the story

######11. create reproducible code

####Possible resource to access data set

```
UCI Machine Lerning Reopsitory
Spambase Data Set for Email Spam/Ham
http://archive.ics.uci.edu/ml/datasets/Spambase
http://search.r-project.org/library/kernlab/html/spam.html
```

####Organized analysis
- Data
  - Raw
    - Stored in analysis folder
    - Source, web url, data accessed in README
  - Processed data
    - Named properly
    - Processing script
    - Tidy
- Figures
  - Exploratory figures
    - Do not need to be pretty
    - During of the analysis
  - Final
    - Axes/colors set to make the figure clear
    - Possibly multiple panels
    - Subset of original plot
- R code
  - Raw/unused scripts
    - Less commented
    - Multiple versions
    - Inculde analysis that are later discarded
  - Final
    - Clearl commentd
    - Processing details
    - Only analyses appear in final write-up
  - R markdown files
- Text
  - README files
    - Step by step process of analysis
  - Text of analysis/report
    - Title, introduction(motivation),methods(statistics),results(measures of uncertainty), conclusions(potential problems)
    - Tell a story
    - Reference

