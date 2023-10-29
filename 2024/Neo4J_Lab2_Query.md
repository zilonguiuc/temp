 
# Introduction to Neo4j
Neo4j is a graph database management system that is used to store, manage, and query large, complex graphs. It is designed to handle highly connected data and to enable efficient traversal of relationships between nodes. In this notebook, we will explore the basic concepts of Neo4j and learn how to use it to create, query, and manipulate graph data.
## Installing Neo4j
Before we get started, you need to have Neo4j installed on your system. You can download the appropriate version of Neo4j for your operating system from the official website:  https://neo4j.com/download/
## Basic Concepts (Creation and deletion)
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

## Importing and Exporting Data (Use NBA Database)
Neo4j also provides functionality for importing and exporting data to and from your graph database. This can be useful for migrating data between different environments, backing up your data, or importing data from external sources.
To import data into Neo4j, you can use the `LOAD CSV` clause to load data from a CSV file (The CSV file must be saved in the import folder of the neo4j data folder):
```sql
LOAD CSV WITH HEADERS FROM 'file:///data_neo4j.csv' AS row
CREATE (:Person {name: row.name, age: toInteger(row.age), city: row.city})

OR From a external URL

LOAD CSV WITH HEADERS FROM 'https://raw.githubusercontent.com/zilonguiuc/badm558/main/data_neo4j.csv' AS row
CREATE (:Person {name: row.name, age: toInteger(row.age), city: row.city})

```
This creates a "Person" node for each row in the "data.csv" file.



## Querying Data
Once you have data stored in Neo4j, you can query it using the Cypher query language. Cypher is a declarative query language that is specifically designed for querying graph data.

### Basic Queries
To retrieve data from a Neo4j graph, you use the MATCH clause followed by the RETURN clause to specify the data you want to retrieve. The MATCH clause specifies the pattern to match in the graph, and the RETURN clause specifies the data to return. For example, to retrieve all nodes labeled "Person", you would use the following query:

```
MATCH (person:Person)
RETURN person
```

This returns all nodes labeled "Person" in the graph. 
 
 
### Filtering Results
You can also filter query results using the `WHERE` clause. The `WHERE` clause allows you to specify conditions that must be met for a node or relationship to be included in the results.
For example, to retrieve all nodes labeled "Person" with the name "Alice", you would use the following query:
```sql
MATCH (person:Person)
WHERE person.name = 'Alice'
RETURN person

OR

MATCH (person:Person {name: 'Alice'})
RETURN person

```
This returns all nodes labeled "Person" with the name "Alice".
You can also use comparison operators and logical operators in the `WHERE` clause to specify more complex conditions:
```sql
MATCH (person:Person)
WHERE person.age > 20 AND person.city = 'New York'
RETURN person

```
This returns all nodes labeled "Person" with an age greater than 20 and a city of "New York".
### Traversing Relationships
One of the most powerful features of Neo4j is the ability to traverse relationships between nodes. To traverse a relationship, you use the `MATCH` clause followed by the `--` or `-->` syntax to specify the direction of the relationship, and the `RETURN` clause to specify the data you want to retrieve.
For example, to retrieve all nodes labeled "Company" that are connected to Alice by a "WORKS_FOR" relationship, you would use the following query:
```css
MATCH (alice:Person {name: 'Alice'})-[:MEMBER_OF]->(group:Group)
RETURN group

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
In Cypher, GROUP BY is done implicitly by all of the aggregate functions. In a WITH/RETURN statement, any columns not part of an aggregate will be the GROUP BY key. You can also use the aggregate clause to group results by a particular property:
 
```sql
MATCH (person:Person)
RETURN COUNT(person), person.city 

```
This returns the number of nodes labeled "Person" for each unique value of the "city" property.



 

## Conclusion
In this notebook, we have learned the basic concepts of Neo4j and how to use it to create, query, and manipulate graph data. We covered nodes, relationships, properties, querying data, filtering results, traversing relationships, aggregating data, and modifying data. With this knowledge, you should be able to start working with Neo4j and exploring the power of graph databases.

  
