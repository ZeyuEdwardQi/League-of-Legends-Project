<!-- # League of Legends Project
A project for DSC 80 at UCSD


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

print(filtered.head().to_markdown(index=False))
 -->

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>League of Legends Project</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            line-height: 1.6;
            margin: 20px;
            background-color: #f9f9f9;
        }
        h1, h2, h3 {
            color: #333;
        }
        h1 {
            font-size: 2em;
            margin-bottom: 10px;
        }
        h2 {
            font-size: 1.5em;
            margin-top: 20px;
        }
        h3 {
            font-size: 1.2em;
            margin-top: 15px;
        }
        p, ul {
            margin-bottom: 10px;
        }
        ul {
            padding-left: 20px;
        }
        ul li {
            margin-bottom: 5px;
        }
        pre {
            background: #f4f4f4;
            padding: 10px;
            border-radius: 5px;
            overflow-x: auto;
        }
    </style>
</head>
<body>
    <h1>League of Legends Project</h1>
    <p>A project for DSC 80 at UCSD</p>

    <h1>Statistical Analysis of Gold Metrics in League of Legends</h1>
    <p>This a comprehensive data science project conducted at UCSD. The project includes various parts of analysis, starting from exploratory data analysis to hypothesis testing, creation of baseline models, and concluding with fairness analysis. The primary focus of the project is to investigate the most influential player in League of Legends in 2018 by evaluating matches and impact on match statistics and outcomes.</p>
    <p><strong>Author:</strong> Zeyu Qi</p>

    <h2>Introduction</h2>

    <h3>General Introduction</h3>
    <p>League of Legends is one of the most popular video games developed by Riot Games. With a thriving competitive scene and millions of active players, it has established itself as one of the premier esports in the gaming industry. Professional matches in LoL are meticulously analyzed and followed by fans worldwide, making them a valuable resource for performance analysis and predictive modeling. The dataset we will be working with is a professional dataset that’s developed by Oracle’s Elixir. The file records match data from professional LoL esports gaming matches in 2018.</p>
    <p>The dataset includes key gameplay statistics from a collection of LoL pro matches. It encompasses various aspects, including individual player performance metrics, team strategies, in-game statistics, and the overall flow and dynamics of the matches.</p>
    <p>In League of Legends (LoL), the concept of "gold" plays a pivotal role, acting as a crucial determinant in the trajectory of a match. Gold is an in-game resource that players earn through various actions, such as defeating minions, killing monsters, taking down turrets, champion kills and assists, and passive income. Beyond its direct influence on the scoreboard, gold profoundly impacts the flow of gameplay, shaping the strategies, dynamics, and potential outcomes as the match progresses.</p>
    <p>The central question of the project is: <strong>to what extent does gold correlate with other gaming statistics in the dataset?</strong> The aim is to utilize data analysis techniques to evaluate the impact of gold on various gaming metrics, including individual player performance, team strategies, in-game dynamics, and overall match outcomes. Building on these insights, I seek to develop a predictive model capable of predicting game results based on the analyzed statistics. This model holds significant potential to enhance strategic decision-making and elevate the overall gameplay experience.</p>

    <h3>Column Introduction</h3>
    <p>The dataset introduces a comprehensive DataFrame with columns of gameplay metrics and match outcomes from professional League of Legends esports matches. There are 80,904 rows and 161 columns in this dataset. However, only a number of columns are important to the project. Here’s a brief introduction to each of these columns:</p>
    <ul>
        <li><strong>league</strong>: This column identifies the professional esports league in which the match was played (e.g., LCS, LEC, LCK). It provides context about the level of competition and regional influences on gameplay strategies and dynamics.</li>
        <li><strong>position</strong>: This column specifies the in-game role or lane assigned to a player during the match. Common positions in League of Legends include: top, jungle, mid, bot, and sup.</li>
        <li><strong>result</strong>: This column represents the outcome of the match for the corresponding team or player, typically encoded as a binary value: 1 indicates a win and 0 indicates a loss.</li>
        <li><strong>kills</strong>: This column indicates the number of enemy champions a player or team has successfully eliminated during the match.</li>
        <li><strong>deaths</strong>: This column represents the number of times a player or champion was eliminated by the enemy team during the match.</li>
        <li><strong>assists</strong>: This column captures the number of times a player contributed to the elimination of an enemy champion, without landing the final blow.</li>
        <li><strong>earned gpm</strong>: This column represents the average amount of gold a player or team earns per minute during the match. It is a critical metric for assessing economic efficiency and resource generation.</li>
        <li><strong>golddiffat10</strong>: This column represents the difference in total gold between a player’s team and the opposing team at the 10-minute mark in the game.</li>
        <li><strong>golddiffat25</strong>: This column represents the difference in total gold between a player’s team and the opposing team at the 25-minute mark in the game.</li>
    </ul>

    <h2>Data Cleaning and Exploratory Data Analysis</h2>

    <h3>Data Cleaning</h3>
    <p>For the purpose of data cleaning, I will only keep the important columns and drop other irrelevant columns: <strong>league</strong>, <strong>position</strong>, <strong>result</strong>, <strong>kills</strong>, <strong>deaths</strong>, <strong>assists</strong>, <strong>earned gpm</strong>, <strong>golddiffat10</strong>, and <strong>golddiffat25</strong>. In the cleaned dataset, there are 17,268 rows and 10 columns, representing 17,268 observations and 10 features.</p>

    <pre>print(filtered.head().to_markdown(index=False))</pre>
</body>
</html>












