# Project 3: Web APIs & NLP

## Problem statement: 

What is best possible classifier model to use to predict between two subreddits given a random submission post?

## Data Chosen: 

 - [`rollingstones.csv`](../data/rollingstones.csv): r/rollingstones webscraped data
 - [`TheBeatles.csv`](../data/TheBeatles.csv): r/TheBeatles webscraped data

## Outside research: 

I have a Works Cited section in the code jupyter notebook. These articles helped with interpretations of AUC ROC curve graph, the confusion matrix, cross validation, etc. 

## Data Dictionary:

|Feature|Type|Dataset|Description|
|---|---|---|---|
|subreddit|int64|beatles_stones|Target variable of model - contains two subreddits mapped to the following values - {'TheBeatles': 0, 'rollingstones': 1}| 
|author|object|beatles_stones|Participation percentage rate of students in 2018 from corresponding state.|
|score|int64|beatles_stones|Also known as Reddit Karma, score is a ratio of upvotes and downvotes on submissions made by user.|
|title|object|beatles_stones|A clear, concise summary of submission post.|
|num_comments|int64|beatles_stones|Number of comments for submission post.|
|title_nopunc|object|beatles_stones|A clear, concise summary of submission post with punctuation, URLs, and other special characters removed.|
|title_length|int64|beatles_stones|The title character length.|
|title_word_count|int64|beatles_stones|The number of words in a submission's title.|
|p_stem_title|object|beatles_stones|Alteration of title column by removing the last few characters of a word to bring each word down to its 'stem'.|
|lem_title|object|beatles_stones|Alteration of title column by converting a word to its meaningful root form but considering the context.|

## Overview of Data Directory:

This directory contains the subreddit data I chose to scrape for this project. I decided on working with a category whose content I am familiar with which is why I chose to examine r/rollingstones & r/TheBeatles. 

## Conclusions & Key-Takeaways:

### EDA 1 Conclusions: 

All of the distributions when analyzing title word count and character length count are right skewed. The average character length between both subreddits is ~56 characters and the median character length is 46. In regards to title word count, the average title word count between both subreddits is ~10 words and the median title word count is 8 words. 

Biggest takeaway from EDA 1: 
When using a Seaborn displot and hue, I found the r/rollingstones to have a greater character length and word count for their title submissions. Since these features are numeric, I will use them with my model to help distinguish between the two subreddits.

### WordCloud Conclusions: 

I was curious at making individual wordclouds for the subreddits to see if the size (frequency) of particular words were the same across both. However, I found a few interesting exceptions in The Beatles wordcloud which were the words cover, album, and vote. When looking at the beatles and rolling stones combined, I found the words most commonly used to be song, album, love, and Let(It Be). Based solely off these common words, I can see a bit more influence coming from the beatles subreddit than the rolling stones subreddit. 

### CountVectorizer EDA Conclusions: 

When running the CountVectorizer without any hyperparameters aside from english stopwords taken out, the words beatles, rolling, and stones appeared well over 800 times each. As a result, I decided to set a max_df of 800 so I could make room for what other less obvious words in the submission titles were used frequently. The words song, album, and like are the top 3 which may end up being a struggle for my model as either of these could just as easily exist in one subreddit as the other. The one advantage my model will have is none of the band member names are shared. 
Although I am not entirely sure the finer details of stemming and lemmatizing, when examining the title columns which were stemmed and lemmatized I found the common word combo order changed slightly. I will keep this in mind when considering those columns as features in my model. More specifically, I would much rather use the lemmatized title column since this was able to pick out much more discernable word combos helpful to my model's predictions between the two different subreddits. 

### TFIDFVectorizer EDA Conclusions:

Overall, the TFIDFVectorizer didn't do as good of a job in my opinion at picking out words or word combos which would help my model distinguish between two different subreddits. For example, the top three words in submission titles were song, album and paul which aside from Paul could exist in either subreddit quite frequently. The lemmatizer won out in this vectorizer as well with being able to pick out a better set of common words. 

