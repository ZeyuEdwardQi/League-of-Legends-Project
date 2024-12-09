
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

 	- `league`: This column identifies the professional esports league in which the match was played (e.g., LCS, LEC, LCK). It provides context about the level of competition and regional influences on gameplay strategies and dynamics.

 	- `position`: This column specifies the in-game role or lane assigned to a player during the match. Common positions in League of Legends include: top, jungle, mid, bot, and sup. 

 	- `result`: This column represents the outcome of the match for the corresponding team or player, typically encoded as a binary value: 1 indicates a win and 0 indicates a loss.

 	- `kills`: This column indicates the number of enemy champions a player or team has successfully eliminated during the match.

 	- `deaths`: This column represents the number of times a player or champion was eliminated by the enemy team during the match.

 	- `assists`: This column captures the number of times a player contributed to the elimination of an enemy champion, without landing the final blow.

 	- `earned gpm`: This column represents the average amount of gold a player or team earns per minute during the match. It is a critical metric for assessing economic efficiency and resource generation.

 	- `golddiffat10`: This column represents the difference in total gold between a player’s team and the opposing team at the 10-minute mark in the game.

 	- `golddiffat25`: This column represents the difference in total gold between a player’s team and the opposing team at the 25-minute mark in the game.


## Data Cleaning and Exploratory Data Analysis

### Data Cleaning

For the purpose of data cleaning, I will only keep the important columns and dropping other irrelevant columns: `league`, `position`, `result`, `kills`, `deaths`, `assists`, `earned gpm`, `golddiffat10`, and `golddiffat25`. In the cleaned dataset, there are 62004 rows and 10 columns, representing that there are 62004 observations and 10 features. 

Below is the head of our filtered dataframe.

| league | position |   result |   kills |   deaths |   assists |   dpm      | 	earned gpm |   golddiffat10 | golddiffat25 |
|:-------|:---------|---------:|--------:|---------:|----------:|-----------:|------------:|---------------:|:-------------|
| LPL    | top      |        1 |       3 |        1 |         3 |   363.4340 |    274.4151 |            5.0 | 1488.0       |
| LPL    | jng      |        1 |       3 |        0 |         5 |   261.2830 |    275.9245 |          182.0 | 2821.0       |
| LPL    | mid      |        1 |       3 |        1 |         8 |   754.1509 |    326.2642 |          255.0 | 1219.0       |
| LPL    | bot      |        1 |       3 |        1 |         7 |   891.4340 |    396.5660 |          554.0 | 3214.0       |
| LPL    | suo      |        1 |       0 |        1 |         9 |   152.2642 |    182.2264 |          -41.0 | 1555.0       |

Note: In the dataset, there are some missing values, escpially in `golddiffat25`. For the purpose of data cleaning, rows of dataset with NaN values in `golddiffat25` are dropped.


### Univariate Analysis

A univariate analysis is performed on the earned gpm statistics in the dataset. 

<iframe
  src="assets/EarnedgpmDistribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This histogram represents the distribution of the "earned gpm" (gold per minute) across all roles in the dataset. The bell-shaped distribution indicates that most players earn between 300 and 500 gold per minute. However, roles such as Bot (ADC) and Mid, which are traditionally carry roles, may skew the distribution toward higher gold values, as these roles often prioritize resource allocation. Conversely, Top, Jungle, and especially Support roles tend to earn less gold, leading to lower frequencies in the higher gold ranges. This trend highlights the resource distribution dynamics within a typical League of Legends game.


Another univariate analysis is performed on the kills statistics in the dataset. 

<iframe
  src="assets/KillsDistribution.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This histogram displays the distribution of kills across players or teams in the dataset. The majority of players/teams have between 0 and 10 kills, indicating that most gameplay scenarios feature moderate kill counts. This aligns with the typical dynamics in League of Legends, where kills are spread across all players, and a few players dominate the kill count. The right-skewed nature of the histogram shows that high kill counts (20 or more) are rare and represent exceptional performances.

### Bivariate Analysis

A Bivariate analysis is performed on the kills and gold earned per minute statistics in the dataset. 

<iframe
  src="assets/scatter_kills_gpm.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

This scatter plot illustrates the relationship between the number of kills and earned gold per minute (GPM) in the dataset. There is a positive correlation, as higher kill counts generally correspond to higher GPM. However, the wide range of GPM at lower kill counts suggests that gold can also come from other sources like farming or objectives, while diminishing returns at higher kill counts indicate that kills alone are not the sole driver of economic efficiency.

