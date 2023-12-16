I trained a Multinomial Naïve Bayes Classifier on a ISOT Fake News dataset (https://onlineacademiccommunity.uvic.ca/isot/2022/11/27/fake-news-detection-datasets/) consisting of 17,455 fake news articles and 21,192 true news articles converted into a bag-of-words representation, achieving a classification accuracy of 94%. Extracting the top features used for fake versus true classification and applying a sentiment analysis model to produce sentiment scores of the top 100 words associated with each class demonstrated that on average, words associated with fake news expressed 10x more negative sentiment than the words associated with true news. Overall, this model is effective at fake news detection, and the computational results of this study are in line with psychologists’ beliefs.


Methods: 

Dataset: 
I used the ISOT Fake News dataset (Fake News Detection
Datasets, n.d.), which contains 23,481 fake news articles
collected from unreliable websites flagged by PolitiFact and
Wikipedia, and 21,417 true news articles from Reuters.com,
all collected between 2016 to 2017. I removed all articles that
had duplicate text, leaving 17,455 unique fake news articles
and 21,192 unique true news articles. While the dataset
included the title, text, type, and date of the article, I only
used the title and text for this study, combining the two to
represent the text of the entire article.

Cleaning the Data:
I began by shuffling the rows of the dataset, to ensure that
order of the data doesn’t introduce any biases. I then cleaned
up the text by only allowing words in the English dictionary
and removing “(Routers)” tags which were frequently in the
true news articles, and “bit.ly” links which were frequently in
the fake news articles.

Converting Text to Bag-Of-Words (BoW) Representation: 
I split up 80% of the data into a training set and 20% of the
data into a testing set, using an arbitrary random_state of 42.
I then used a CountVectorizer to tokenize the text, build a
vocabulary of known words, and count the occurrence of
each word in each article. I fit the CountVectorizer to the
training data (X_train), transforming the text into a BoW
representation. The BoW representation is a sparse matrix
where each row corresponds to an article, each column
corresponds to a unique word in the vocabulary, and at the
intersection is how many times that word appeared in that
article. I then transform the test data (X_test) using the
vocabulary learned from the training data, ensuring that the
same set of features (words) is used for training and testing.
The number of vocabulary words in the training data was 24,202.

Utilizing a Naïve Bayes Classifier: 
I then created and trained a Multinomial Naïve Bayes
Classifier using vectorized training data, so that it learns the
relationships between the features (word counts) and the
labels (classifications) based on the training set. Finally, I use
this trained model to make predictions on the vectorized test
data.

Extracting Most Important Features: 
I first extract the feature names from the CountVectorizer.
I then get the log probabilities for each feature (word) for
each class (Fake versus True). I calculate the feature
importance scores by subtracting the log probabilities of the
“Fake” class from the log probabilities of the “True” class,
the resulting scores representing the contribution of each
feature to the likelihood of a news article being classified as “True.” Therefore, the most positive features (words) will be
most associated with true articles, and the most negative
features will be most associated with fake articles.

Evaluating Sentiment Scores of Words: 
I used the pre-trained sentiment analysis model Valence
Aware Dictionary and sEntiment Reasoner (VADER) to
analyze the sentiment/emotion associated with each word.
Each word is calculated a sentiment score ranging from -1
(most negative sentiment) to 1 (most positive sentiment).

Results:

The Multinomial Naïve Bayes Classifier was able to
classify fake and news articles in the test set with 94.02%
accuracy. Broken down by each class, the model was able to
predict fake news with .94 precision, .93 recall, and an f1
score of .93, among 3486 fake articles in the test set. The
model was able to predict true news with .94 precision, .95
recall, and an f1 score of .95, among 4244 true articles in the
test set. A confusion matrix displays that 3233 fake news
articles were correctly classified as fake (true negative), 253
fake news articles were incorrectly classified as true (false
positive), 209 true news articles were incorrectly classified as
fake (false negative), and 4035 true news articles were
correctly classified as true (true positive). Overall, the model
performs well at classifying true versus fake news, with high
accuracy, recall, and F1-scores for both classes.

After extracting the most important features, aka the
features (words) that are most associated with fake versus
true classification, it was clear that the top words associated
with fake news are less professional and more emotional, and
more often adjectives, than the top words associated with true
news. Among the top 20 words associated with fake news
were “hilarious”, “creepy”, “idiotic”, and “narcissistic” for
example. Meanwhile, among the top 20 words associated
with fake news, were places like “Barcelona” and “Bali” and
more neutral and professional terms like “accession” and
“provincial”.

After conducting sentiment analysis on the most frequent
20 words linked to true and fake news, a notable pattern
emerged. The words associated with true news consistently
yielded a sentiment score of 0.0, indicating a neutral sentiment. In contrast, the words tied to fake news exhibited
greater variability in sentiment scores, ranging from negative
to positive.

Among the top 100 words associated with fake news, the
average sentiment score was approximately -0.071, with a
median of 0.0 and a standard deviation of 0.237. In
comparison, the average sentiment score for the top 100
words associated with true news was around -0.006, also with
a median of 0.0, and a standard deviation of 0.046. This
suggests that, on average, words linked to fake news convey
sentiment that is ten times more negative than those
associated with true news and displays a higher overall
variance from neutrality.

Read my whole paper here: https://drive.google.com/file/d/1udVaVI3LWE5XdpW_kpXZrRv0HCUax7F3/view?usp=sharing
