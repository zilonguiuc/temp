## Step 1: Downloading Data from GitHub
### Objective: Retrieve the NBA data files from GitHub.
```
wget [URL_of_ranking.csv]
wget [URL_of_team.csv]
```
## Step 2: Uploading Data to HDFS (Hadoop Distributed File System)
### Objective: Store the downloaded data in HDFS.
``` 
hdfs dfs -mkdir /user/[username]/nba_data
hdfs dfs -put ranking.csv /user/[username]/nba_data/ranking.csv
hdfs dfs -put team.csv /user/[username]/nba_data/team.csv
```
 
## Step 3: Setting Up Hive
### Objective: Prepare the Hive environment for data manipulation.
Activities:Start Hive shell:
```
hive
```
## Step 4: Creating Tables in Hive
### Objective: Create Hive tables to store the NBA data.
 
1. For the Ranking Data:
``` 
CREATE TABLE nba_ranking (
  team_id BIGINT,
  league_id INT,
  season_id STRING,
  standingsdate STRING,
  conference STRING,
  team STRING,
  g INT,
  w INT,
  l INT,
  w_pct FLOAT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

2. For the Team Data:
```
CREATE TABLE nba_team (
  league_id INT,
  team_id BIGINT,
  min_year INT,
  max_year INT,
  abbreviation STRING,
  nickname STRING,
  yearfounded INT,
  city STRING,
  arena STRING,
  arenacapacity STRING,
  owner STRING,
  generalmanager STRING,
  headcoach STRING,
  dleagueaffiliation STRING
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

## Step 5: Loading Data into Hive Tables
### Objective: Populate the Hive tables with data from HDFS.
Hive Commands:
For the Ranking Data:
``` 
LOAD DATA INPATH '/user/[username]/nba_data/ranking.csv' INTO TABLE nba_ranking;
```
For the Team Data:
```
LOAD DATA INPATH '/user/[username]/nba_data/team.csv' INTO TABLE nba_team;
```

## Step 6: Modify Hive Tables
### Part 1: Adding a Record to the nba_team Table
###  Objective: Insert a new team record called "Dragons" into the nba_team table.
Hive Query:
```
INSERT INTO nba_team 
VALUES (0, 1610612999, 2023, 2023, 'DGN', 'Dragons', 2023, 'Imaginary City', 'Dragon Arena', '20000', 'John Doe', 'Jane Smith', 'Alex Johnson', 'Imaginary D-League');
```
This query adds a new team with made-up details.

### Part 2: Updating a Record in the nba_team Table
### Objective: Update the arena name of the "Dragons" team.
Hive Query:
```
UPDATE nba_team 
SET arena = 'New Dragon Arena'
WHERE team_id = 1610612999 AND nickname = 'Dragons';
```
This updates the 'Dragons' team's arena name to 'New Dragon Arena'.
 
### Part 3: Deleting a Record from the nba_team Table
#### Objective: Delete the record of the "Dragons" team.
Hive Query:
```
DELETE FROM nba_team 
WHERE team_id = 1610612999;
```
This removes the 'Dragons' team from the table.
 

## Step 7: Querying and Manipulating Data
### Objective: Execute various queries and data manipulations.

a. Simple query to list all teams:
``` 
SELECT * FROM nba_team;
```

b. Join query between ranking and team data:
```
SELECT r.team, r.w, r.l, t.city, t.arena
FROM nba_ranking r
JOIN nba_team t ON r.team_id = t.team_id;
```
 
c. Identify the win ratio of each team on the latest day of each season, and creating a Temporary Table to Save Query Results
``` 
CREATE TABLE temp_latest_season_win_ratio AS
SELECT nr.season_id, nr.team_id, nr.team, nr.w_pct
FROM nba_ranking nr
INNER JOIN (
    SELECT team_id, season_id, MAX(standingsdate) as latest_date
    FROM nba_ranking
    GROUP BY team_id, season_id
) max_dates ON nr.team_id = max_dates.team_id AND nr.season_id = max_dates.season_id AND nr.standingsdate = max_dates.latest_date;

```

d. Based on prior query results, determine the team with the highest win ratio for each season.
```
SELECT t.season_id, t.team_id, t.team, t.w_pct
FROM (
    SELECT season_id, MAX(w_pct) as max_w_pct
    FROM temp_latest_season_win_ratio
    GROUP BY season_id
) as max_wins
JOIN temp_latest_season_win_ratio t ON max_wins.season_id = t.season_id AND max_wins.max_w_pct = t.w_pct;
```
 
## Step 8: Cleanup and Close
### Objective: Properly end the session and clean up if necessary.
Commands- Exit Hive shell:
``` 
exit;
```
---------------------------------------------------------------------------------
## In-Class Exercise: Hive Querying with NBA Player and Player-Team Data
## Exercise Setup:
### Task 1. Downloading Data
### Objective: Retrieve the NBA player and player-team data files from GitHub.

### Task 2.Uploading Data to HDFS
### Objective: Store the downloaded data in HDFS.
 
### Task 3. Creating Tables in Hive
1. For Player Data (nba_player):
2. For Player-Team Data (player_team):
 
### Task 4. Loading Data into Hive Tables
1. For Player Data:
2. For Player-Team Data:

### Task 5. Modify Data
1. Updating Player Information:Assume that there's a need to update the weight of a specific player due to incorrect data entry. For instance, let's say the weight of the player named "Aaron Gordon" needs to be corrected to 100 kg.
2. Insert a New Record: Add a new player record named "Mike Z", the record data is below 
('Mike Z', 200, 90, 'UIUC', 'USA', '2020', '1', '10', 999999);
3. Delete a Record: Remove a player record named Mike Z


### Task 6. Query Data
1. Find the average height and weight of players for each team for the 2019 season.
2. Determine the tallest player for each NBA team for the 2019 season.


-----------------------------------------------------------------------------------------------------------------------------------------------------
### In-Class Exercise Solutions: Hive Querying with NBA Player and Player-Team Data
 
### Task 1: Downloading Data
```
wget [URL_of_player.csv]
wget [URL_of_player_team.csv]
```
### Task 2: Uploading Data to HDFS
```
hdfs dfs -mkdir /user/[username]/nba_data
hdfs dfs -put player.csv /user/[username]/nba_data/player.csv
hdfs dfs -put player_team.csv /user/[username]/nba_data/player_team.csv
```
### Task 3: Creating Tables in Hive
For Player Data (nba_player):
```
CREATE TABLE nba_player (
  player_name STRING,
  player_height FLOAT,
  player_weight FLOAT,
  college STRING,
  country STRING,
  draft_year STRING,
  draft_round STRING,
  draft_number STRING,
  player_id BIGINT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```
For Player-Team Data (player_team):
```
CREATE TABLE player_team (
  player_name STRING,
  team_id BIGINT,
  player_id BIGINT,
  season INT
)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```

### Task 4: Loading Data into Hive Tables
For Player Data:
```
LOAD DATA INPATH '/user/[username]/nba_data/player.csv' INTO TABLE nba_player;
```

For Player-Team Data:
```
LOAD DATA INPATH '/user/[username]/nba_data/player_team.csv' INTO TABLE player_team;
```
### Task 5: Modify Data
1. Updating Player Information:
```
UPDATE nba_player SET player_weight = 100 WHERE player_name = 'Aaron Gordon';
```
2. Insert a New Record:
```
INSERT INTO nba_player VALUES ('Mike Z', 200, 90, 'UIUC', 'USA', '2020', '1', '10', 999999);
```
3. Delete a Record:
```
DELETE FROM nba_player WHERE player_name = 'Mike Z';
```

### Task 6: Query Data
Query 1:
```
SELECT pt.team_id, AVG(np.player_height) as avg_height, AVG(np.player_weight) as avg_weight
FROM nba_player np
JOIN player_team pt ON np.player_id = pt.player_id
WHERE pt.season = 2019
GROUP BY pt.team_id;
```

Query 2:
```
SELECT pt.team_id, np.player_name, MAX(np.player_height) as max_height
FROM nba_player np
JOIN player_team pt ON np.player_id = pt.player_id
WHERE pt.season = 2019
GROUP BY pt.team_id, np.player_name
ORDER BY pt.team_id, max_height DESC;
 ```
