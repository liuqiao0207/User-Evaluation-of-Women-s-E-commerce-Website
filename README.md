# User-Evaluation-of-Women-s-E-commerce-Website
User Evaluation of Women's E-commerce Website
## Task 1 - Analysing the product reviews
In this project, you are supposed to analyse product reviews and extract helpful information from them. The case we are studying here is the review dataset of women’s clothes that are sold by a company online. In the file `WomensApparelReviews.csv`, you are given over 23000 reviews that are real but anonymized. The columns of this dataset are the following variables:


**Product ID**: integer variable that refers to the specific item that is reviewed.

**Age**: the reviewers age.

**Title**: the title picked by the reviewer (some reviewers didn't pick any titles).

**Review Text**: the body text of the review.

**Rating**: the product score given by the customer from 1 (worst), to 5 (best).

**Is it Recommended?**: the customers are asked whether or not they recommend the product. 1 means the product is recommended, 0 means not recommended.

**Department**: the products are classified in different departments such as dress, top and ...

A major part of this task is analysing the review text and deciding how positive or negative it is. To that end, there are two more data files: `positive-words.txt` and `negative-words.txt`, which contain lists of positive and negative words, respectively. These words come from the paper by *Minqing Hu and Bing Liu. "Mining and summarizing customer reviews." Proceedings of the ACM SIGKDD International Conference on Knowledge Discovery & Data Mining, Seattle, Washington, USA, Aug 22-25, 2004*. You will need to invent a metric for how positive or negative "Review Text" is, based on how many of the words in it are in the positive/negative word lists. For instance, is a review containing one positive and one negative word: overall positive, negative or neutral? - try and develop a single measure based on the word occurrences that will describe the positivity/negativity of the review. You can also decide if a "Title" is positive, negative or neutral by searching for them in the lists of positive and negative words. Once you have developed one positivity/negativity measure can you think of other measures that you could compare?

This project is open-ended, so you can come up with your own ideas to analyse the dataset and extract useful information or interesting facts. However at least one of the ideas you present should make use of the positive and negative word lists for analysing the reviews text. Here are some questions you might address in your analysis (of course you are not limited to just these questions):

- What is the age distribution of customers?
- What is the most popular item in each age group? (you can classify the ages however you think appropriate - be sure to justify what you do).
- Using the measure of negativity or positivity that you define, rate the reviews. You can also decide whether a title is positive or negative. Are the negativity-positivity of the titles and that of the review texts correlated? 
- What is the average rating in positive, negative or neutral reviews?
- Is the rating correlated to your measure of negativity-positivity? 
- Are there many outliers who wrote a negative text but left a high rating (or vice versa)?
- Which product attracted the most positive reviews? This would help the company to focus more on the product that people liked or make changes to the product that people did not like. Is there any such advice you could give them on the products that could come from the reviews?
- What is the most recommended product? What is the least recommended product?
- Which group of reviewers wrote a longer text in their review? Do unhappy customers write longer reviews or satisfied customers? 
- Which age group uses more positive words? Which age group uses more negative words?
- Are older people more inclined to recommend a product or younger people?
- Is it true that unhappy customers use more capital letters? or it is the other way around?
- Can you come up with a way to consider the positive words in a negative statement negative? For example, "Not impressed or satisfied" is a negative title, but if you just count the positive and negative words, you will find two positive words ("impressed" and "satisfied") and a negative word ("not"). Hence, just based on the word count, you might wrongly find the title to be positive. This might be easier for the titles, but you can also break down the review text to sentences and apply your method there.
## Measurement of the text
### 1. Using the amount of positive words and negative words to measure
### 2. Improvement: considering the effect of  Negative Words and Gradable Adverbs words

The easy way: First we define the function **`howmany(a,b)`** to calculate how many positive or negative words are seperately in each test. Then we use the amount of positive words minus the amount of negative words to get the measurement for this test. And the result is this test's emotion mark. And the result for function is called `'number_title'` for title and `'number_comment'` for reviews.

Improvement: we consider this question as an accuracy question, which means if we can take more than positive or negative words into consideration, we will get a more accurate emotion mark for this text. Therefore, we begin to consider the negativng words such as not, don't, aren't, etc. We download the **`NegatingWordList.txt`** which contains many negating words from this website: http://sentistrength.wlv.ac.uk. Then we want to consider the gradable adverbs because 'extremely good, very good and good' should have different emotion mark. Therefore we create **`adv-words.txt`** on our own which contains over 50 gradable adverbs. Now each text needs to go through 4 word list txt to get the emotion mark. And the function is **`whatpoint(a,b)`**. and the result is called `'point_title'` for title and `'point_comment'` for reviews. We use the positive points minus negative points to get the final emotion mark for this text.

A simple example with the function *whatpoint*: extremely good = 3; very good = 2; good = 1; partly good = 0.5; not good = -1; not very good = -1; bad = -1, very bad = -2, extremely bad = -3.

First we clean the data whose reviews and titles are blank. Second we read and turn **`positive-words.txt;negative-words(1).txt;NegatingWordList.txt;adv-words.txt`** into lists. Third we create funtion whatpoint() and howmany() to get the emotion mark for each text. Fourth we use new lists to collect the results of the functions and add new column on the pd.read dataframe, `'number_title'`, `'point_title'`, `'number_comment'`, `'point_comment'`.

It takes about 2.5 minutes to get the 4 new lists of the emotion marks for title and reviews under different measurements.

