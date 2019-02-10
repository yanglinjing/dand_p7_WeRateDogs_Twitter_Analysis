# Data Wrangling and Analysing Report - WeRateDogs Twitter
BY YANG, Linjing
2019/02/10
# Introduction
Real-world data rarely comes clean. Using Python and its libraries, I gathered data from a variety of sources and in 3 different formats, assessed its quality and tidiness, and then cleaned it, which is called data wrangling.
## Goal
Practice data wrangling using WeRateDogs Twitter data in order to create interesting and trustworthy analyses an visualizations.
## Tools
I documented my wrangling efforts in a Jupyter Notebook, plus showcased them through analyses and visualizations using Python and its libraries (pandas, numpy, requests, json, tweepy, etc.).
## Dataset
My dataset consists of data from 3 different sources.
### 1. Twitter Archive
The first one is the tweet archive of Twitter user @dog_rates, also known as WeRateDogs, which is a Twitter account that rates people's dogs with a humorous comment about the dog.
WeRateDogs has over 4 million followers and has received international media coverage.
Its ratings almost always have a denominator of 10, but the numerators are always greater than 10 (e.g. 11/10, 12/10, 13/10, etc). Why? Because "they're good dogs Brent."
### 2. Additional Information via the Twitter API
The second one is retweet count and favorite count of each tweet gathered from Twitter's API by Tweetpy Library in a Json format.
### 3. Image Prediction File
The third is the prediction of dog images and breeds downloaded programmatically by Requests Library from the neural network.
## What I did
Examine the 3 datasets (6,787 total entries)
Use Python to wrangle and analyze them
Create a custom visualization to communicate observations

# Data Wrangling
## Data Gathering
Data was gathered from 3 different sources.
### 1. Twitter Archive
The Twitter archive #WeRateDogs, a csv file that contains various kinds of information, such as dog ratings, stages, tweet ids, posted date, etc.
### 2. Additional Information via the Twitter API
The retweet and favorite count of each tweet gathered from Twitter's API by Tweetpy Library in a Json format.
### 3. Image Prediction File
The prediction of dog images and breeds downloaded programmatically by Requests Library from the neural network.

## Data Accessing
Data was accessed based on both of quality and tidiness issues.
### Quality Issues
#### Dataset 1
Completeness:
- in_reply_to_status_id: 78 out of 2356 is non-null
- in_reply_to_user_id: 78 out of 2356 is non-null
- retweeted_status_id: 181 out of 2356 is non-null
- retweeted_status_user_id: 181 out of 2356 is non-null
- retweeted_status_timestamp: 181 out of 2356 is non-null
- name: string 'None' should be replaced by Null

Validity:
- rating_denominator contains invalid values (e.g. denominator = 0)
- expanded_url just includes incomplete url, which contains "https://twitter.com/dog_rates/status/" plus part of tweet_id

Accuracy:
- rating_numberator contains extremely large values (e.g. 1776 when denominator = 10)

Consistency:
- source: the long name with HTML tag could be shorten.

Data Types:
- tweet_id: integer -> object
- timestamp: object -> datetime
- in_reply_to_status_id: float -> object
- in_reply_to_user_id: float -> object
- retweeted_status_id: float -> object
- retweeted_status_user_id: float -> object
#### Dataset 2
Completeness:
- retweet & favourite count: "Nan" should be replaced by Null.
- retweet & favourite count: 16 missing values

Data Type:
- retweet & favourite count: object -> integer
#### Dataset 3
Data Type:
- tweet_id: integer -> object

### Tidiness Issues
#### Dataset 1
- The dog stages - doggo / floofer / pupper / puppo - could be combined into 1 column as categorical data.
#### Dataset 3
- The column names could be more clear.

## Data Cleaning
- The three datasets were combined into one with more clear column names.
- The columns that could not contribute to analysis were dropped.
- The row that contains invalid values was deleted.
- All missing values were presented as Null.
- The data types of all columns were corrected.
- The dog stages were combined into one column as categorical data.
- The HTML tags in the ‘source’ column were deleted.


# Data Analysing
## 1. Dog Ratings
Since there are various rating denominators (although most of them are 10), the rating of dogs is calculated by dividing the numerator by the denominator.
From the sorted raw data in the Data Cleaning section and the calculation above, it can be seen that there are 10 rows have their ratings larger than 1.7, including most outliers.
After cutting off these 10 rows, it shows that the ratings of dogs are left-skewed distributed, with the mean of 1.07 and the median of 1.10. Besides, 75% of the dogs are rated equal to or more than 100%. Thus, it can be found that most dogs are considered to be better than perfect.

![Dog Ratings](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/dog_ratings.png)

## 2. Source of Tweet
From the pie chart, it presents that the dominant source is from iPhone, which is 94.3%. Only a few people use Vine (3.9%), Website (1.4%) and TweetDect (0.5%) to browse WeRateDogs Tweet.

![Source of Tweet](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/sources.png)

## 3. Relationship between Retweet and Favourite
The count of retweet and favourite are highly positively correlated ( r = 0.797). Thus, we could say that the more people like a tweet, the more they retweet it.

![Retweet and Favourite](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/retweet_favourite.png)

## 4. Breeds
The top 15 predicted dogs are shown in the plot.

![Breeds](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/dog_predictions.png)

It can be seen that golden retriever is the No.1 predicted dog, which has been predicted 150 times with high confidence. The confidence of predicting it is left skewed, with the median of 0.78 and mean of 0.72.
The second most predicted dog is Labrador_retriever (100 times), the high confidence of which is also left skewed with the median of 0.71 and mean of 0.67.

![prediction_confidence](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/prediction_confidence.png)

## 5. Dog Stages
Only 366 out of 2355 dogs have their stages presented in the dataset. The most common stage is pupper (245), followed by doggo (83) among the dogs whose stage has been presented.

![dog_stages](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/dog_stages.png)

The explanation of dog stages is shown as follows.

![dogtionary](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/dogtionary.png)


## 6. Post Tweet Day
From Monday to Sunday, the number of posted tweet decreases. WeRateDogs followers may expect to see more new tweets on Monday.

![day_of_week](https://github.com/yanglinjing/dand_p7_data_wragling/blob/master/readme_pic/day_of_week.png)



# Conclusion
- 75% of the dogs are rated equal to or more than 100%. Thus, most dogs are considered to be better than perfect.
- The dominant source is from iPhone (94.3%).
- The count of retweet and favourite are highly positively correlated - the more people like a tweet, the more they retweet it.
- The top 1 predicted dog is golden retriever, followed by labrador retriever.
- The most common stage is pupper, followed by doggo.
- From Monday to Sunday, the number of posted tweet decreases.
