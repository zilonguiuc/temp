# 1.Basic Operations:
These are standard CRUD (Create, Read, Update, Delete) operations and other fundamental operations

## Loading Data (NBA data player_game.csv) into MongoDB

1. **Connect to your MongoDB instance using Compass.**
2. **Select the desired database**, or create a new one.
3. **Select the desired collection**, or create a new one.
4. **Add Data**: 
    - Once inside the collection, you'll see an `ADD DATA` dropdown on the right side.
    - Click it and select `Import File`.
5. **Choose the data file** (JSON or CSV) you want to import. 
    - Configure the options accordingly and click `Import`.

## Displaying a Sample Document:
```
db.player_game.findOne()
```

## Displaying a Few Documents:
```
db.player_game.find().limit(5)
```

## Count of Documents:
```
db.player_game.count()
```

# 2.Query Operation 

## Query result to find certain documents (similar to SQL syntax where)
**Find player who can scored exactly 20 points in a game**
```
db.player_game.find({ PTS: 20 })
```
**Find players who scored above 20 points:**
```
db.player_game.find({ PTS_home: { $gt: 20 } })
```
**Find players who scored between 21 to 29 points:**
```
db.player_game.find({ PTS_home: { $gt: 20, $lt: 30 } })
```
**Find players who started in the Center (C) position:**
```
db.player_game.find({ start_position: "C" })
```
## Query result with and OR
**Find Players who Scored More than 20 Points and had More than 5 Blocks in a Game**
```
db.player_game.find({ PTS : { $gt: 20 }, BLK: { $gt:  5} })
```

**Find Players who Scored More than 20 Points or had Less than 10 Blocks in a Game**
```
db.player_game.find({ $or: [ { PTS: { $gt: 20 } }, { BLK: { $lt: 10 } } ] })
```

## Using Projections, silimar to select columns in SQL:
**returns players who scored more than 20 points, but only displays their names (PLAYER_NAME) and points (PTS)**
```
db.player_game.find({ PTS: { $gt: 20 } }, { PLAYER_NAME: 1, PTS: 1 })
```

## Sort results
**retrieves the top 5 scoring games based on the points (PTS) in descending order.**
```
db.player_game.find({}).sort({ PTS: -1 }).limit(5)
```

 
# 3.Data Summary:
## Numerical Variables:
**This aggregates the data to provide a summary of the PTS field including count, average, minimum, maximum, and standard deviation**
```
db.player_game.aggregate([
  {
    $group: {
      _id: null,
      count: { $sum: 1 },
      avg_pts: { $avg: "$PTS" },
      min_pts: { $min: "$PTS" },
      max_pts: { $max: "$PTS" },
      stddev_pts: { $stdDevPop: "$PTS" }
    }
  }
])

```
## Categorical Variables:
**This groups the data by starting position (START_POSITION) and provides a count of occurrences for each position**
```
db.player_game.aggregate([
  {
    $group: {
      _id: "$START_POSITION",
      count: { $sum: 1 }
    }
  }
])

```

# 4.Advanced Query Operations:
## Aggregations:
**This aggregates the average points (PTS) scored by each team**
```
db.player_game.aggregate([
  {
    $group: { 
        _id: "$TEAM_ID", 
        avg_points_per_team: { $avg: "$PTS" } 
    }
  }
])
```
## Adding New Fields:
**This adds a new field called total_attempts, which is the sum of field goal attempts (FGA), three-point field goal attempts (FG3A), and free throw attempts (FTA)**
```
db.player_game.aggregate([
  {
    $addFields: {
        total_attempts: { $add: ["$FGA", "$FG3A", "$FTA"] }
    }
  }
])
```


## Text Search:  
**The first line creates a text index on the COMMENT field. The second query is a placeholder to find documents with a specific text "coach" within the COMMENT field**

db.games.createIndex({ COMMENT: "text" })
db.games.find({ $text: { $search: "coach" } })

**We can also search the comments containing coach use regular expression but it is much slower for big data**
db.games.find({ COMMENT: /^coach/i })

# 5.Data Manipulation Operations: Operations that modify the underlying data.
## Handling Missing Data:
**For example, handling missing data in points field (PTS): This replaces any missing PTS values with 0**
```
db.player_game.aggregate([
  {
    $project: {
        GAME_ID: 1,
        PLAYER_NAME: 1,
        PTS: { $ifNull: ["$PTS", 0] }
    }
  }
])
```

## Deleting Documents:
**This deletes all documents where the player scored less than 5 points**
```
db.player_game.deleteMany({ PTS: { $lt: 5 } })
```

## Renaming Fields:
**For example, renaming PLAYER_NAME to player:**
```
db.player_game.updateMany({}, { $rename: { "PLAYER_NAME": "player" } })
```

## Upserting:
**Updating or inserting a record based on GAME_ID and PLAYER_ID:**
```
db.player_game.updateOne({ GAME_ID: "21900895", PLAYER_ID: "202083" }, { $set: { PTS: 15 } }, { upsert: true })
```

## Inserting Nested Documents: 
**Inserts a document with a nested location field. The second query finds games played in "NBA City".**
```
db.games.insertOne({
    GAME_ID: "12345678",
    TEAM_ID: 101
    PLAYER_ID: 101
    PTS: 10
    location: {
        stadium: "Progressive Arena",
        city: "ClevelandCleveland",
        state: "OH",
        zip: "61822"
    }
})
```

## Query Nested Documents: 
**finds games played in "NBA City".**
```
db.games.find({ "location.city": "ClevelandCleveland" })
```
## Diagnostics:
**This explains the query plan for fetching players who scored more than 20 points.**
db.player_game.find({ PTS: { $gt: 20 } }).explain()

## Join with another collection
**First create another collection called team and load the data.**


**Joins the player_game collection with the team  collection based on team_id and places the result in the player_team_details array.**
```
db.games.aggregate([
  {
    $lookup: {
        from: "team",
        localField: "team_id",
        foreignField: "team_id",
        as: "player_team_details"
    }
  }
])
```

# 7.Create and drop database
## Create an new database called NBA2;
```
use NBA2
```

## Create an new collection within the NBA2 database and called ranking.
```
db.createCollection("ranking")
```

## Insert one record for Lakers
```
db.ranking.insertOne({
    "team": "Lakers",
    "winning_ratio": 0.7,
    "conference": "western"
})
```

## Delete entire collection:
**This deletes the player_game collections**
```
db.ranking.drop()
```

## Delete the NBA2 database
```
db.dropDatabase()
```
 

