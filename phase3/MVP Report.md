# 
# Executive Summary
Problem: With the rise of social media, many social media platforms have taken on an increasing role in macroeconomics. Influential political and social media figures routinely post on the internet and whether or not those posts correlate with subsequent market movement is a question that retail investors have no practical way to answer. There are too many accounts to follow, too many posts to read, and no systematic way to distinguish a post that is genuinely market-relevant from one that is just noise. Even when a retail investor does encounter a relevant post, evaluating whether that person's past statements have actually predicted market behavior requires historical data and quantitative analysis that most individuals do not have the tools or training to perform 

Solution: This project delivers an automated pipeline which scrapes data from influential accounts across major platforms such as X and Threads. The system then runs multi-layer language processing on every post to extract sentiment features, aligns those features with real market data, and applies a linear regression to determine whether a given person's market-related statements correlate with actual market movement. The final output presents this correlation in plain English, giving a retail investor a clear, data-backed answer to the whether a post is worth paying attention to. 

#
# User & Use Case
User: The target user is someone who manages their own portfolio, follows financial news and political commentary casually across social media, and is aware that the statements of prominent media figures can potentially guess or influence market sentiment. 

Usage case: A user wants to evaluate whether a political commentator's statements about the S&P 500 are worth acting on. They run SLICE against that person's X account, specifying a start date to define a historical window. The scraper collects all posts since that date and saves them as a dated text file. It then analyzes the text file, in a separate program, as chunks and converts those chunks into data points where it measures various attributes using AI language processing. Then it retrieves the S&P 500 direction for each corresponding date from a market data file, and computes the relationship between what the person said and what the market did. 

#
# System Design

#
# Data

#
# Models
The system used several pre-trained, specialized models and workflow strategies to provide comprehensive analysis of social media post. Some of the pre-trained models used include Vader, TextBlob, and distilBert. These are to analyze social media, extract noun phrases and binary sentiment classification. The supervised statistical models used include least squares regression line and mathematical modeling; these include finding the relationship between the sentiment score and the S&P 500 market directions and to determine if a person is reliable “predictor” for said market movement. The workflow and its strategies were designed through a multi-dimensional approach; first using Lexical Density to count specific “emotional” words via Vader, Contextual Sentiment to understand the polarity/confidence of the statement by DistilBert, and Keyword Filtering to filter for “S&P500” relevance before the data is inputted into the matrix (via TextBlob). There was very few fine-tuning performed as the model uses an already fined-tuned of SST-2. For prompting, the system did not use Generative AI prompting, but rather programmatic parsing. 

#
# Evaluation
In evaluating this system, for its quantitative metrics it evaluates the influencer’s signal effectiveness using standard statistical measures derived from text sentiment and market direction correlation. This is accomplished through find the coefficient of determination measuring the how much variance in the S&P500 direction can be explained by the influencer. If a strong relationship, given a score >0.7, if weak, <0.3. Then it finds the correlation coefficient to find the strength and direction of the linear relationship; positive slope equals the person being a “leading indicator” and vise versa for a negative slope. Thirdly, the system uses lexical density to filter out posts that lack actionable importance. Possible errors analyzed includes any sarcasm and slang which DistilBert and Vader can misinterpret and contextual blindness in which a post can have a neutral score while containing high-impact views. 

