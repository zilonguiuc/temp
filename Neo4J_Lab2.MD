 
# Introduction to Neo4j
Neo4j is a graph database management system that is used to store, manage, and query large, complex graphs. It is designed to handle highly connected data and to enable efficient traversal of relationships between nodes. In this notebook, we will explore the basic concepts of Neo4j and learn how to use it to create, query, and manipulate graph data.
## Installing Neo4j
Before we get started, you need to have Neo4j installed on your system. You can download the appropriate version of Neo4j for your operating system from the official website:  https://neo4j.com/download/
## Basic Concepts
In Neo4j, data is stored as a set of nodes and relationships between them. Nodes represent entities in the graph, and relationships represent connections between those entities. Both nodes and relationships can have properties, which are key-value pairs that provide additional information about the entity.
### Nodes
Nodes are the basic building blocks of a Neo4j graph. They represent entities in the graph and can be labeled to categorize them. Each node can have multiple properties associated with it.
To create a node in Neo4j, you use the `CREATE` clause followed by the `(:Label)` syntax to specify the label for the node, and `{property: value}` syntax to specify any properties:
```css
CREATE (:Label {property: value})

```
For example, to create a node representing a person named Alice, you would use the following query:
```css
CREATE (:Person {name: 'Alice'})

```
This creates a node labeled "Person" with a single property "name" set to "Alice".
You can also create multiple nodes at once using the `CREATE` clause followed by a comma-separated list of nodes:
```css
CREATE (:Person {name: 'Bob'}), (:Company {name: 'Acme'})

```
This creates a node labeled "Person" with a single property "name" set to "Bob", and a node labeled "Company" with a single property "name" set to "Acme".
### Relationships
Relationships are used to connect nodes in the graph. They represent connections between entities and can be directed or undirected. Relationships can also have properties, which are key-value pairs that provide additional information about the relationship.
To create a relationship in Neo4j, you use the `MATCH` clause to find the nodes you want to connect, followed by the `CREATE` clause and `[:TYPE {property: value}]` syntax to specify the type and any properties for the relationship:
```scss
MATCH (node1:Label1), (node2:Label2)
CREATE (node1)-[:TYPE {property: value}]->(node2)

```
For example, to create a relationship between Alice and a node representing a company named Acme, you would use the following query:
```css
MATCH (alice:Person {name: 'Alice'}), (acme:Company {name: 'Acme'})
CREATE (alice)-[:WORKS_FOR {since: 2020}]->(acme)

```
This creates a directed relationship labeled "WORKS_FOR" with a single property "since" set to 2020, connecting Alice to Acme.
You can also create multiple relationships at once using the `CREATE` clause followed by a comma-separated list of relationships:
```css
MATCH (bob:Person {name: 'Bob'}), (acme:Company {name: 'Acme'})
CREATE (bob)-[:WORKS_FOR {since: 2015}]->(acme), (bob)-[:FRIEND_OF]->(alice)

```
 
This creates a directed relationship labeled "WORKS_FOR" with a single property "since" set to 2015, connecting Bob to Acme, and an undirected relationship labeled "FRIEND_OF" connecting Bob to Alice.
## Querying Data
Once you have data stored in Neo4j, you can query it using the Cypher query language. Cypher is a declarative query language that is specifically designed for querying graph data.

```
CREATE (:Person {name: 'Alice', age: 25, city: 'New York'})
CREATE (:Person {name: 'Bob', age: 30, city: 'Los Angeles'})
CREATE (:Person {name: 'Charlie', age: 35, city: 'San Francisco'})
CREATE (:Group {name: 'Neo4j User Group', location: 'Online'})
CREATE (:Group {name: 'Data Science Club', location: 'New York'})
CREATE (:Group {name: 'Hiking Club', location: 'Los Angeles'})
```

### Basic Queries
To retrieve data from a Neo4j graph, you use the MATCH clause followed by the RETURN clause to specify the data you want to retrieve. The MATCH clause specifies the pattern to match in the graph, and the RETURN clause specifies the data to return. For example, to retrieve all nodes labeled "Person", you would use the following query:

```
MATCH (person:Person)
RETURN person
```

