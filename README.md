# probelm statement

### Key Question: 
" Can we leverage our online conversational data to classify MBTI personlity type and use it to enhance online engagement?"

### Introduction
In the ever-evolving digital landscape, online platforms, chat platforms, and social media platforms continuously seek innovative ways to understand and engage their users effectively. While traditional metrics like page views, clicks, and chat interactions provide valuable insights into user behavior, they fail to capture the nuances of individual preferences and motivations. This presents an opportunity to explore the potential of personality data to enhance user engagement and marketing strategies.

### Case Studies Reference
Case Study 1: Predicting Personality Types from Twitter Posts
https://www.researchgate.net/publication/366614754_Personality_Prediction_from_Twitter_Dataset_using_Machine_Learning 

Case Study 2: Personality Type Based on Myers-Briggs Type Indicator with Text Posting Style by using Traditional and Deep Learning
https://arxiv.org/pdf/2201.08717.pdf

### Target Audience
The primary target audience for this research is "Online Platform Developers"
 
### Research Methodology
1) Model Development Using Subreddit Posts: We will develop a predictive model using posts from two subreddit forums, specifically the subreddits dedicated to the INFP and ESTJ Myers-Briggs personality types. This phase focuses on analyzing the language and content of these posts to classify them according to the personality type they most likely represent.
#####          Remark: Please be aware that our focus for the model detailed below is primarily on this first method, "Model Development Using Subreddit Posts."

2) Expanding the Model to Include All 16 Personality Types: The model will be expanded to cover all 16 Myers-Briggs personality types, involving posts from 16 different subreddits.

3) Shifting Focus from Posts to People: The model will shift from classifying posts to classifying the people behind them. Participants will take the official MBTI test for model benchmarking.

4) Testing and Adapting the Model Across Platforms: The model will be tested and adjusted across various online platforms, analyzing user behavior and interactions.

5) Tesing with marketing campaign: the model will be tested with marketing professional on each platform to select target group and personalize content for each personality type, using A/B testing to see the result changes in the marketing metrics 

### Expected Contributions
This research is expected to contribute significantly to the understanding of how personality data can enhance user engagement and marketing strategies across digital platforms.

### Anticipated Challenges
Challenges include data privacy concerns, potential biases in personality assessments, and the complexity of integrating personality data into existing platforms.

### Conclusion
The use of personality data represents a promising area of research with the potential to revolutionize user engagement and marketing strategies in the digital landscape. This research aims to provide a comprehensive understanding of leveraging personality data in the digital environment.

----------------------------------------------------------------------------------------------------------------------------------------------------------------

# Procedure 

IMPORT LIBRARIES

DATA COLLECTION VIA WEB SCRAPING

  - subreddit - infp
 
  - subreddit - estj

DATA PREPROCESSING
 
  - Load Data
 
  - INFP Data Checking & Processing
 
  - ESTJ Data Checking & Processing 
 
  - INFP + ESTJ data --> Final Data Checking & Processing

BASE MODEL BUILDING 
  
  - BASE MODEL 1: Include 5 columns  
 
  - BASE MODEL 2: Exclude 1 column which is post type column which is specific to Reddit Website
  
  - BASE MODEL 3: Exclude Word "infp", "estj", 'infps", 'estjs" which are considered as data leakage form text column

MODEL TUNING 

  - TUNING 1: Vecorization selection (COUNT vs TF-IDF), stemming/lemmanization selection (yes vs no)
 
  - TUNING 2: Top 3 Models Selection
 
  - TUNING 3: Top 3 Models with parameter tuning 
  
      - TUNING 3.1: Logistic regression
    
      - TUNING 3.2: Radom Forest 
   
      - TUNING 3.3: Gradient Boosting 

CONCLUSION AND BUSINSS RECOMMENDATION 

  - Conclusion

  - Business Recommendation 

----------------------------------------------------------------------------------------------------------------------------------------------------------------

# Conclusion 

## Data Preprocessing Summary

 - we load data from infp subreddit 
 - we load data from estj subreddit 
 - we concat both data into 1 data frame 
 - we select 10 columns including 
        - id                  
        - author_fullname      
        - subreddit           
        - link_flair_text      
        - title               
        - selftext            
        - num_comments         
        - selftext_length      
        - title_length        
        - title_emoji_count 
 - we combine title and selftext column into 1 column called text column 
 - we remove all text that are url   

## Base Model Building Summary
 - in base model 1, we include select 5 columns including 'link_flair_text','text','num_comments', 'selftext_length', 'title_length', 'title_emoji_count'
       
        - link_flair_text is categorical data which we get dummify 
        - text is text data which tokenize 
        - other columns are numerical data which we do standard scaling 

 - as a result, we get very high accuracry score train = 1.0 vs test = 0.98 
 - in base model 2, we exclude 'link_flair_text' column which is specific to reddit website 
 - as a result, we get lower accuracy score train = 1.0 and vs text = 0.88
 - in base model 3, we exclude word 'infp', 'estj', 'infps', 'estjs' which we regard as the data leakage in the text column.
 - as a result, we get even lower accuracy score tain = 1.0 vs text = 0.81
 - as the next step, we will start tunning our model to increase the accuracy score 

## Model Tuning Summary 

- for tunning 1, we do 4 combination of tuning which including vectorisation (count vs TF-IDF) and stemming/lemmanization (yes or no)
 - as a result, we have better test accuracy score, compared to base model 3, from 0.62 to 0.72 (for the best model) 
        
|Vectorization Method|Stemming|Lemmatization|Accuracy| 
|---|---|---|---|
|Count Vectorizer|True|True|0.88|
|Count Vectorizer|False|False|0.87|
|TF-IDF Vectorizer|True|True|0.83|
|TF-IDF Vectorizer|False|False|0.84| 

 - in addition, we find count vectorizer is much better than TF-IDF vectorizer 
 - but there is not much difference there is stemming/lemmanization 
 - for tunning 2, we have total 7 model for selection including Logistic Regression, KNN, Bagged Decision Tree, Random Forest, ADA Boost, G Boost, SVM
 - as a result, we have better 3 models that perform best including logistic regression, random forest, and G Boost 
 - there is no difference between top 3 models without parameter tuning; both has score at 0.88

|Model|Accuracy|
|-----|--------|                   
|Logistic Regression|0.880488|   
|KNN|0.697561|
|Bagged Decision Tree|0.843902|
|Random Forest|0.880488|
|AdaBoost|0.753659|   
|Gradient Boost|0.814634| 
|SVM|0.775610|

 - for tunning 3, we do parameter tunning for each model
 - as result, we found that random forest has best performance, followed very closely by Gboost. 
      
       - logistic regression train at 0.99 vs test at 0.89 --> 0.10 gap
       - random forest train at 1.0 vs test at 0.92 ---> 0.08 gap

## Final Conclusion

 - there is high potential for MBTI classification in online conversation, considering ver high accuracy score of our best model (random forest) at 0.79 but it is still very overfit model because train comapare to test score has the big gap 0.21. 
 - we need to accumulate more post to get more data to improve our score and redut overfitting 

 ## Business Recommendation for the next step

  - currently the result is still not sufficient for business application beucase we still only use only 2 personality type post to do classify. however the result suggest that we can move step 2 which is collect data from 16 personality type post do 16 personality class classification. 