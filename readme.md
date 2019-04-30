# Project Report
The amount of misinformation spread on the social media platform and by the media houses has increased a lot in the recent past. 
Our society is in a grave danger because of the amount of misinformation spread since it can create mass hysteria, hatred and communal violence or polarization of votes during election based on incorrect data. 

However, in order to start addressing this problem, we need to have an understanding on what Fake News is. Only then can we look into the different techniques and fields of machine learning (ML), natural language processing (NLP) and artificial intelligence (AI) that could help us fight this situation.

So, what exactly is fake news?
Fake news can be of different types such as 
1.	Satire or Parody which has no intention to cause harm but has potential to fool
2.	False connections when headlines, visuals or captions don’t support the content
3.	False context when genuine content is shared with false contextual information
4.	Etc 


Different problems require different solutions; 
Here we are targeting on the fake news related with False connections with headlines and the one with false contextual information. 

A similar dataset on Kaggle which has two news headlines and the first headline has been confirmed as the fake news. The problem states that given the title 1 as fake news, classify title 2 as unrelated, agreed or disagreed. 
This won’t solve the entire problem but it gave us a head start to us for approaching this problem. 



#### Twitter Sentiment Analysis on Indian Election 2019


In this project, we have done sentiment analysis of the upcoming Lokshobha Elections for the political parties Congress and BJP by crawling tweets from different hashtags of either parties, party leaders, as well as news hashtags. The sentiments analysed covers different user-reactions. 

We have categorised the analytics into 3 sections:

1. Crawling, cleaning data and labelling un-structured data by using/mapping known English words from various sources

2. Applying Natural Language based classifiers used for text processing to train tweets and predict moods

3. Applying standard machine learning algorithms and deep learning to do multi-class mood classification for 2 prominent parties in the election

![Alt text](images/Report_1.png?raw=true "Title")


##### 1. Crawl Weekly tweets and Merge:

We crawl tweets on a weekly basis and merge them with previous weeks to have an overall prediction over a period of few months. The system is designed to learn from tweets every week and consolidates results by eliminating duplicate tweets. It preserves the retweet counts to understand the impact of higher number of retweets.


##### Crawl Mood Words and labelling unstructured data:

The mood vocabulary is built using english word repository available in the internet. The following mood labels Joy, Sadness, Arousal, Dominance, Neutral, Anger, Fear, Faith(Support) were assigned to tweets by taking the strongest mood in the sentence, by taking each word from the sentence into account, along with the emoji in consideration. For example, the overall mood of the sentence is Dominance when each word in the sentence have the following moods.

[‘dominance’, ‘dominance’, ‘dominance’, ‘dominance’, ‘dominance’, ‘joy’, ‘arousal’, ‘dominance’]

The sentiment of each word is derived by assigning an affectual score to it . The lexicon dictionary for 25,000 words are dowloaded from NRC Word -Emotion Association Lexicon (Reference 2). If certain words in a sentence are missing from Vader or the specific mood type is missing, TextBlob is used to determine positive/negative sentiment of the word. For example, for the following tweet “I request all fellow Indians to get rid of this clown coming elections. Please vote wisely”, the word “wisely” encounters a Valence score of 0.878, but it does not differentiate between positive (Joy)/negative (Sadness/Anger) mood, which necessitates a further lookup of word polarity through TextBlob. Finally with a positive score of 0.7 its labelled as sentiment of “Joy”.

While affectual score and TextBlob determines mood of each word, SentimentIntensityAnalyzer is used to calculate the overall polarity of a sentence. It uses Vader’s lexicon (Reference 2) which rates individual words (present in the lexicon) in a sentence on a scale of highly negative to highly positive.

For example, for a tweet, “We stand rock solid behind you @narendramodi Our party has performed well under all odds, we will do better in” has few words in the lexicon with score as “solid”: 0.6, “party” : 1.7, “well” :1.1 and “better” 1.9

These word ratings help to derive four sentiment metrics to represent the proportion the tweet falls under it.

‘compound’: 0.8074, ‘neg’: 0.0, ‘neu’: 0.632, ‘pos’: 0.368

This explains the tweet is how much positive, negative or neutral. The compound score have been standardised to range between -1 and 1 and is calculated by calculating the normalized sum (normalize(sum_s)) of all of individual word ratings (0.6, 1.7, 1.1, 1.9) present in the lexicon.


