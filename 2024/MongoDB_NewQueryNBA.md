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
db.games.aggregate([
  {
    $group: {
      _id: "$HOME_TEAM_ID",
      count: { $sum: 1 }
    }
  }
])
```


Data Manipulation Operations:
Operations that modify the underlying data.