### Interesting Aggregates

|      |   ('kills', 0) |   ('kills', 1) |   ('earned gpm', 0) |   ('earned gpm', 1) |   ('golddiffat25', 0) |   ('golddiffat25', 1) |
|:-----|---------------:|---------------:|--------------------:|--------------------:|----------------------:|----------------------:|
| top  |       1.545    |        2.97136 |            221.011  |             286.53  |              -825.19  |               825.19  |
| jng  |       1.48578  |        2.71763 |            162.365  |             227.653 |              -854.782 |               854.782 |
| mid  |       2.12657  |        4.28237 |            234.58   |             305.527 |              -925.004 |               925.004 |
| bot  |       2.20244  |        4.88214 |            254.497  |             334.405 |             -1035.33  |              1035.33  |
| sup  |       0.594155 |        1.01568 |             96.6212 |             147.802 |              -602.684 |               602.684 |
| team |       7.95394  |       15.8692  |            968.046  |            1300.61  |             -4242.99  |              4242.99  |


This table highlights the role-specific contributions to match outcomes in League of Legends. Winning teams consistently exhibit higher kills, earned gold per minute (GPM), and positive gold differences at 25 minutes across all roles, with Bot and Mid lanes being the most impactful in carrying games. Support roles show minimal individual stats but significant improvements in GPM and gold difference in winning games, emphasizing their team-oriented influence. The data underscores the importance of early-game gold leads (golddiffat25) and strong performance from carry roles in determining match success.

## Assessment of Missingness

### NMAR Analysis

In the dataset, it is plausible that the column golddiffat25 could be Not Missing At Random (NMAR). This is because the missingness in this column might depend on the value itself. For example, if a match ends early due to a surrender or decisive victory, there might be no recorded gold difference at 25 minutes, as the match did not reach that time point. In such a case, the missingness directly depends on the outcome of the match and the game duration, making it NMAR.

### Missingness Dependency

In this part, we are going to test if the missingness of `earned gpm` depends on other columns. The two other columns that we used are `position` and `result`. The significance level we choose for both permutation tests is 0.05, and test statistic variance of the proportions of missing values. 

**Null Hypothesis**: The missingness of `earned gpm` is independent of `position`

**Alternative Hypothsis**: The missingness of `earned gpm` is dependent on `position`

After we performed permutation tests, we found that the observed statistic for this permutation test is: 1.7086659695309514e-07, and the p-value is 0.036. The plot below shows the empirical distribution of the permutated test statistic.

<iframe
  src="assets/PositionPermutation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is less than the 0.05 significance level, we reject the null hypothesis. Thus, the missingness of `earned gpm` depends on the `position`.

**Null Hypothesis**: The missingness of `earned gpm` is independent of `result`

**Alternative Hypothsis**: The missingness of `earned gpm` is dependent on `result`

After we performed permutation tests, we found that the observed statistic for this permutation test is: 7.876104809599199e-10, and the p-value is 0.909. The plot below shows the empirical distribution of the permutated test statistic.

<iframe
  src="assets/ResultPermutation.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Since the p-value is greater than the 0.05 significance level, we fail reject the null hypothesis. Thus, the missingness of `earned gpm` does not depend on the `result`.

## Hypothesis Testing

We will test whether the average gold earned per minute (earned gpm) differs between winning teams (result = 1) and losing teams (result = 0).

**Null Hypothesis**: The average gold earned per minute is the same for winning and losing teams.

**Alternative Hypothsis**: The average gold earned per minute differs between winning and losing teams.

**The test statistic**: The absolute difference in mean gold earned per minute between winning and losing teams, with significance level of 0.05

Here is a histogram containing the distribution of our test statistics during the hypothesis test:

<iframe
  src="assets/GoldHypothesis.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>

Based on the hypothesis test performed, with a p-value of 0.0, we reject the null hypothesis. There is sufficient evidence that the average gold earned per minute differs between winning and losing teams. It is possible that teams earning more gold per minute tend to win games, reflecting the importance of economic advantage in League of Legends gameplay.

## Framing a Prediction Problem

