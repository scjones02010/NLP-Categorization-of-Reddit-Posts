# Executive Summary Project 3

### Problem Statement

Given a randomized set of posts and the words used within them, how likely is it that a republican or a democrat posted these words?

#### Process

In this project, we will mine the republican and democrat subreddit and use the vocabular to determine new posts coming from the republican or democratic sentiments. In this we will create a for loop to mine the posts, perfrom EDA to clean and gather information, create a series of models and then conclude their accuracy.

### Data Gathering

Data was gathered from the Democrat and Republican subreddits. The subreddit links will be below. This information was used to gather the title information from the subreddits up to 1000 posts per day from each subreddit. When looking toward these, each was saved as their own data frame to be cleaned and merged.


### Data Cleaning and EDA

Each data frame was imported and using pandas. Each data frame was checked for duplicates, null and nas. All duplicates were deleted. Each data frame had a column created using a D or a R representing a republican or democrate post. These data frames were merged into a single data frame similar to a union and then vader sentiment analysis was applied to each title. This showed the postive, negative neutral and compond sentiment. Also each data frame was analyzed for the character count within each title. It was found that Republican posts tended to have slightly higher positive, or negative sentiment. Democratic posts tended to be more neutral, but longer in comparison. These were kept in mind while constructing models for analysis.


## Model Creation and Selection

For models were constructed using the Count Vectorizor and the TFIDVectorizer for each round. The models that were chosed were the KNN Classifier, the Logistic Model, the Multinomial Bayes model and the Bernouli Bayes model. Each was run without anly paramter tuning using grid searching and all models showed signs of significant overfitting. When tuning the parameters the following was used for each instance.

Count Vectorizor
    #Stop words were either engligh or none
    #Ngrams were either (1,1), (1,2) or (1,3)

TFID Vectorizor
    #Stop words were either engligh or none
    #Ngrams were either (1,1), (1,2) or (1,3)

Logistic Regression
    #C values were tested from 1 to 10
    
KNN Regressor
    #Manhattan and Eucldian distances were tested
    #N neighbors were 3, 5, 7, 9, 15

After testing each of the parameters, there were corrections to error due to overfitting, but this had minimal gains to the overall bias of the model. When selecting the best model, this was a logistic regressor with the Count Vectorizor tuned over the following parameters: using stop words, n grams (1,3) and a C value of 10. This model performed at a 75% training rate and a 73% test rate. 

### Conclusions

Using the tuned logistic regression model, the model was generally okay when looking at most posts, but had issues when looking at posts that contained highly correlated words typically used by the other subreddit. Words with strong coefficients like trump, whistleblower or crooked, would be misclassified due to the model not being able to pick up context correctly. An example democratic post such as "Trump is making America Great Again?" would be classified as a republican posts due to the words, but would not pick up on the context of the question. When applying this to a confusion matrix, there were errors due to false positives and negatives. The model did perform better of specificity then sensitvity (recall). This is due to Republican posts having much more heated language while democratic posts are more neutral in nature. Improvements to this model should take into account previously selected words such as looking at likelihoods of words following one another other than simple groupings. Stemming or Lemmitization will only narrow the words, but will not take the context of them into account.
