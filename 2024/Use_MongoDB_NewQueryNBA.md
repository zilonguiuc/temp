# Basic Operations:
These are standard CRUD (Create, Read, Update, Delete) operations and other fundamental operations

## Loading Data into MongoDB

## Displaying a Sample Document:

```
db.player_game.findOne()
```

### Displaying a Few Documents:

```
db.player_game.find().limit(5)
```

### Count of Documents:
```
db.player_game.count()
```


# Query Operation 

### Query result filer, similar to SQL where
```
db.player_game.find({ PTS_home: 20 })
```

```
db.player_game.find({ PTS_home: { $gt: 20 } })
```

```
db.player_game.find({ PTS_home: { $gt: 20, $lt: 30 } })
```

```
db.player_game.find({ start_position: "C" })
```

### Query result with and OR

```
db.player_game.find({ PTS : { $gt: 20 }, BLK: { $gt:  5} })
```

```
db.player_game.find({ $or: [ { PTS: { $gt: 100 } }, { BLK: { $lt: 90 } } ] })
```


### Using Projections, silimar to select columns in SQL:
```
db.player_game.find({ PTS: { $gt: 20 } }, { PLAYER_NAME: 1, PTS: 1 })
```

### sort
db.player_game.find({}).sort({ PTS: -1 }).limit(5)

### Text Search: [Note: The sample doesn't include a game_description field, so this is hypothetical.]

```
db.player_game.createIndex({ COMMENT: "text" })
db.player_game.find({ $text: { $search: "??" } })
```


## Data Summary:
### Numerical Variables:
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

Categorical Variables:
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

## Advanced Query Operations:
Aggregations:
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


Adding New Fields:
```
db.player_game.aggregate([
  {
    $addFields: {
        total_attempts: { $add: ["$FGA", "$FG3A", "$FTA"] }
    }
  }
])
```



Text Search: [Note: The sample doesn't include a game_description field, so this is hypothetical.]

db.games.createIndex({ COMMENT: "text" })
db.games.find({ $text: { $search: "coach" } })


db.games.find({ COMMENT: /^coach/i })


## Data Manipulation Operations:
Operations that modify the underlying data.

### Handling Missing Data:
For example, handling missing data in points field (PTS):
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

Deleting Documents:
Deleting players with less than 5 points:

db.player_game.deleteMany({ PTS: { $lt: 5 } })


Renaming Fields:
For example, renaming PLAYER_NAME to player:
db.player_game.updateMany({}, { $rename: { "PLAYER_NAME": "player" } })

Upserting:
Updating or inserting a record based on GAME_ID and PLAYER_ID:
db.player_game.updateOne({ GAME_ID: "21900895", PLAYER_ID: "202083" }, { $set: { PTS: 15 } }, { upsert: true })

Inserting Nested Documents: [This is a hypothetical example since the sample data doesn't contain nested fields.]

db.games.insertOne({
    GAME_ID: "12345678",
    TEAM_ID:
    PLAYER_ID: 
    PTS: 105
    location: {
        stadium: "NBA Arena",
        city: "NBA City",
        state: "NBA State",
        zip: "12345"
    }
})


db.games.find({ "location.city": "NBA City" })




Delete collection:
db.player_game.


Diagnostics:
db.player_game.find({ PTS: { $gt: 20 } }).explain()


join with other table
```
db.games.aggregate([
  {
    $lookup: {
        from: "teams",
        localField: "HOME_TEAM_ID",
        foreignField: "team_id",
        as: "home_team_details"
    }
  }
])
```

create an new collection within the same database and called ranking.
use zz

insert one record
db.insertone

delete ranking collection
db.your_collection_name.drop()