Biggest takeaway: After running some charts on both CountVectorizer and TFIDFVectorizer with stemming and lemmatizing as well, I think CountVectorizer will be my vectorizer of choice as this was able to pull highly distinguishable words and word combos which would be helpful for my model to predict between two different subreddits. 

### Multiple Models Conclusions: 

The goal overall is training my model to be good at determining between two different subreddits. Reddit is a widely popular website for posting opinions on a multitude of topics e.g. music, travel, politics, and gardening to name a few. With this being said, I am most interested in seeing how well my model does on unseen data. Since the amount I scraped, 5,000 submissions, is only a fraction of what has been written on either of the subreddits I chose, I am concerned about how overfit my model will be which is why I sorted this dataframe by 'Testing Score'. 

The least overfit and highest performing model thus far without tuning hyperparameters is the Multinomial Naive Bayes model with the CountVectorizer. When looking at training scores, the best performing model was the RandomForestClassifier with CountVectorizer though, so I would like to see if using the lemmatize or stemmed title columns will offer any improvements on the testing score. In addition to tuning hyperparameters, I would like to run the 'title_length' column through a classifier model to see how well due to the large coefficient value when I ran the features through a Logistic Regression model. 

Based off how well the Multinomial Naive Bayes model worked on the 'title_nopunc' feature, I want to use this model as a jumping off point in examining if my lemmatized title or stemmed title features perform any better during training and testing. After running these models, I will determine which feature to add with 'title_length' and tune hyperparameters to achieve a training and testing score of above .92 as a benchmark for the final model. 

### Modeling Conclusions: 

After some slight tuning, my best performing model turned out to be MultinomialNB with CountVectorizer using my lemmatized title column. The cross validation score and testing score rounded to 0.89 accuracy with the training score coming in at 0.92. Even though the RandomForestClassifier models performed with almost 100% accuracy on our training data, we should be more concerned with testing accuracy because testing accuracy is a better estimate than training accuracy on out-of-sample performance.  

For the next section, I worked on tuning the parameters of my pipeline, transformer, and classifier to try to improve my testing score; however, after several iterations, I still only managed to improve my cross-validation score by 0.01. Cross validation is process of splitting our initial dataset into separate training and test subsets or folds. Cross validation has a value, k, which represents how many different folds we will perform on our dataset. The cross validation score in this dataframe represents the average across the specific number of folds. We use cross-validation to avoid overfitting and estimate the skill of the model on new data. 

I used the cross validation before running my pipeline parameters through a gridsearch as an initial look into how well the model would perform on unseen data. As we can see from the table, KNeighborClassifier had quite a low cross val score which didn't give me much hope on selecting this as my model of choice. The cross validation score gives us another metric to base our decision of model selection on. As mentioned previously, Reddit is a popular website across many demographics with thousands of submissions posted daily. My goal of this project was to find the least overfit model so we could use this model to identify subreddit based off submission content. 

Although the model was slightly overfit, I have run multiple models and several iterations of my best scoring model through parameter tuning and managed to match my cross-val-score and testing score at .89 accuracy. With only a 0.03 difference between training and testing, I am satisfied with these final results especially considering how well this model outperforms the baseline model.

## Best Performing Model Evaluation Metrics: 

#### Confusion Matrix Interpretation: 
Confusion matrix is a performance measurement for machine learning classification. Our model had 1142 true negatives which means the model predicted 1142 submissions weren't from TheBeatles subreddit and the submissions weren't from TheBeatles subreddit. Similarly, our model had 1072 true positives which means the model correctly predicted a submission was in TheBeatles subreddit. 

On the contrary, our model had 178 false negatives which means the submission being evaluated was actually in TheBeatles subreddit and the model predicted incorrectly. Finally, the amount of false positives was 108 or the model predicted a submission was in TheBeatles subreddit but in fact was not. Overall, the model's performance of ~89% accuracy is quite impressive and for the use case gets my vote of confidence.