All tweets vary in intensity from -1 to +1. As the below figures shows strong positive sentiments like “Joy” and “Faith” incline more 0 to +1 for both BJP and Congress, while negative sentiments like “Anger” and “Sadness” incline more between -1 to 0. “Neutral” sentiment is centred around zero. Sentiments like “Arousal” and “Dominance” are more or less distributed equally between -1 to +1 which signify they can be either tweeted in a positive or negative mind.

For example, the tweet “In 2014 when Modi elected PM candidate, people eected change will happen” records “Dominance” with positive sentiment . While the tweet “2019 elections will be fought on completely different lines’, says @amitmalviya, National Spokesperson, BJP in conversation” records a negative sentiment because of the word “fought”. SentimentIntensityAnalyzer calculates the compound metric of the tweet as -0.3182, while positive, negative and neutral scores are 0.0, 0.247 and 0.753 respectively. Further rating the word “fought” in terms of “Valence” — (Joy/Sadness/Anger/Fear/Faith), “Arousal” or “Dominance”, the measuremnets are “Valence” : 0.531, “Arousal” : 0.809, “Dominance” : 0.868, justifying the predominance of “Dominance” mood.

Similarly, both positive and negative sentiments can be observed with “Arousal” mood. “Arousal” incorporates any feeling that causes state change or prompts to rise and undertake any activity. The tweet “Govt today introduced a bill in to make provisions regarding recognition of, drawing opposition from the as well as the CPI(M) which staged a walkout calling it a ‘draconian and unconstitutional’ legislation” records a compound score of -0.3182 showing a negative “Arousal” sentiment. While the tweet “God bless you all. Now do the job well, Dems, it’s been way too long since it was done properly. Show them how it’s done” is a positive “Arousal” sentiment with a compound score of 0.95 .

![Alt text](images/Report_2.png?raw=true "Title")


The upper and bottom figures demonstrate how sentiments differ for Congress and BJP. The most visually distinguishing aspects are seen in the 2 sentiments “Faith” and “Arousal”. BJP records a higher recording in “Faith” while Congress shows higher predominance of “Arousal”.

![Alt text](images/Report_3.png?raw=true "Title")

The following figure illustrates tweet that belongs to both BJP and Congress. “Dominance” is still seen as the predominant mood. A sample tweet involving both parties : “Very close fight in . The difference between BJP and Congress not too many seats” — — clearly shows close and stiff competition between the two.

![Alt text](images/Report_4.png?raw=true "Title")

#### Tweet Analytics
In this section, we structurize the blog into different areas of analytics and provide visual representations for comparisions.

1. Frequency of different Moods
2. Sentiment representation by Word Cloud
3. N-gram model
4. Location-wise tweet distribution
5. Retweet frequency distribution

##### Frequency of different Moods

The different mood frequencies show public reactions towards both the parties before elections. “Dominance” mood dominates in case of both the parties followed by “Joy” mood. SNS countplot provides functionality to plot total frequency distribution of each individual mood which helps to compare within party different moods as well compare a specific mood for both the parties. For instance, for the following graphs of BJP and Congress shows the total number of tweets received for BJP is more than Congress and consequently each corresponding mood gets a higher percentage of tweets for BJP than Congress.

![Alt text](images/Report_5.png?raw=true "Title")
![Alt text](images/Report_6.png?raw=true "Title")

#### Sentiment Comparisions
Sentiment Representation by WordCloud
The different kinds of tweet sentiments are represented by means of different WordClouds. WordClouds are ideal representatives of labelled sentiments as the most common words specific to a mood appear bigger and bolded than other less frequent words. WordClouds are fast and easy mechanism of representing the most relevant words for a theme or context. Its one of the most convenient ways to convey information visually appealing and engaging manner.

Here 2 different sentiments of BJP “Faith/Support” and “Fear” are represented by 2 different WordClouds.

From the figure below, it can be observed that certain words of BJP like “modi”, “pm” are more frequent and the tweets exibit a tendency to “support”, “congratulate” , “thank” Prime Minister Narendra Modi for country’s development. Words like “vikas”, “development”, “honest team” , “agree”, “sath” , point out positive sentiment towards Modi government. Futher tweets that honour Prime Minister, are visible though words like “hon pm”, “dearest”, “fan”.

![Alt text](images/Report_7.png?raw=true "Title")


