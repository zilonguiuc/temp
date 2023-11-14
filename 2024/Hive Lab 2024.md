## Step 1: Downloading Data from GitHub
### Objective: Retrieve the NBA data files from GitHub.

wget [URL_of_ranking.csv]
wget [URL_of_team.csv]

## Step 2: Uploading Data to HDFS (Hadoop Distributed File System)
### Objective: Store the downloaded data in HDFS.
 
hdfs dfs -mkdir /user/[username]/nba_data
hdfs dfs -put ranking.csv /user/[username]/nba_data/ranking.csv
hdfs dfs -put team.csv /user/[username]/nba_data/team.csv

 
## Step 3: Setting Up Hive
### Objective: Prepare the Hive environment for data manipulation.
Activities:Start Hive shell:

hive

##Step 4: Creating Tables in Hive
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
Step 5: Loading Data into Hive Tables
Objective: Populate the Hive tables with data from HDFS.
Hive Commands:
For the Ranking Data:
sql
Copy code
LOAD DATA INPATH '/user/[username]/nba_data/ranking.csv' INTO TABLE nba_ranking;
For the Team Data:
sql
Copy code
LOAD DATA INPATH '/user/[username]/nba_data/team.csv' INTO TABLE nba_team;
Step 6: Querying and Manipulating Data
Objective: Execute various queries and data manipulations.
Examples of Hive Queries:
Simple query to list all teams:
sql
Copy code
SELECT * FROM nba_team;
Join query between ranking and team data:
sql
Copy code
SELECT r.team, r.w, r.l, t.city, t.arena
FROM nba_ranking r
JOIN nba_team t ON r.team_id = t.team_id;
Advanced queries involving group by, order by, etc.
Step 7: Cleanup and Close
Objective: Properly end the session and clean up if necessary.
Commands:
Exit Hive shell:
bash
Copy code
exit;
Additional Notes:
Customization: Modify the table creation queries based on the exact structure of your CSV files.
Error Handling: Ensure students know how to troubleshoot common errors in Hive and Hadoop.
Practice: Include exercises that require students to write their own Hive queries.