#### Classification Report Interpretation: 
The classification report visualizer displays the precision, recall, F1, and support scores for the model. Our precision or accuracy of positive predictions is 4% better with our rollingstones subreddit than TheBeatles subreddit. On the other hand, our recall or ability of our classifer model to find all positive instances is 5% better with TheBeatles subreddit. 

The F1 score is a weighted harmonic mean between precision and recall which is slightly better with TheBeatles subreddit by 1%. As mentioned previously, the accuracy of our classifier model is 89% which in terms of our baseline model's accuracy far exceeds its performance.

#### ROC Curve Interpretation: 
The area under the ROC curve is a measurement of how much overlap exists between our distributions and is important evaluation metric for checking any classification model's performance. The closer our ROC AUC is to 1, the better our model is at distinguishing between classes. With this being said, an area under the curve of 0.97 means our model does astonishingly well at distinguishing between our two different subreddits. 

## Presentation Liner Notes: 

Project 3 Presentation
1. My presentation today is about my approach to Project 3 which was working with APIs, NLP, & classifiers. 
2. My problem statement I set out to answer was: What is the best possible classifier model to use to help predict between two subreddits given a random submission post? I will let my assistant Paul Rudd reveal which two subreddits I chose to work with. 
3. The different steps of this project required were writing a web-scraping function which used the ‘requests’ library and an API to scrape for posts on reddit. As mentioned previously, I chose  r/rollingstones & r/TheBeatles as my subreddits. One roadblock I ran into when retrieving my data was not initially setting a time between scrapes which caused a ValueError to occur. Once I added this time between scrapes, I was able to gather the appropriate amount of submissions or 5,000 posts from each subreddit. Next, I removed all punctuation, and stemmed & lemmatized my title column to use as features in modeling. The EDA I performed followed in line with our NLP EDA lab which consisted of looking at title length, word count, & diverting slightly I decided to generate word clouds to see differences between the two subreddits. Finally, I used several different classifier models, LogisticRegression, RandomForest, KNeighbors, and Multinomial Naive Bayes with both CountVectorizer & TFIDFVectorizer  to assess which model generated the highest cross-val & testing score. 
4. Looking at the word clouds I generated for each individual subreddit, the band name and prominent band members are some of the most frequent terms to show up in submission posts. However, looking at the word combined subreddit word cloud - The Beatles seem to have a greater influence on word frequency since Paul and John show up much larger than Keith Richards and Mick Jagger. 
5. In order to eliminate some outliers and unhelpful terms, I chose to set the max_df on my Vectorizers to 800, and remove the stop words. Based off these two bar graphs, I found the CountVectorizer to be much more effective at pointing out words of importance such as popular band members, and famous albums, whereas the TFIDIF pulled out strange word combos such as round vote & survivor round. 
6. The goal overall is training my model to be good at determining which subreddit a post came from; as a result, my concern is creating a model which is the least overfit due to the multitude of other submissions this model will be used on. After some slight tuning, my best performing model turned out to be MultinomialNB with CountVectorizer using the lemmatized title column. Even though the RandomForestClassifier had incredibly high training scores, we are more focused on how the model performs on unseen data which is why I also chose to include cross-val-scores as another metric in my table. Cross validation folds the data into subsets and gives us a window into how the data will perform on unseen data. 
7. In the top right corner is the confusion matrix which states our model had 1142 true negatives, 1072 true positives, 178 false negatives, and 108 false positives. The two blue squares can be thought of as correct guesses which as stated before puts our model at an 89% accuracy rate overall. Then finally, the area under the ROC curve is a measurement of how much overlap exists between our distributions and is an important evaluation metric for checking any classification model’s performance. The closer our ROC AUC is to 1, the better our model is at distinguishing between classes. With this being said, an area under the curve of 0.97 means our model does astonishingly well at distinguishing between the two different subreddits. 
