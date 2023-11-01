Setting Up & Loading Data:
Let's assume you've imported the data into Neo4j as nodes with label Player, and each player has a relationship PLAYS_FOR to a node with label Team.

cypher
Copy code
LOAD CSV WITH HEADERS FROM 'file:///player_team.csv' AS line
MERGE (p:Player {PLAYER_ID: line.PLAYER_ID})
SET p.PLAYER_NAME = line.PLAYER_NAME, p.SEASON = toInteger(line.SEASON)
MERGE (t:Team {TEAM_ID: line.TEAM_ID})
MERGE (p)-[:PLAYS_FOR]->(t);

Displaying a Sample Record:
```
MATCH (p:Player)
RETURN p
LIMIT 1;
```


Displaying Multiple Records:
```
MATCH (p:Player)-[r:PLAYS_FOR]->(t:Team)
RETURN p.PLAYER_NAME, t.TEAM_ID, p.PLAYER_ID, p.SEASON
LIMIT 5;
```

Count of Players:
MATCH (p:Player)
RETURN COUNT(p) AS PlayerCount;


Filtering Players by Season:
MATCH (p:Player)
WHERE p.SEASON = 2019
RETURN p.PLAYER_NAME;

 Filtering Players by Season and Team:
cypher
Copy code
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
WHERE p.SEASON = 2019 AND t.TEAM_ID = '1610612762'
RETURN p.PLAYER_NAME;
2. Filtering Players by Multiple Seasons (Using OR):
Suppose you're interested in players who played in either the 2019 or 2020 seasons:

cypher
Copy code
MATCH (p:Player)
WHERE p.SEASON = 2019 OR p.SEASON = 2020
RETURN p.PLAYER_NAME;
3. Filtering Players excluding a Season:
To get players who didn't play in the 2019 season:

cypher
Copy code
MATCH (p:Player)
WHERE NOT p.SEASON = 2019
RETURN p.PLAYER_NAME;

4. Combining AND and OR:
Imagine you want players who played in 2019 for a specific team or those who played in 2020 for another team:

cypher
Copy code
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
WHERE (p.SEASON = 2019 AND t.TEAM_ID = '1610612762') OR (p.SEASON = 2020 AND t.TEAM_ID = '1610612763')
RETURN p.PLAYER_NAME;
5. Filtering by Range:
To get players who played between 2018 and 2020:

cypher
Copy code
MATCH (p:Player)
WHERE p.SEASON >= 2018 AND p.SEASON <= 2020
RETURN p.PLAYER_NAME;


. Find all players for a specific team:
Given a TEAM_ID, you can fetch all players associated with that team.
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team {TEAM_ID: '1610612762'})
RETURN p.PLAYER_NAME;

2. Find the team for a specific player:
Given a PLAYER_NAME or PLAYER_ID, you can retrieve the team they play for.
MATCH (p:Player {PLAYER_NAME: 'Rudy Gobert'})-[:PLAYS_FOR]->(t:Team)
RETURN t.TEAM_ID;


3. Find teammates of a specific player:
To find players who share the same team relationship as a specific player:
MATCH (p1:Player {PLAYER_NAME: 'Rudy Gobert'})-[:PLAYS_FOR]->(t:Team)<-[:PLAYS_FOR]-(p2:Player)
WHERE p1 <> p2
RETURN p2.PLAYER_NAME;


5. Determine if two players play for the same team:
You can check if two specific players share the same team relationship.
MATCH (p1:Player {PLAYER_NAME: 'Rudy Gobert'})-[:PLAYS_FOR]->(t:Team)<-[:PLAYS_FOR]-(p2:Player {PLAYER_NAME: 'Joe Ingles'})
RETURN t.TEAM_ID;


 2. Data Summaries and Aggregations:
a. List Teams and Their Player Count:
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
RETURN t.TEAM_ID, COUNT(p) AS PlayerCount;

b. Unique Player Count by Season:
MATCH (p:Player)
RETURN p.SEASON, COUNT(DISTINCT p.PLAYER_NAME) AS UniquePlayers;

c. Teams with Most Players:
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
WITH t, COUNT(p) AS PlayerCount
ORDER BY PlayerCount DESC
RETURN t.TEAM_ID, PlayerCount
LIMIT 5;

3. Data Manipulation Operations:
a. Adding a New Player Record:
CREATE (p:Player {PLAYER_NAME: "New Player", PLAYER_ID: "1234567", SEASON: 2020})

b. Updating a Player's Name:
MATCH (p:Player {PLAYER_ID: "1234567"})
SET p.PLAYER_NAME = "Updated Player Name"
RETURN p;

c. Deleting a Player:
MATCH (p:Player {PLAYER_ID: "1234567"})
DETACH DELETE p;

d. Adding a Relationship (e.g., a new player for a team):
MATCH (p:Player {PLAYER_ID: "1234567"}), (t:Team {TEAM_ID: "1610612762"})
MERGE (p)-[:PLAYS_FOR]->(t);


4. Advanced Query Operations:
a. Filtering Players based on Team and Season:
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
WHERE t.TEAM_ID = '1610612762' AND p.SEASON = 2019
RETURN p.PLAYER_NAME;

b. Finding Players without a Team (if any exist):
MATCH (p:Player)
WHERE NOT (p)-[:PLAYS_FOR]->(:Team)
RETURN p.PLAYER_NAME;

To delete all players in a specific team
MATCH (p:Player)-[:PLAYS_FOR]->(t:Team)
WHERE t.TEAM_ID = 'YourTeamIDHere'
DETACH DELETE p;


deleting all nodes.

MATCH (n)
DETACH DELETE n;