This returns all nodes labeled "Person" in the graph. You can also specify multiple labels in the MATCH clause to retrieve nodes that have any of those labels:
```
MATCH (node:Label1 OR Label2)
RETURN node
```
```
MATCH (node:Person OR Group)
RETURN node
```
 
### Filtering Results
You can also filter query results using the `WHERE` clause. The `WHERE` clause allows you to specify conditions that must be met for a node or relationship to be included in the results.
For example, to retrieve all nodes labeled "Person" with the name "Alice", you would use the following query:
```sql
MATCH (person:Person)
WHERE person.name = 'Alice'
RETURN person

```
This returns all nodes labeled "Person" with the name "Alice".
You can also use comparison operators and logical operators in the `WHERE` clause to specify more complex conditions:
```sql
MATCH (person:Person)
WHERE person.age > 30 AND person.city = 'New York'
RETURN person

```
This returns all nodes labeled "Person" with an age greater than 30 and a city of "New York".
### Traversing Relationships
One of the most powerful features of Neo4j is the ability to traverse relationships between nodes. To traverse a relationship, you use the `MATCH` clause followed by the `--` or `-->` syntax to specify the direction of the relationship, and the `RETURN` clause to specify the data you want to retrieve.
For example, to retrieve all nodes labeled "Company" that are connected to Alice by a "WORKS_FOR" relationship, you would use the following query:
```css
MATCH (alice:Person {name: 'Alice'})-[:WORKS_FOR]->(company:Company)
RETURN company

```
This returns all nodes labeled "Company" that are connected to Alice by a "WORKS_FOR" relationship.
You can also specify a variable-length path using the `*` syntax:
```css
MATCH (alice:Person {name: 'Alice'})-[:FRIEND_OF*2]->(friend:Person)
RETURN friend

```
This returns all nodes labeled "Person" that are exactly two "FRIEND_OF" relationships away from Alice.
### Aggregating Data
You can also aggregate data in Neo4j using the `COUNT`, `SUM`, `AVG`, `MIN`, and `MAX` functions. These functions allow you to perform calculations on the data in your graph.
For example, to retrieve the number of nodes labeled "Person" in the graph, you would use the following query:
```scss
MATCH (person:Person)
RETURN COUNT(person)

```
This returns the number of nodes labeled "Person" in the graph.
You can also use the `GROUP BY` clause to group results by a particular property:
 
```sql
MATCH (person:Person)
RETURN person.city, COUNT(person)
GROUP BY person.city

```
This returns the number of nodes labeled "Person" for each unique value of the "city" property.
## Modifying Data
In addition to querying data, you can also modify data in a Neo4j graph. You use the `CREATE`, `MERGE`, `SET`, and `DELETE` clauses to create, update, and delete nodes and relationships.
### Creating Nodes and Relationships
We already covered how to create nodes and relationships in Neo4j using the `CREATE` clause. You can also use the `MERGE` clause to create a node or relationship only if it does not already exist:
```css
MERGE (person:Person {name: 'Alice'})
MERGE (company:Company {name: 'Acme'})
MERGE (person)-[:WORKS_FOR {since: 2020}]->(company)

```
This creates a node labeled "Person" with the name "Alice", a node labeled "Company" with the name "Acme", and a "WORKS_FOR" relationship connecting them, but only if they do not already exist.

 
### Indexing and Constraints
In addition to the basic concepts of nodes and relationships, Neo4j also supports indexing and constraints to help optimize data access and enforce data integrity.
Indexes can be used to improve the performance of queries that filter on specific properties. You can create indexes in Neo4j using the `CREATE INDEX` clause:
```css
CREATE INDEX ON :Person(name)

```
This creates an index on the "name" property of all nodes labeled "Person".
Constraints can be used to enforce unique or required properties on nodes and relationships. You can create constraints in Neo4j using the `CREATE CONSTRAINT` clause:
```sql
CREATE CONSTRAINT ON (person:Person) ASSERT person.name IS UNIQUE

```
This creates a unique constraint on the "name" property of all nodes labeled "Person", ensuring that no two nodes have the same name.


