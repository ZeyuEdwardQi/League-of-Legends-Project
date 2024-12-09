
# Statistical Analysis of Gold Metrics in League of Legends

 This a comprehensive data science project conducted at UCSD. The project includes various parts of analysis, starting from exploratory data analysis to hypothesis testing, creation of baseline models, and concluding with fairness analysis. The primary focus of the project is to investigate the most influential playerin League of Legends in 2018 by evaluating matches and impact on match statistics and outcomes.

 Author: Zeyu Qi

 ## Introduction
 ### General Introduction

 League of Legends is one of the most popular video games developed by riot games. With a thriving competitive scene and millions of active players, it has established itself as one of the premier esports in the gaming industry. Professional matches in LoL are meticulously analyzed and followed by fans worldwide, making them a valuable resource for performance analysis and predictive modeling. The data set we will be working with is a professional data set that’s developed by Oracle’s Elixir. The file records match data from professional LOL esports gaming matches in 2018.

The dataset includes key gameplay statistics from a collection of LOL pro matches. It encompasses various aspects, including individual player performance metrics, team strategies, in-game statistics, and the overall flow and dynamics of the matches.

In League of Legends (LoL), the concept of "gold" plays a pivotal role, acting as a crucial determinant in the trajectory of a match. Gold is an in-game resource that players earn through various actions, such as:
defeating Minions, killing monsters, taking down turrets, champion kills and assists, and 
passive income. Beyond its direct influence on the scoreboard, gold profoundly impacts the flow of gameplay, shaping the strategies, dynamics, and potential outcomes as the match progresses.

The central question of the project is: **to what extent does gold has to other gaming statistics in the data set**? The aim is to utilize data analysis techniques to evaluate the impact of gold on various gaming metrics, including individual player performance, team strategies, in-game dynamics, and overall match outcomes. Building on these insights, I seek to develop a predictive model capable of game results based on the analyzed statistics. This model holds significant potential to enhance strategic decision-making and elevate the overall gameplay experience.


 ### Column Introduction

 The dataset introduces a comprehensive dataframe with columns of gameplay metrics and match outcomes from professional League of Legends esports matches. There are 80904 rows and 161 columns in this dataset. However, only a number of columns are important to the project. Here’s a brief introduction to each of these columns:

 	- ==league==: This column identifies the professional esports league in which the match was played (e.g., LCS, LEC, LCK). It provides context about the level of competition and regional influences on gameplay strategies and dynamics.

 	- ==position==: This column specifies the in-game role or lane assigned to a player during the match. Common positions in League of Legends include: top, jungle, mid, bot, and sup. 

 	- ==result==: This column represents the outcome of the match for the corresponding team or player, typically encoded as a binary value: 1 indicates a win and 0 indicates a loss.

 	- ==kills==: This column indicates the number of enemy champions a player or team has successfully eliminated during the match.

 	- ==deaths==: This column represents the number of times a player or champion was eliminated by the enemy team during the match.

 	- ==assists==: This column captures the number of times a player contributed to the elimination of an enemy champion, without landing the final blow.

 	- ==earned gpm==: This column represents the average amount of gold a player or team earns per minute during the match. It is a critical metric for assessing economic efficiency and resource generation.

 	- ==golddiffat10==: This column represents the difference in total gold between a player’s team and the opposing team at the 10-minute mark in the game.

 	- ==golddiffat25==: This column represents the difference in total gold between a player’s team and the opposing team at the 25-minute mark in the game.


## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

For the purpose of data cleaning, I will only keep the important columns and dropping other irrelevant columns: ==league==, ==position==, ==result==, ==kills==, ==deaths==, ==assists==, ==earned gpm==, ==golddiffat10==, and ==golddiffat25==. In the cleaned dataset, there are 17268 rows and  10 columns, representing that there are 17268 observations and 10 features. 

| league | position |   result |   kills |   deaths |   assists |   dpm      | 	earned gpm |   golddiffat10 | golddiffat25 |
|:-------|:---------|---------:|--------:|---------:|----------:|-----------:|------------:|---------------:|:-------------|
| LPL    | top      |        1 |       3 |        1 |         3 |   363.4340 |    274.4151 |            5.0 | 1488.0       |
| LPL    | jng      |        1 |       3 |        0 |         5 |   261.2830 |    275.9245 |          182.0 | 2821.0       |
| LPL    | mid      |        1 |       3 |        1 |         8 |   754.1509 |    326.2642 |          255.0 | 1219.0       |
| LPL    | bot      |        1 |       3 |        1 |         7 |   891.4340 |    396.5660 |          554.0 | 3214.0       |
| LPL    | suo      |        1 |       0 |        1 |         9 |   152.2642 |    182.2264 |          -41.0 | 1555.0       |












