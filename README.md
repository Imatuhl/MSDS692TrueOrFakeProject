# News: Fact or Fiction Using 
Nueral networks, Transfer learning and machine learning techniques to classify news articles

Introduction:
With the rise of sensationalist news, outrage culture, and the election of Donald Trump as president many news outlets have been accused of publishing fake news. These factors along with foreign influencers have contributed to growing uncertainty surrounding news sources and ttheir credability.

This project aims to using machine learning and natural language processing techniques to analyze news articles so that they can be classified as either fact or fiction. 

## The Data
The data set being analyze was obtained from Kaggle titled "Fake and real news dataset". The dataset includes 20826 randomly obtained factual news articles and 17903 randomly obtained fake news articles. The original categories of the data set include artciles from world news, government news, politics, sports, entertainment, US News, Left news and middle eastern news. There are four variables in the dataset title, text, category and date. 

Fake news articles
![GitHub Logo](/images/FakeNewsHead.png)

Factual news articles
![GitHub Logo](/images/FactualNewsHead.png)

After reviewing the dataset the date and category variables will not help much with our analysis so they will need to be removed.

## Exploratory Data Analysis

Initial exploration of the data will show that there are a number of different categories in this data. The Fake news set has several categories within the set that may not necessarily contribute to the analysis. 

Fake News Articles

![GitHub Logo](/images/Articlegraph1.png)

True News Articles

![GitHub Logo](/images/truearticle1.png)

Next counting the articles we can see that the true and false dataset are almost balanced.

![GitHub Logo](/images/article_count.png)

To gain an understanding of what might constitute a fake news article and what might make up a true article word clouds can be created to see the frequency of words in these articles and might display a trend between the two types of articles.

Fake News WordCloud

![GitHub Logo](/images/fakewordcloud.png)

True News WordCloud

![GitHub Logo](/images/truewordcloud.png)

Since the data was into two separate files they needed to be merged so that they could be classified once merged we can see that the sets are balanced and fit into a number of different categories.

Merged data categories:

![GitHub Logo](/images/mergedcategories.png)

After removing all of the categories that will not help with the analysis we add in our own category of 0 for false news and 1 for true news. 

![GitHub Logo](/images/mergedtruefalse.png)

Finally, creating a wordcloud of the merged set might tell us more about how the articles look as a whole.

![GitHub Logo](/images/mergedwordcloud.png)

What I found was the Donald Trump was one of the most frequent word combinations in the fake news category and when merged with the true dataset was one of the most used overall. What this tells me is that there could be an overwhelming amount of fake news articles that mention President Donald Trump. This could be due to news outlets publishing anything they hear about the President in order to get the attention of its readers.

## Data Cleaning

Since the text of each article was in a raw format it needed to be cleaned in order to analyze it. Stopwords, whitespace, punctuation and capital letters all needed to be removed to obtain an accurate classification. Using the nltk package all of these items were removed from the text. Next the data was tokenized so that it can be fed into the convultional neural network.

## Building the model

To build the model the Keras libraries were used to create a 1d Convolution neural network. A 1d network was used because it is better at analyzing linear data such as text. Initially the model I created used Conv1d, MaxPooling1d and BatchNormalization layers. The model had 32 and 64 nodes in each layer to analyze the data. This initial model only achieved a 51% accuracy rating. Adjusting the number of nodes and layers in the model achieved better results. I removed the MaxPooling layers and some of the BatchNormalization layers and the new model achieved an accuracy rating of 99.6%.

![GitHub Logo](/images/conv1dnet.png)

![GitHub Logo](/images/conv1dvalidloss1.png)

![GitHub Logo](/images/conv1daccvalid1.png)

![GitHub Logo](/images/conv1dresult.png)

After achieving a higher rate of accuracy I imported the GloVe embedding data to complete a transfer learning experiment. GloVe is a neural network developed by Stanford to complete text analysis. GloVe uses related words to and vectors to analyze relationships between words to classify the data. This experiment imports the GloVe network weights into dense layers to analyze the data. This experiment achieved an accuracy rating of 99.1%

![GitHub Logo](/images/glovevalidacc1.png)

![GitHub Logo](/images/glovevalidloss1.png)

![GitHub Logo](/images/gloveresult.png)


## Comparing the results

Both of these models performed well for this experiment and the difference in performance is negligable. One major difference between the models I observed was the GloVe transfer learning experiment looked to be more stable than the conv1d network. Large spikes in the validation loss of the convolutional network were a frequent occurance when training the model while the GloVe model was very consistant through out training. I created heat maps to better visualize how the models performed. 

![GitHub Logo](/images/conv1dheat.png)

![GitHub Logo](/images/gloveheat1.png)

Finally, comparing these models to other machine learning techniques shows that these methods are comparrable to other methods and may slighlty outperform some.

Support Vector Machine

![GitHub Logo](/images/svmpic.png)

Bernoulli Naive Bayes 

![GitHub Logo](/images/naivebayespic.png)

Logistic Regression 

![GitHub Logo](/images/logregresspic.png)

## Model Expansion Ideas

This model could be expanded by paring it with an IP address algorithm that can detect where a parrticular article is coming from, which could help with determing if a foreign actor is trying to spread false influence. Additionally, We could try identifing these types of fake articles coming from our own sources like Fox News MSNBC or CNN. Another idea for expanding this model is using a database of buzzwords to detect if these articles are using particular words to spark outrage. 