### Using Labels and Properties in Queries
In addition to filtering and matching nodes by label and property values, you can also use these values in other parts of your query. For example, you can use the `SET` clause to update a property value based on another property value:
```sql
MATCH (person:Person)
WHERE person.age > 30
SET person.is_adult = true

```
This updates the "is_adult" property of all nodes labeled "Person" with an age greater than 30 to true.
You can also use labels and properties in the `RETURN` clause to customize your query output:
```vbnet
MATCH (person:Person)
WHERE person.city = 'New York'
RETURN person.name AS name, person.age AS age

```
This returns the "name" and "age" properties of all nodes labeled "Person" with a "city" property of "New York".
### Working with Date and Time Data
Neo4j also supports date and time data types, which can be useful for working with time series data or event data. You can store date and time data as properties on nodes or relationships, and query and filter based on these values.
For example, you can use the `datetime()` function to create a datetime value:
```css
CREATE (:Event {name: 'New Year\'s Eve', date: datetime('2022-12-31T23:59:59Z')})

```
This creates an "Event" node with the name "New Year's Eve" and a "date" property set to December 31, 2022 at 11:59:59 PM UTC.
You can then use date and time functions to manipulate and compare these values:
```vbnet
MATCH (event:Event)
WHERE event.date > datetime('2022-12-31T18:00:00Z') AND event.date < datetime('2023-01-01T06:00:00Z')
RETURN event.name

```
This returns the name of all "Event" nodes with a "date" property between 6:00 PM and 6:00 AM on New Year's Eve.
### Using Transactions
Neo4j supports transactions, which allow you to group multiple database operations into a single unit of work. Transactions ensure that either all of the operations in the transaction are completed successfully, or none of them are.
To use transactions in Neo4j, you can use the `BEGIN`, `COMMIT`, and `ROLLBACK` clauses:
```css
BEGIN
CREATE (:Person {name: 'Bob', age: 40})
CREATE (:Person {name: 'Alice', age: 35})
COMMIT

```
This creates two "Person" nodes in a single transaction.
If you encounter an error while executing a transaction, you can use the `ROLLBACK` clause to undo any changes made in the transaction:
```php
BEGIN
CREATE (:Person {name: 'Bob', age: 40})
CREATE (:Person {name: 'Alice', age: 35})
CREATE (:Person {name: 'Bob', age: 50}) // This line will cause an error
COMMIT

```
This transaction will fail due to the duplicate "name" property value in the third node, and all changes made in the transaction will be rolled back.

### Updating Nodes and Relationships
You can use the `SET` clause to update the properties of a node or relationship:
```css
MATCH (person:Person {name: 'Alice'})
SET person.age = 35

```
This updates the "age" property of the node labeled "Person" with the name "Alice" to 35.
You can also use the `SET` clause to add or remove properties:
```php
MATCH (person:Person {name: 'Alice'})
SET person.city = 'New York', person.age = 35

```
This adds a "city" property to the node labeled "Person" with the name "Alice" and sets it to "New York", and updates the "age" property to 35.
### Deleting Nodes and Relationships
You use the `DELETE` clause to delete nodes and relationships:
```css
MATCH (person:Person {name: 'Alice'})-[r:WORKS_FOR]->(company:Company)
DELETE r, person

```
This deletes the "WORKS_FOR" relationship between the node labeled "Person" with the name "Alice" and the node labeled "Company", and then deletes the "Person" node.

### Importing and Exporting Data
Neo4j also provides functionality for importing and exporting data to and from your graph database. This can be useful for migrating data between different environments, backing up your data, or importing data from external sources.
To import data into Neo4j, you can use the `LOAD CSV` clause to load data from a CSV file:
```sql
LOAD CSV WITH HEADERS FROM 'file:///data.csv' AS row
CREATE (:Person {name: row.name, age: toInteger(row.age), city: row.city})

```
This creates a "Person" node for each row in the "data.csv" file.
To export data from Neo4j, you can use the `neo4j-admin` command-line tool to create a backup of your database:
```css
neo4j-admin backup --backup-dir=/var/neo4j/backup --name=mydatabase

```
This creates a backup of the "mydatabase" database in the "/var/neo4j/backup" directory.

## Conclusion
In this notebook, we have learned the basic concepts of Neo4j and how to use it to create, query, and manipulate graph data. We covered nodes, relationships, properties, querying data, filtering results, traversing relationships, aggregating data, and modifying data. With this knowledge, you should be able to start working with Neo4j and exploring the power of graph databases.

  
