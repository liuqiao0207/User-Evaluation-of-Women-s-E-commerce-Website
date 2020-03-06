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
### 3. Sales volume by department

The chart below shows the proportion of sales in different departments. As you can see from the pie chart below, the Jackets department has the highest sales volume, accounting for 44.6%, which is the largest proportion. Jackets department was followed by Dresses, Intimate, accounting for 26.9% and 16.2% respectively. This was followed by the Bottoms and Tops divisions, which accounted for 7.4% and 4.4% respectively. The Trend department accounts for the smallest proportion , which accounts for only 0.5%. Therefore, the company should continue to maintain the sales of the Jackets department, while focusing on rectifying and improving the Trend department, thereby improving the company's performance.
### 4. Top five products with the most sales

The chart below shows what the top five products are. As can be seen from the figure below, the product with the product ID of 1078 has the highest sales volume, followed by the products of 862, 1094, 1081, and 872. Therefore, companies should focus on the top five products.
### 5. The highest and lowest rating product

The following shows the highest rated products and the lowest rated products. For products with high scores, the company should continue to make it a star product of the site. For products with low scores, companies need to find reasons for customers' dissatisfaction and low scores, improve or directly remove these products, and enhance customer satisfaction. There are almost 400 products which are ranked at 5, but many of which are actually have only 1 customer.
### 6. What is the age distribution of customers?

The following shows the age distribution of customers. By segmenting the age of the customer (the segmentation standard refers to https://zhidao.baidu.com/question/217291248.html ),
the age range can be cut in 0-12 years old for children's wear, 13-20 years old for youth, 21-30 years old for young ladies, 31-45 years old for middle-aged wear and 46 years old and older for old age. As can be seen from the figure, the main customers of the website are middle-aged and elderly people aged 31-45 and older, followed by young people aged 21-30, and almost no one is 0-12 years old and 13-20 years old. It can be seen that the target group of the website is middle-aged and elderly women. The 31-45-year-old group is also the group with higher consumption in the women's clothing market. They have stable work, certain economic ability, stress on life and high requirements for clothing value. The demand for old people's (45 years old) Above) clothing is not large, and the purchase desire is this group is low. However, the 31-45-year-old group and the people over the age of 45 have no particularly high requirements for fashion, fashion, and personalization. This explains why the sales volume of the trend department is particularly low in the first point.
### 7. What is the most popular item in each age group?

The following is the most popular products of every age group. It can be seen that in each age group, the most popular goods is No.1078. It can be seen that No.1078 item is suitable for all ages and is loved by all ages.
### 8. Are older people more inclined to recommend a product or younger people?

The relationship between recommendation and age is obtained by calculating the average age of customers who select to recommended item. As can be seen from the following figure and the table below, the average age of customers who choose not to recommend products is 42.3, and the average age of customers who choose recommended products is 43.3. So there is no such thing as older people prefer to recommend products or young people prefer to recommend products.
### 9. Is the rating correlated to your measure of negativity-positivity? 

We draw the graph and apply OLS to 'Rating' and 'point_comment'. We also get all the correlation.

The correlation between rating and my measure of negative-positive is 0.4. And from the graph we can tell that it is a very positive relationship. The R-squared of the OLS method is 0.16 which is very low, but considering this is to test emotion mark in each text, high R-squared is impossible. Customers who give high rating are more likely to have a higher positive emotion mark. Customers who give low rating are more likely to have a negative emotion mark.
### 10. Which group of reviewers wrote a longer text in their review?

We calculate the length of each comment and apply OLS to length and text's emotion mark. 

From the correlation sheet above we the correlation between point_comment and length_comments is 0.2. From the graph we can also tell that their relationship is positive. The R-squared is very small, so there is not a strong relationship between them. The answer is that very happy or very unhappy customers are more likely to write a longer text, but generally the emotion mark does not affect length of text very much.
### 11. The relationship between Rating and Recommendation

From the above correlation sheet we can get the correlation between rating and recommendation is 0.79 which is a very positive relationship. By using OLS we get: $Recommedation=0.28*Rating-0.33$. The R-squared is 0.629. The relationship is positive.
### 12. The relationship between Age and Rating

By drawing the scatter plot of age and rating, the relationship between age and rating is obtained. From the figure and from the correlation sheet above, the correlation between age and rating is as low as 0.035. 
### 13. Which age group uses more positive words? Which age group uses more negative words?

We get the average number of positive/negative words used in different age groups. As can be seen from the table and chart below, the difference in the number of positive/negative vocabularies used at each age is not very large. 13-20 years old group use the most positive words, using an average of 3.7154 positive words. 31-45 years old group use less positive vocabulary, using an average of 3.379101 positive vocabulary.
### 14. Is it true that unhappy customers use more capital letters? or it is the other way around?

We first get the number of uppercase letters in the comments, then drew the picture of 'the relationship between the number of uppercase letters in the comments and satisfaction'. 

From the figure below, we can get the number of the uppercase letters in most comments is 1 and the number of uppercase letters in the small part of the comment is 0. There is basically no correlation between satisfaction and the number of uppercase letters. So it is not true that unhappy customers use more capital letters.
### 15. What is the average rating in positive, negative or neutral reviews?

We first use our results of measurement for review text to judge which are positive, negative or neutral reviews, creating the new column called simple_measure. Then we calculate the average rating based on the classification of simple_measure.

From the result we can tell that usually positive customers give Rating at 4.34, negative customers give Rating at 2.82 and neutral customers give Rating at 3.31.
### 16. Are there many outliers who wrote a negative text but left a high rating (or vice versa)?

In this question, I set that a high rating is Rating>3, and that a low rating is Rating<3. I set that a positive text is point_comment>0 and that a negative text is point_comment<0.

Based on this assumption, the number of positive outliers with low rating is 1192 and the number of negative outliers with high rating is 373. Therefore, there are actually many outliars. However, this is based on this assumption, if we set a more strict assumption such that positive text are whose point_comment>2, then the number is 564.
### 17. Which product attracted the most positive or negative reviews?

We first use both 'Product ID' and 'simple_measure' to do the classfication, and then count each kind of product's positive and negative customers individually. Because each product has many customers among who some give positive reviews while some give negative reviews.

The result: there some products such as whose ID are: 1078, 862, 1094... sold a lot and that there are many positve reviews and negative reviews. Because these products sell a lot that we can suggest the sellers focus on these products and do some improvement so that there will be more positive reviews and less negative reviews for this product. We can also tell that some products such as whose ID are: 872, 867... these products are good because they have much more positive reviews than negative reviews. For products such as 1072, the sellers need to do some adjustments because it has more negative reviews.
