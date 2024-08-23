# Overview
Welcome to my analisis of the international matches from 1872 to 2024 in the football history. This project was created with the desire of searching in the data and obtain different answers and curious things, allowing to discover more about the greatest sport, football.

The dataset sourced from [International football results from 1872 to 2024](https://www.kaggle.com/datasets/martj42/international-football-results-from-1872-to-2017), wich provides a foundation to my analisis, containing accurate information about every match and score detail.

# The Questions
Below are the questions that i wanted to answer in my project:

1. Which are the tournaments with most matches?
2. Which are the teams with the most goals internationally?
3. Which are the classic clashes in international matches?
4. What are the most frequent minutes of goal in International Matches?
5. Which are the top scorers in the international history?
6. Which are the top international scorers in the last season (23/24)?

# Tools I Used

- Python: The basis of the analysis, letting me to explore, filter and find every insight, combined with some libraries, like:
  - Pandas Library: To analyse the data.
  - Matplotlib: To show the data in plots.
- Jupyter Notebooks: To run the Python scripts.
- Visual Studio Code: The IDE for executing the scripts.
- Git and Github: To control and share the Python code.

# The Analysis

## 1. Which are the tournaments with most matches?

To find the tournaments with most matches, i calculated the sum of encounters in every tournament, and later show in a bar plot the top 10.

```python
count_matches = df_results["tournament"].value_counts().sort_values(ascending=False).head(10)

count_matches.plot(kind="bar", figsize=(10, 5), color="skyblue")

plt.title("Top 10 tournaments with most matches")
plt.ylabel("Number of matches")
plt.xlabel("Tournament")
plt.xticks(rotation=45, ha="right")
plt.show()
```

### Results
![Visualization of top 10 tournaments](/visualizations/1_top_tournaments_most_matches.png)

### Insights

- The Friendly encounters are the most concurrents, this is because in the world the friendly matches are much more common than competitive tournaments.
  
- The Fifa World Tournaments are the second with most matches, indicating their global significance and the extensive number of matches played.

- Followed by the regional encounter, like continents tournaments, including Copa America, Eurocup and African Cup.

- Tournaments like CECAFA Cup and CFU Caribbean Cup qualification have significantly fewer matches, likely due to their regional scope and the smaller number of participating teams.


## 2. Which are the teams with the most goals internationally?

To find the total goals of every single team, i added the goals (home score and away score) of every match, obtaining what team has more goals and ordering the top 10.

```python
goals_local = df_results.groupby("home_team")["home_score"].sum()
goals_away = df_results.groupby("home_team")["away_score"].sum()

total_goals = goals_local.add(goals_away, fill_value=0).sort_values(ascending=False).head(10)
total_goals

# Show The Plot

total_goals.plot(kind="bar", figsize=(10, 5), color="skyblue")

plt.title("Top 10 teams with most goals in international matches")
plt.ylabel("Number of goals")
plt.xlabel("")
plt.xticks(rotation=45, ha="right")
plt.gca().set_yticklabels([])

for i in range(len(total_goals)):
    plt.text(i, total_goals.iloc[i], total_goals.iloc[i], ha="center", va="bottom")

plt.show()
```

### Results

![Visualization of the teams with most goals](/visualizations/2_teams_with_most_goals.png)

### Insights

- Brazil is the leader of goals, proving its supremacy of the team with most world championship
- Germany and Argentina follow closely behind Brazil, indicating a high level of competition among these teams.
- European teams dominate the top 10, with 7 out of 10 teams being from Europe.
- Mexico is the only north american country in this top.

## 3. Which are the classic clashes in international matches?

The question was resolved counting every match between the teams, but first, i needed to ordered alphabetically, this because "Argentina vs Uruguay" and "Uruguay vs Argentina" counts to the same rivalry. This query highlights that process, showing the top 10 encounters.

```python
encounters = df_results["home_team"] + " vs " + df_results["away_team"]

sorted_encounters = sorted(encounters.str.split(" vs ").apply(lambda x: tuple(sorted(x))).value_counts().items(), key=lambda x: x[1], reverse=True)

df_encounters = pd.DataFrame(sorted_encounters, columns=["Encounter", "Count"]).head(10)

df_encounters["Encounter"] = df_encounters["Encounter"].str.join(" vs ")
df_encounters
```

## Results

![Visualization of the clashes](/visualizations/3_most_matches_internationally.png)

## Insights

- The most classic rivalry is a south american one, Argentina and Uruguay, two world champions.
- Many European rivalrys make their appareance, Austria And Hungary being the most frequently.
- The African Classic is Kenya and Uganda.
- The frequent matchups between these teams likely reflect historical, political, or geographical factors that have contributed to their rivalry.

## 4. What are the most frequent minutes of goal in International Matches?

Grouping the dataset by the minutes of goals, i concluded this answer, giving me a curious insight.

## Results

![Visualization of the minutes](/visualizations/4_minutes_most_goals.png)

## Insights

- The 90th minute is the most common in goals, being the final of the regular time, this is incredible, because suggest that the teams often push hard in the closing stage of a match.
- The last 15 minutes of the match are the most productive in terms of goals.
- Does not exist a consistent pattern in goals between the 20-75 minutes, indicating that the middle portion of the game has a consistent pace of play.

## 5. Which are the top scorers in the international history?

To know the result, it was enough to count each goal made by the scorer, getting the top 10 with this query

```python
top_scorers = df_scorers["scorer"].value_counts().head(10)

top_scorers.plot(kind="barh", figsize=(10, 5), color="skyblue")

plt.title("Top 10 goal scorers in international matches")
plt.xlabel("Number of goals")
plt.ylabel("")
plt.gca().invert_yaxis()

for i in range(len(top_scorers)):
    plt.text(top_scorers.iloc[i] + 0.5, i, top_scorers.iloc[i], ha="left", va="center")
```

## Results

![Visualization of top scorers in history](/visualizations/5_top_scorers.png)

## Insights

- Cristiano Ronaldo is the leader in this top, this is natural, being the top scorer in the history of football.
- The gap between every scorer is relatively small, indicating a high level of competition.
- European players dominate the top 10, including only one Asian player (Ali Daei).

## 6. Which are the top international scorers in the last season (23/24)?

Filtering the players that scored from the start date of the season (11/8/2023), i obtained the top 10 scorers of the past season.

## Results

![Visualization of the scorers](/visualizations/top_scorers_last_season.png)

## Insights

- Akram Afif and Romelu Lukaku are heading the list with 8 goals.
- The european players dominate the list, suggesting the consistent dominating of the european football.
- The only south american in the list is Lautaro Martinez, the argentine astro.

# What I learned
In this project, i was allowed to practice more python coding, an using pandas, i understood more about explore, filtering and managing data in general.

# Challenges I Faced

- Problems with team matchmaking: In the third plot, when a team was local and later visitor, the dataframe treated it as a different encounter.

# Conclusions
My exploration into the history of the international matches in football has been so fun and informative, letting me to know more about one of my favorite sports. This project is good to anyone who wants to learn more about football history and curiosities.