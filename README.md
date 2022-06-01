## American Airlines Mobile App Reviews Analysis Project - Overview:
The idea of this project was to collect as many samples of reviews from American Airlines' mobile application and find common issues that customers may be facing when using the application.

* Scraped approximately 3700 reviews from the American Airlines mobile application off of the Apple App store. 

* Prior to performing analysis tasks, I used nltk and string methods to tokenize the reviews data.

* Following tokenization, I applied a wide range of analysis techniques to the text data of reviews. These including N-gram analysis, t-SNE for word exploration, Latent Dirichlet Analysis (LDA) to identify common topics within the data, as well as LIME and SHAP to investigate word impact on rating/sentiment as well as potentially towards the topics LDA identified.

I applied lime and shap with the target being the rating (ranging from 1 to 5) as well as the topics generated from LDA when applied to all reviews.

## Code and Resources Used:

**Python Version:** 3.8.5

**Packages:** numpy, pandas, requests, beautiful soup, matplotlib, seaborn, sklearn, lime, shap, gensim, nltk, collections, AppStore (app_store_scraper)

## References:

* Various project structure and process elements were learned from Ken Jee's YouTube series: 
https://www.youtube.com/watch?v=MpF9HENQjDo&list=PL2zq7klxX5ASFejJj80ob9ZAnBHdz5O1t

* Guide on learning t-SNE and how to apply it towards text data exploration as well as learning how to use Word2Vec from gensim
https://towardsdatascience.com/using-word2vec-to-analyze-news-headlines-and-predict-article-success-cdeda5f14751

## Web Scraping:

Using the web scraper tool from the AppStore module. I scraped the following information from the American Airlines mobile application:

*   username
*   review
*   isEdited
*   rating
*   title
*   date

## Data Cleaning

After collecting the data, I used nltk along with python string methods to tokenize the data and remove punctuation and other non alpha-numeric characters from the reviews.

## EDA
Within the BI-gram analysis of the data, I noticed that since a lot of the reviews were primarily low ratings, the common issues revolved around boarding passes, booking flights, and credit cards. Even requests to fix the application were also present. Again since this was only a sample of the data, we can't get a holistic view of the issues across all records.

The amount of reviews collected (since January 2019) remained fairly steady with a dip around the time when the COVID-19 pandemic hit the United States.

I also included a picture of one of the topics identified by applying LDA. This topic revolved around customers having issues with boarding passes as well as account issues. Unlike a few other topics, this one is relevant to the mobile application itself and not just their experience flying with the airline in general.

In addition is the t-SNE plot I used to explore word similarity when reducing the dimensions of the data to 2 aftering making a word2vec model of the review data (using the first 750 words). The area in the top right depicts words common among the application.

I also have a picture of the scatterplot of the shap values across reviews for the word 'boarding'. The shap value for this word is almost always in a direction pointed towards a negative sentiment. This is just an example of how we can analyze certain words for their sentiment in the reviews.

![alt text](https://github.com/elayer/American-Airlines-Mobile-App-Reviews-Analysis/blob/main/aareviews_bigrams.png "Bi-gram Analysis")
![alt text](https://github.com/elayer/American-Airlines-Mobile-App-Reviews-Analysis/blob/main/reviews_over_time.png "Reviews over Time")
![alt text](https://github.com/elayer/American-Airlines-Mobile-App-Reviews-Analysis/blob/main/aareviews_topics.png "LDA Topics")
![alt text](https://github.com/elayer/American-Airlines-Mobile-App-Reviews-Analysis/blob/main/tsne_plot.png "t-SNE plot")
![alt text](https://github.com/elayer/American-Airlines-Mobile-App-Reviews-Analysis/blob/main/boarding_analysis.png "Boarding Picture Example")

## Latent Dirichlet Analysis (LDA) Topic Modeling:
When applying LDA to the data, I was able to identify the following topics (labelling them manually):
* Mobile App Feelings & Mobile App Issues (nearby each other as 1 and 3 in the EDA pictures). 
* Flight delay issues
* Baggage and luggage issues
* Generally positive sentiment (picked up of course from the reviews with higher ratings)

Since the majority of reviews had lower ratings, I also applied LDA to reviews with less than or equal to 2, I found the following four topics:
* Negative sentiments related to their experience flying with the airline
* Luggage and baggage issues
* Boarding pass, credit card, and flight/ticket information access 
* Mobile application issues around login and passwords

Of course we want to highlight reviews that relate to the mobile application since that's the domain of where we analyzing. Tangible issues such as luggage and baggage may not always be related to the mobile application.

## Model Performance for Lime & Shap Analysis:
Using Logistic Regression, I obtained the following accuracies when setting the target to rating (sentiment) and topic (topics obtained by LDA) respectively:

Accuracy with Rating as Target: 87.12%

Accuacy with Topic as Target: 82.05%

## Future Improvements
With the AppStore scraper, I was only able to scrape a certain number of reviews despite the sleep time between scraping attempts. I believe I could obtain a better holistic view of the reviews if I was able to scrape more reviews and would have resulted in a more accurate depiction of what I wanted to get out of this project.
