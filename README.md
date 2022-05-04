# 2013-14 NBA Dataset DSCI2 Capstone Project

## Background

* The NBA is composed of 450 players each season
* Each season there are close to 200,000 shots taken across the league
* Around 45% of shots taken are made in a typical season coming out to around 90,000 makes out of the 200,000 attempts
* There are many factors that go into the points scored by each player, whether it be shot attempts, made shots, minutes, or plenty of other factors. But which is the best predictor?

## Data

I am going to use the player statistics from the 2014-15 NBA season. This season was before the true breakout of Steph Curry, which led to a massive increase of 3-point attempts across the league. This dataset will be skewed less by shot distance than the current 3-point heavy era we are currently seeing in the NBA. Shots were more evenly distributed between 3s, mid-range, and inside shots. I attached the Kaggle link below
https://www.kaggle.com/drgilermo/nba-players-stats-20142015?select=players_stats.csv 

## Objective

I plan to create a model after seeing which variables are the most closely correlated with points scored per game. I plan on exploring the dataset and finding out what variables most clearly increase or decrease a player’s scoring average, then create a predictive model to predict points scored given the other variable. My original plan was to create a model to predict Field Goal Percentage, but after looking at the variables correlations with each other, i shifted my focus towards points per game, an attribute I added.

## Methodology

1. The first step was getting the data. I searched through Kaggle to find NBA statistic datasets, and settled on the 2013-14 season dataset because it presented a moderately sized dataset. I then downloaded the dataset and loaded it in to a jupyter notebook where I looked at the variables and the head of the dataset
2. The next step was the wrangling/cleaning of the data. Overall, the dataset was much less messy than I expected it to be. I checked my dataset for missing values, which did exist, but they were all exclusively in variables that I wasn’t working with or needed(College, Experience, Height, BMI, etc.). I did add a few variables because they were all totals and I thought categories like points, assists, and rebounds needed per game attributes
3. After this I started visualizing the dataset. This is a good starting place for exploring your data, looking at how different variables interact with each other can give me a good idea of where to start. I used visualizations to find correlations between my variables and find two that I wanted to work with. I was down to two choices of variables to try to predicts points scored, Shots Made and Minutes. In the end I chose minutes, because I believe it to be the most interesting predictor for points scored, even though it’s not as strongly correlated. After starting modelling with these two variables I would eventually switch from total points scored and total minutes played to points per game and minutes per game because It was easier to understand.
4. The fourth step was creating training and testing sets for the data. This step had to take place before I did any testing of the dataset. For my training and testing sets I only brought in two variables from my whole dataset, x = Minutes per game and y = Points per game. I will only be using these two variables and Points is the y value because it is what I will be attempting to predict. The training set is 80% of the data and testing 20%
5. The next and most important step was where I began testing different models on my data. The first model I tried was a linear regression model which was able to get an MAE of about 2, meaning that my model was predicting points per game within two points given minutes per game, which was good but I wanted to try more. The second model I tried was a Random Forest Regressor, I expected this one to perform better than the linear regressor because it's an ensemble method, howver the RF came back with an MAE of about 5.5, which is pretty significantly worse. I had planned on trying a Neural Network next but after some research on regressors I tried an XGB Regressor and that worked beautifully coming back with an MAE of around 0.5. I decided to move forward with this model because of it's performance.


```python

```

# Results

### Prepared Data

Number of players in data: 490

Number of Variables: 42

Added Variables: PPG, MPG, APG, RPG

## Correlation between my variables

Correlation = 0.893

![per_game_correlation.png](attachment:per_game_correlation.png)

## Best Model

The best model performed on the training set was the XGBoost Regressor coming back with an MAE of only 0.43, meaning that the model was prediciting points per game within half a point given a player's minutes per game (which was very good). I then went on to tune the hyperparameteres of the model using GridSearchCV and find the best possible model using that. However, when I implemented this model on the test set it came back with an MAE of 1.6, which was still better than my second best model on the training set, but clearly worse then XGB's performance on the training set. 

## Final Thoughts

I believe that is possible to accurately predict a player's points per game given their minutes per game, and I think the model'sperformance on the training set proved that. While it could have been something as simple as overfitting the model, I believe that the reason that my model performed worse on the test set was that I didn't have enough data. I think the size of the test set being 98 players was too small to be hyper accurate and if I had chosen a larger dataset, spanning over multiple season, the model would have markedly improved.

## References

* https://www.kaggle.com/drgilermo/nba-players-stats-20142015?select=players_stats.csv
* https://fivethirtyeight.com/features/how-mapping-shots-in-the-nba-changed-it-forever/ 
* https://www.basketball-reference.com/leagues/NBA_stats_per_game.html 
* https://www.kaggle.com/code/jayatou/xgbregressor-with-gridsearchcv/script
* Géron, A., & Demarest, R. (2019). Hands-on machine learning with scikit-learn
	and tensorflow: Concepts, tools, and techniques to build Intelligent 	Systems. O'Reilly. 
