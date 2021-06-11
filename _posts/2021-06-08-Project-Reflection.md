---
layout: post
title: Project Reflection Post
---



## Overall, what did you achieve in your project? 
In the project we created, we combined two parts of stock analysis:

- From the long-run perspective, we used a three-factor model to identify the assets that have been incorrectly priced by the market in the past year, and use these assets as the `basis` of our portfolio
- From the short-run perspective, we estimate the expected return of each of the assets on a particular day using returns in previous **5** days and tweets in previous **2** days.
- Finally, we retrieve the estimated variance and covariance matrix of these stocks and construct a optimized portfolio using the portfolio theory.

We return this optimized portfolio to our user as a guidance for trading on a specific day. Though this is not necessarily optimal and hasn't gone through any retrospective testing, but we got something for the users.

## What are two aspects of your project that you are especially proud of? 

- To build our model, we did a large amount of research as well as trial and error to find a **theoretically well supported** model for our long-run analysis. The nature of the stock market in the past year (extreme liquidity and volatility) makes this task difficult. Any direct approximation of stock returns tend to overfit the period from 2020.3 to 2020.4, or become heavily influenced by this period. (And indeed, empirically this is difficult to anticipate if we put ourselves right at the time after the market crashed. No one would expect the Fed to provide so much liquidity and no one would expect Tesla to skyrocket like that.) So we decided to take a rather systemetic approach to the problem that `is built on its own before observing any stock data`. Therefore, our final version is based on the paper by Fama and French in 1993. (https://doi.org/10.1016/0304-405X(93)90023-5) In this paper, they developed a three-factor model from the theoretical perspective and found it could explain the majority of the stock variation in the U.S. market and could provide a systemetic approach to identify the stocks with potentially higher returns in the near future.
- Though we lack the computation power and fast access to data, we still built our project in a **highly modulized** way- that is we encode every critical parts of our project in functions that can be adapted easily for future improvement. For example, the long-term analysis part, though we are now using data from `2020.5` to `2021.4`, it can be easily adapted for future uses if we rewrite the data-accessing part of the main function by applying some quant trading module provided by any trading platform.


## What are two things you would suggest doing to further improve your project? (You are not responsible for doing those things.)
- **More Data!** We have tried our best to access as much market data as we could, including borrowing an access to a professional financial database developed by a Chinese service provider from a friend, but the nature of algorithm trading requires more. For example, we only looked at **PB (Price-to-Book Ratio)** and **MK(Market Capitalization)** as two factors in the market in addition to the **Market Return** in the three-factor model because ths had been the traditional approach. However, other factors might perform better in estimating the returns on the stocks, but most of them are much more complicated than a static number like **PB** and **MK**. For example, a momentum factor would measure both the *Daily Trading Volumn* and *Price changes from previous high/low*, and the *Daily Trading Volumn* is something only Bloomberg or a quant trading platform can provide. We simply couldn't get those data if we use only Yahoo Finance or that database we have been using.
- Better prediction model for daily returns! If we are provided more data for the stocks, not only can we improved the long-run analysis but the short run as well. We would be able to feed our model with more data, like *Trading Volumn* from previoud days or even previous *minutes*, the *Call/Put Ratio* of the stock's options during the previous week or even during the past *hour*, implicity volatilities on these options right at this moment, and etc. Adding these into the model will perhaps, if computation power allows, make the prediction model actually `real-time` and more `short-term`.

## How does what you achieved compare to what you set out to do in your proposal? (if you didn't complete everything in your proposal, that's fine!)

### Successful parts:
- We are able to select a theoretically-well-based group of stocks as the basis of portfolio
- We are able to predict the returns on these stocks using market sentiments
- We are able to consturct a final portfolio and return that to the user

### Unseccesful/Partial Success parts:
- Though we include the tweets in our return prediction model and we discussed how tweets are going to affect the volatility and returns in the following tradedays, it should be noted that this is going to function poorly when the market is dealing with extreme events like a complete market failure in 2020.3, or when the election results came out. These `market sentiment factors` we included in the model are sentiments during the time when the market is not **too sentimental**. This is quite different from what we expected in the project proposal, as at that time we were thinking tweets and news could well predict the volatility of the market. We were being naive about this and in reflection, this actually makes sense. If we could anticipate the influence of the pandemic or the riots after the election, none of these would be problems any more. The fact that they did become disasters means that none could predict its impact perfectly.
- We are not able to test our portfolio in retrospective testing because of the lack of computational power as estimating our model for **1** day would take around **10 to 15** minutes to complete.


## What are three things you learned from the experience of completing your project? Data analysis techniques? Python packages? Git + GitHub? Etc? 
- Data Processing. This first includes data-cleaning. Notice the raw data we retrieve using the database access we borrowed was messy in its format and cleaning this dataframe required us to utilize almost all data processing techniques we have learned, including stacking, unstacking, transformation and indexing. And data processing in our project also includes many data manipulations, especially when building the three-factor model for the long-run analysis. This part of the project led us become familiar with function applications and pivoting within the dataframe.
- Python Packages and Online APIs. We got familiar with a lot of packages and online APIs. We used `snscrape` to retrieve twitter information, we used the `pushshift` reddit API to retrieve comments on reddits, and finally we used the `tipranks` API to retrieve sentiments from Tipranks.com. `BF` is a good webscraping module that could be easily incorporated into Jupyter Notebook, and we also found `statsmodel` to be really handy.
- Research and justify our decisions. We actually didn't expect this project, which intuitively we thought was just *dealing with some data using machine learning*, would require us to familiarize ourselves with some paper from 1993. And we couldn't possibly think that we need to do tons of trial-and-error to see how diffent online comments, news and tweets would explain the stock movement best. In our previous experiences, we built our models and that was it, but working on this project actually taught us to think deeper into the question and justify our moves before we rush towards merely a result.


## How will your experience completing this project will help you in your future studies or career? Please be as specific as possible. 
- For me personally, I learned how to systemetically think about a problem like this, and how to develop a rough idea into a justified model. 
- Also, I got much more familiar with data processing, web scraping and machine learning techniques in Python.
- These experiences have just helped me stand out in a technology consulting internship interview and I will start working at PwC this summer.
- And I'm thinking about applying machine learning and data analysis skill to my Economics and Political Science theses as well!