In the previous sections, we realized how influencial is gold to the outcome of Legue of Legends as it directly impacts a team's ability to purchase items, strengthen their champions, and secure objectives. From this section, we will explore more about how significant gold-related metrics are to game outcomes. In other words: **Can in-game performance metrics, such as kills, gold earned per minute (GPM), and gold differences at various stages, predict whether a team will win or lose a match?**

We will address the question by using binary classification algorithms. The Response variable will be the outcome of the game as they are the most important factor in competitive gameplay analysis, and they provide a clear and measurable target for assessing the impact of player and team performance metrics. We will be evaluating two metrics: F1-Score and ROC-AUC Score. F1-Score balances precision and recall, making it well-suited for situations where class distributions may be imbalanced.
For esports data, it is critical to minimize both false positives and false negatives to avoid biased conclusions about a team's performance. While accuracy is a simpler metric, it does not account for class imbalance and can give misleading results if one class is more prevalent. ROC-AUC Score Measures the model's ability to distinguish between classes across different thresholds and provides insight into the overall effectiveness of the classifier beyond a single decision threshold.

## Baseline Model

The baseline model is a Logistic Regression classifier used to predict whether a team wins or loses a match (binary classification). The model uses both quantitative and nominal features to evaluate in-game performance and team dynamics. Features in the Baseline Model inlcude one quantitative features `earned gpm` and one nominal feature `position`. `earned gpm` is standardized using a StandardScaler to normalize the scale and improve model performance. `position` is encoded using OneHotEncoder to convert the categorical position variable into binary columns for each role. A Logistic Regression classifier was chosen as the baseline because it is simple and provides a benchmark for more complex models.

After fitting the model,the precision is **0.84** for winning classes (win = 1) and , **0.84** for losing classes (loss = 0). This indicates that when the model predicts a win or loss, 84% of those predictions about winning is correct and 83% of those predictions about losing is correct. The recall for class 0 (loss) is **0.84**, meaning 84% of actual losses are correctly identified by the model. The recall for class 1 (win) is **0.82**, meaning 81% of actual wins are correctly identified by the model. Both classes have F1-scores around **0.83**, showing a good balance between precision and recall. The overall accuracy is **0.83**, meaning the model correctly predicts match outcomes 83% of the time. The ROC-AUC score is **0.91**, indicating that the model performs well at distinguishing between the two classes across various probability thresholds. The Baseline Model demonstrates balanced performance: The precision, recall, and F1-scores are consistent for both classes, showing that the model does not heavily favor one outcome over the other. However, there are limitations to the Baseline Model. While the performance is reasonable, a logistic regression model might not fully capture complex interactions between features like `earned gpm`, `golddiffat25`, and `kills` because it assumes linearity.

The baseline model provides a good starting point, with metrics indicating consistent and balanced performance. However, the addition of engineered features and more sophisticated models could improve performance further.

## Final Model

There are several features added into the Final Model. 

1. kills_x_gpm (Kills × Earned GPM):

This interaction term captures the synergy between a player's ability to secure kills and their efficiency in acquiring resources (gold). A player with a high kill count and high GPM likely contributes more significantly to their team's success, making this feature a valuable predictor for match outcomes. In professional League of Legends games, kills often lead to additional resources, creating a snowball effect. By combining these two metrics, the model can better understand the combined impact of aggression and resource management.

2. kills_x_golddiff (Kills × Gold Difference at 25 Minutes):

This feature measures how a player's kills contribute to their team's overall gold advantage at a crucial stage of the game (25 minutes). Teams with higher gold differences often have a stronger chance of winning, and this feature quantifies the importance of individual contributions. Gold difference at 25 minutes is a well-known predictor of match outcomes in professional League of Legends games. Combining it with kills highlights players who directly influence team success.

3. Polynomial Terms (Second-Order Interactions):

Polynomial features (e.g., squared terms) allow the model to capture non-linear relationships in the data. For example, diminishing returns on gold or kills might exist, where extreme values behave differently than moderate ones. Non-linear relationships between metrics such as GPM, kills, and gold difference often arise in esports data. Squared terms help capture these patterns, improving the model's predictive power.


The Final Model uses Random Forest Classifier because it is robust to non-linear relationships, can handle feature interactions implicitly, and provides feature importance scores for better interpretability. It also performs well on tabular data with mixed feature types. Hyperparameters are selected by GridSearchCV: it performed an exhaustive search over a grid of hyperparameters with 3-fold cross-validation on the training data.




