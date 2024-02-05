# Analyzing Facebook Group posts ["Belarusians in Warsaw"](https://www.facebook.com/groups/322757917839370)


This project focuses on a comprehensive analysis of the Facebook group "Belarusians in Warsaw" using text mining techniques. The exploration spans various aspects, from demographic insights to sentiment analysis and topic modeling.
The aim is to make decisions regarding which algorithms can be used in tasks such as clustering of **short textual documents sourced from social networks**.

## Data Collection and Preprocessing:

The project starts with web scraping techniques to collect data from the Facebook group . To obtain the corpus in the project, an extension for the Google Chrome browser called Instant Data Scraper was used.
The dataset was collected on a monthly basis and stored in .XLSX files from January 2021 to July 2022. The corpus of unstructured data in the .XLSX file contained 14,536 rows of posts:
![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/022eff91-1adb-4183-bb37-233e230e5d3a)

The preprocessing of data is a crucial step in cleaning and preparing text for classification. When dealing with raw text from online sources for further analysis, it's essential to create additional functions to:

- Remove URLs, hashtags (e.g., #topic), and user identifiers (@username).
- Correct typos.
- Remove symbols, emoticons.
- Remove spaces (whitespaces).
- Remove punctuation marks, special characters (: \ | [ ] ; : {} - + ( ) < > ? ! @ # % *, etc.), ASCII characters, numbers, ellipses.

## Textual Data Processing:

A significant portion of the project revolves around handling textual data. This includes steps such as tokenization, lemmatization, and cleaning of posts to prepare the data for further analysis.
A typical text data processing pipeline involves several steps to clean and prepare the text data for analysis. Here's a simplified representation of a text data processing pipeline:

![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/083ca317-6744-4931-9fa7-613994fb5a52)

## Lemmatization Libraries for Russian Language in Python:

For lemmatization in Python, several libraries have been developed. Unfortunately, most of them do not support the Russian language, and if they do, the results may be unsatisfactory. Among these libraries are nltk (nltk.stem.snowball) and spaCy (spacy.lang.ru). The following will discuss the two most popular syntactic analyzers for the Russian language:

**Pymorphy:**
Pymorphy is an open-source syntactic analyzer that provides all the functions of full morphological analysis and word form synthesis. It is based on dictionary morphology and utilizes the dictionary data of the OpenCorpora project, consisting of 391,842 lemmas. Pymorphy2 is continuously maintained, and the OpenCorpora framework is regularly updated, enhancing the accuracy and completeness of syntactic analysis.

**Pymystem:**
Pymystem is a syntactic analyzer developed by Yandex. The first version was released in June 2014. The current version, Pymystem 3.1, offers all the features of full syntactic analysis but lacks synthesis functionality. It relies on the national corpus of the Russian language11, comprising 1.5 billion words. The package is open source under the MIT license. However, it's essential to consider that Yandex Mystem is not open source and is licensed according to Yandex's terms. To work with the Pymystem3 tool, you need to use the Mystem wrapper.

*Both libraries mentioned above work well, but when dealing with large datasets, it is better to utilize Pymystem3. In this project, the Pymystem3 analyzer was employed.*

## Basic Statistics for the Structured Dataset:

In this section of the project, distributions related to post frequency, language usage, and post length over time were presented. 

**Distribution of Single Posts for Each Day from January to July 2022**

![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/93b05dae-a479-4a10-8d11-fe0aca7d8020)


**Distribution of the Average Number of Comments Each Day**

![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/d7c0de17-10ad-4142-bf22-45eb142b669e)

The figures illustrate significant differences in the number of published posts over the months from January to July 2022, primarily attributed to the onset of the war in Ukraine. 

**Distribution of positive and negative sentiments in the discussion within the "Belarusians in Warsaw" group over the months from January to July 2022**

![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/d230c40a-cebe-4a25-ae81-a68528dec2bb)


## Sentiment Analysis:
The sentiment analysis section evaluates the emotional tone of posts using various sentiment classifiers, including TextBlob, dostoevsky, and VADER. These figures depict the distribution of positive and negative sentiments, offering a nuanced understanding of the group's dynamics.

The dataset consists of 97 comments and includes the columns "comment," "likes," and a column with polarity assessed by the project author – "my_polarity." Values in the "my_polarity" column indicate
- Positive: 1
- Neutral: 0
- Negative: -1

1. **TextBlob:** A library based on the NLTK package and a dictionary with labeled polarity. It utilizes the Naive Bayes Classifier for sentiment analysis[^20^].
2. **dostoevsky:** A library based on the dictionary from the Russian text corpus RuSentiment, which has labeled polarity. RuSentiment is constructed from 31,185 posts from the Russian social networking site vk.com [^21^].
3. **VADER (Valence Aware Dictionary and sEntiment Reasoner):** Part of the NLTK library, created as a tool for analyzing data from social media[^23^].

[^20^]: https://textblob.readthedocs.io/en/dev/
[^21^]: https://github.com/bureaucratic-labs/dostoevsky
[^23^]: https://github.com/cjhutto/vaderSentiment


The **TextBlob** and **VADER** libraries do not perform sentiment analysis on Russian-language expressions but have a translation function to English. Therefore, for determining polarity, translations of the original texts were used.

**Prediction Results Table using TextBlob, dostoevsky, and VADER Libraries for All Three Sentiment Classes**
|                 | TextBlob              | dostoevsky            | VADER                |
|-----------------|-----------------------|-----------------------|----------------------|
| **Negative**    | Precision: 0.35       | Precision: 0.57       | Precision: 0.54      |
|                 | Recall: 0.32          | Recall: 0.55          | Recall: 0.64         |
|                 | F1 Score: 0.33        | F1 Score: 0.56        | F1 Score: 0.58       |
| **Neutral**     | Precision: 0.40       | Precision: 0.41       | Precision: 0.67      |
|                 | Recall: 0.21          | Recall: 0.83          | Recall: 0.21         |
|                 | F1 Score: 0.27        | F1 Score: 0.55        | F1 Score: 0.32       |
| **Positive**    | Precision: 0.49       | Precision: 1.00       | Precision: 0.65      |
|                 | Recall: 0.71          | Recall: 0.17          | Recall: 0.94         |
|                 | F1 Score: 0.58        | F1 Score: 0.29        | F1 Score: 0.77       |



## Topic Modeling:
The latter part of the project dives into topic modeling using techniques like CountVectorizer, TF-IDF, Gensim and GSDMM. 
The algorithms identified topics within the Facebook group, providing a glimpse into the prevalent themes of discussions.

The goal is to find the best algorithm for short text modeling, and one such model is the GSDMM (Gibbs Sampling Dirichlet Multinomial Mixture) proposed by Jianhua Yin and Jianyong Wang in 2014. Short texts, often originating from microblogs, online reviews, and social networks like Twitter, Facebook, Reddit, and Stack Overflow, pose a unique challenge due to their sparsity, heterogeneity, and noise.

*Clustering short texts differs from clustering regular texts. In short texts, most words occur only once, making traditional techniques like TF-IDF inadequate for capturing infrequent words. It's worth noting that the LDA (Latent Dirichlet Allocation) algorithm, performs well with larger documents but faces challenges when dealing with shorter texts or sparse text data. This becomes a significant concern given the prevalence of short text data from social networks today.*

The fundamental principle of GSDMM is described through an analogy known as the *"film group approach."*
Let's envision the input data as a group of students (documents). Each student (document) is represented by a short list of favorite movies (words). The goal of this approach is to divide students (documents) into several groups so that students (documents) within the same group are similar, while those in different groups are dissimilar. 

Let's define the set of different movies (words) as *V*. Although each short document has only a small number of words (the average word count is often less than **10^2**), it is represented by a vector of size *V* (often larger than **10^5**).

Imagine a professor inviting students to a massive restaurant and randomly assigning students to K tables. The professor then asks students to re-select a table based on 2 rules:

1. Choose the table with the most students.
2. Choose the table where students have similar interests to yours (i.e., watched the same movies).As the professor repeats the instructions, the number of students at some tables will increase, while at others, it will decrease. Finally, only some tables will still have students, and students at each table will have similar interests. The rules of the "film group approach" are naturally linked to clustering goals: completeness and homogeneity.

The following features can be highlighted for GSDMM: the algorithm automatically selects the number of clusters, handles the sparsity and high dimensionality problem, and, like LDA, can present words belonging to each cluster.

**Distribution of Topic Occurrences According to the GSDMM Model**
![image](https://github.com/AnaSmola/Text_mining_in_posts_analysis/assets/94449616/47f26fb1-f297-477e-bd14-efc7f10d715b)

