
#### 1. Install Neo4j on your machine and start the Neo4j server.

#### 2. Create a new Neo4j database.

#### 3. Load the data provided using the following commands:
```
CREATE (:Person {name: 'Alice', age: 25, city: 'New York'})
CREATE (:Person {name: 'Bob', age: 30, city: 'Los Angeles'})
CREATE (:Person {name: 'Charlie', age: 35, city: 'San Francisco'})
CREATE (:Person {name: 'David', age: 40, city: 'Seattle'})
CREATE (:Person {name: 'Emma', age: 20, city: 'Boston'})
CREATE (:Organization {name: 'Acme Inc.', industry: 'Technology'})
CREATE (:Organization {name: 'XYZ Corporation', industry: 'Finance'})
CREATE (:Organization {name: 'ABC LLC', industry: 'Retail'})
```

#### 4. Add a "FRIENDS_WITH" relationship between David and Emma using the following command:
```
MATCH (david:Person {name: 'David'}), (emma:Person {name: 'Emma'})
CREATE (david)-[:FRIENDS_WITH]->(emma)
```

#### 5. Add a "PARTNERS_WITH" relationship between Acme Inc. and XYZ Corporation using the following command:
```
MATCH (acme:Organization {name: 'Acme Inc.'}), (xyz:Organization {name: 'XYZ Corporation'})
CREATE (acme)-[:PARTNERS_WITH]->(xyz)
```

#### 6. Add a "PARTNERS_WITH" relationship between XYZ Corporation and ABC LLC using the following command:
```
MATCH (xyz:Organization {name: 'XYZ Corporation'}), (abc:Organization {name: 'ABC LLC'})
CREATE (xyz)-[:PARTNERS_WITH]->(abc)
```

#### 7. Query the database to retrieve all nodes labeled "Person" using the following command:
```
MATCH (person:Person)
RETURN person
```

#### 8. Filter the previous query to only retrieve nodes labeled "Person" who are over the age of 30 using the following command:
```
MATCH (person:Person)
WHERE person.age > 30
RETURN person
```

#### 9. Retrieve all nodes labeled "Organization" using the following command:
```
MATCH (org:Organization)
RETURN org
```

#### 10. Retrieve all "PARTNERS_WITH" relationships using the following command:
```
MATCH ()-[:PARTNERS_WITH]->()
RETURN *
```

#### 11. Retrieve all "FRIENDS_WITH" relationships using the following command:
```
MATCH ()-[:FRIENDS_WITH]->()
RETURN *
```

#### 12. Aggregate the number of nodes labeled "Person" by city using the following command:
```
MATCH (person:Person)
RETURN person.city, COUNT(person)
GROUP BY person.city
```

#### 13.  Delete all nodes labeled "Organization" using the following command:
```
MATCH (org:Organization)
DETACH DELETE org
```

#### 14. Delete all "PARTNERS_WITH" relationships using the following command:
```
MATCH ()-[r:PARTNERS_WITH]->()
DELETE r
```
#### 15. Delete all nodes labeled "Person" using the following command:
```
MATCH (person:Person)
DETACH DELETE person
```
Good job!
