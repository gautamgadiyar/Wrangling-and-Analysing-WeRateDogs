# Wrangling and Analysing WeRateDogs 
This is a project aimed at performing various data wrangling actions that get the right data from the data source. 
I had to <b>gather, assess the data and clean</b> it so that the analysis could come out clean with no discrepency. 
There were many tidiness and quality issues with the data gathered. This was cleaned up.
The twitter handle, <b>'WeRateDogs'</b> is the main source of data that was retrieved.

<img src='https://d17h27t6h515a5.cloudfront.net/topher/2017/October/59dd378f_dog-rates-social/dog-rates-social.jpg'/>

## Data Gathering:

1. twitter_archive_enchanced.csv - The data was obtained using the CSV file provided containing all the tweets data till 1st August 2017 in the file. This was the base data for the analysis.
2. image_predictions.csv – This file contaned all the predictions using neural network for the breed of the dog. This is provided the the instructor.
3. additional_tweet_data.csv – This file was created using the Twitter API after getting the favorite count and retweet count for all the tweets in the base archive file. Twitter authencation has been used to get the data.

## Assessing data:

The data was investigated for any issues, Quality or Tidiness, and the issues were noted down to be resolved in the cleaning process. 
    • Quality issues – This is mainly missing, duplicate or incorrect data that is present.
    • Tidiness – The structural issues in the dataset like incorrect column names, multiple related tables.
       
The following were the various issues identified.


Quality issues:
1. The rating_denominator should have a standard throughout to be 10. There are various other values, which is erroneous.
2. The rating_numerator has many erroneous values, like in 100s.
3. the datatype of timestamp should be datetime and not string.
4. The are wrong dog names mentioned like 'a', 'an'.
5. The rows that contain non-empty 'retweeted_status_id'  need to be removed as these are retweets.
6. Columns like 'in_reply_to_status_id', 'in_reply_to_user_id', 'retweeted_status_id', 'in_reply_to_user_id' have lot of missing values. The columns are not useful in the analysis and can be dropped.
7. The 'expanded_url' column has a few missing values. This suggests that there are no images in the tweets. These tweets cannot be considered for analysis.
8. There are urls in the text which is not readable for user. This needs to be reduced to text only.
9. The columns names like p1,p2 are not clear in Image predictions.

Tidiness Issues:
1. The favorite_count and retweet_count need to belong to the same dataframe.
2. Columns 'doggo', 'floofer', 'pupper', 'puppo' in twitter_archive_df should belong to one colomn, maybe dog_stage.

## Data Cleaning:
All the issues that were identifies in the Assess step were repaired in the step following the standard data wrangling steps.

Quality issues resolution:
1. The false denominators were changed to 10 after refering the tweet text. Incase the tweet had data like 110/90, then the denominator data was replaced by NULL.
2. The numerators were changed after refering the tweet and changed to right data. In case the rating wasn’t relevent, it was deleted from analysis. A regular expression was used to retrieve even the decimal data that was found in the text. Fauty numerator were replaced by NULL. This would not hinder analysis as the count was very less.
3. The timestamp data was converted from string to datetime type.
4. The wrong dog name like ‘a’, ‘an’ were changed to NaN values. This was done by looking for all lowercase words and were replaced by None. The lowercase words were verified not to be names.
5. The non-empty values of retweet_status_id was used to delete the rows that would be retweets. These would just be duplicate data.
6. Columns like 'in_reply_to_status_id', 'in_reply_to_user_id', 'retweeted_status_id', 'in_reply_to_user_id' were dropped as they were not useful for the analysis.
7. The mssing urls indicated no images, so those records were deleted since it is not accurate to analyse them.
8. The urls were replaced by the text in the url like ‘Twitter for Iphone’.
9. The columns names like p1, p2 were changed to readable names.

Tidiness issues resolution:
1. The favorite and retweet count columns were merged into the main dataframe.
2. One new column containing all the dog stages, dog_stage, was created and the data was concatenated into one columns. The 4 columns of different stages were dropped.