One kind of negative sentiment like “Fear” for the BJP government is analysed and represented through a separate WordCloud. The “Fear” WordCloud shows a kind of negative feeling, fear/threat in people’s mind from opposition parties.


The “Fear” WordCloud has prominent bolded words like “worry”, “failure”, “mistrust”, “fighting” “worried” , “unexpected” , “wounded” that raises questions about doubts and uncertainities in people’s minds.

![Alt text](images/Report_8.png?raw=true "Title")

Similarly, doing the sentiment analysis for Congress, 2 different moods one Positive — Joy and another negative -Sadness are represented by means of WordCloud. The “Sadness” WordCloud of Congress have clearly distinguishable words like “lost”, “refused”, “defeat”, “destroy”, “crying”, “missed”, “loot”, “slaps” that remark a sense of negative disheartened feeling in the tweets. Further the occurrence of most frequent words “Gandhi” , “Rahul” shows Rahul Gandhi as one of the foremost leaders of Congress.

![Alt text](images/Report_9.png?raw=true "Title")

The positive tweet sentiments for Congress are represented by means of “Joy” WordCloud. Similar to the previous WordCloud “Rahul Gandhi”, “Congress” dominates the word cloud.

Words like “win”, “good”, “congratulation”, “great”, “truth”, “happy”, “love”, “victory”, “dancing” , “grand” , “cheer” , “laugh” exhibits a strong “Happy” and “Joyous” public sentiment for Congress.

![Alt text](images/Report_10.png?raw=true "Title")

#### N-gram Model
The most popular bag-of words in NLP has n-gram models comprising of 1 -word text (Unigram) , 2-word text (Bi-gram) , 3-gram text (Tri-gram), where the number of occurrences of single word, side-by-side 2 words, side-by-side 3 words are counted and fed as feature-vectors to Text Classifiers (Naive Bayes, Maxium Entropy and Support Vector Machines). Word occurrences are counted after cleaning the tweets from hashtags, urls, emojis stopwords and character repeatations. This helps to extract most popular 1-word, 2-words, 3-words from tweet and construct feature vectors to determine the overall sentiment score of the text.


Similarly, Bigram Frequency Distribution for Congress and BJP shows the most dominant 2-word occurring in the respective tweets.

![Alt text](images/Report_11.png?raw=true "Title")
![Alt text](images/Report_12.png?raw=true "Title")
![Alt text](images/Report_13.png?raw=true "Title")

#### Location wise tweet distribution
A pie-chart is constructed for each of Congress and BJP by taking into account percentages of tweets from some of the known states of India. While both of them have larger percentages of tweets from unknown location and unknown states of India, New Delhi, Mumbai and Bangalore still dominates the percentages of tweets from India.

![Alt text](images/Report_14.png? "Title")
![Alt text](images/Report_15.png? "Title")

#### Retweet Frequency Distribution

The popularity of tweets have been represented with the retweet count . Only first 25 unique retweets are selected. Its seen, that BJP tweets are much more frequent than Congress and ranges between 100–250 while average retweet frequency for Congress is 20–30. The retweet frequency along with the tweet text have been graphically displayed below.

![Alt text](images/Report_16.png?raw=true "Title")
![Alt text](images/Report_17.png?raw=true "Title")

### Conclusion
This part of the project mainly focusses on labelling tweets from known word dictionaries and rating them between -1 and 1 . It further compares BJP and Congress side by side considering tweet sentiments, frequency of different tweet sentiments, commonly used words in tweets (anargrams 1–2 words), location of users who tweeted as well as the most popular tweets obtained from the retweet count. The following posts will cover on different ML techniques used for NLP, comparing them side by side with different metrics of accuracy like Precision , Recall and F1 Score as well as processing time to train the models. The election results for 2019 is still a month to go and the study hopes to find more interesting results through more weekly tweet crawls.

Reference:

Norms of valence, arousal, and dominance for 13,915 English lemmas. Warriner AB1, Kuperman V, Brysbaert M.
https://saifmohammad.com/WebPages/NRC-Emotion-Lexicon.htm

Disclaimer Statement:

The work analyses tweet of 2 prominent parties for the upcoming election. We have no intention to create controversy in people’s mind or hurt anybody’s feelings or incite feelings of anger or hatred. Its purely done for academic, research and information purposes and somebody else might get different results on application of other techniques of analysis. Its an unbiased and impartial summary and does not discriminate/differentiate any individual or group.
