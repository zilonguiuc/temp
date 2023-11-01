# Basic Operations:
These are standard CRUD (Create, Read, Update, Delete) operations and other fundamental operations

## Loading Data into MongoDB

## Displaying a Sample Document:

```
db.games.findOne()
```

### Displaying a Few Documents:

```
db.games.find().limit(5)
```

### Count of Documents:
```
db.games.count()
```

### Query result filer, similar to SQL where
```
db.games.find({ PTS_home: 100 })
```

```
db.games.find({ PTS_home: { $gt: 100 } })
```

```
db.games.find({ PTS_home: { $gt: 100, $lt: 120 } })
```

```
db.games.find({ start_position: "C" })
```

### Query result with and OR

```
db.games.find({ PTS_home: { $gt: 100 }, PTS_away: { $lt: 90 } })
```

```
db.games.find({ $or: [ { PTS_home: { $gt: 100 } }, { PTS_away: { $lt: 90 } } ] })
```


### Using Projections, silimar to select columns in SQL:
```
db.games.find({ PTS_home: { $gt: 100 } }, { HOME_TEAM_ID: 1, PTS_home: 1 })
```
