# Neo4J Lab 3 for BDI

In this lab, we are using a credit card transaction dataset and learning how to use Neo4j to model and query graph data. We will start by creating nodes for each entity in the dataset, such as customers, credit cards, transactions, and merchants, and connecting them with relationships that represent the interactions between these entities. We will also learn how to use Cypher, the query language for Neo4j, to retrieve and modify data in the graph.

Throughout the lab, we will cover various aspects of graph modeling and querying, such as creating and deleting nodes and relationships, filtering and aggregating data, and traversing relationships between nodes. By the end of the lab, we will have a good understanding of how to use Neo4j to model and query complex graph data, and how it can be used to gain insights and make data-driven decisions in various industries such as finance, social networking, and supply chain management.

#### 1. Install Neo4j: Download and install Neo4j Desktop from the Neo4j website (https://neo4j.com/download/).

#### 2. Create a new project: Open Neo4j Desktop, click on "Create a New Project," and give it a name (e.g., "BankCreditCards").

#### 3. Create a new database: Within the newly created project, click on "Add Database" and choose "Create a Local Database." Give it a name (e.g., "BankCreditCardsDB").

#### 4. Start the database: Select the newly created database and click on "Start."

#### 5. Open the Neo4j Browser: In the Neo4j Desktop, click on the "Open Neo4j Browser" button next to the database.

#### 6. Create the "Customer" node: Use the following command to create a "Customer" node:

```
CREATE (:Customer {customer_id: 1234, name: "John Smith", age: 35, location: "San Francisco", income: 75000, occupation: "Engineer", credit_score: 800})
```

#### 7. Create the "CreditCard" node: Use the following command to create a "CreditCard" node:

```
CREATE (:CreditCard {card_number: "1234567890123456", card_type: "Visa", card_limit: 10000, balance: 8000, credit_age: 2, reward_program_status: "Silver", payment_history: ["on-time payment", "late payment"]})
```

#### 8. Create a relationship between "Customer" and "CreditCard" nodes: Use the following command to create a "OWNS" relationship between the "Customer" and "CreditCard" nodes:

```
MATCH (c:Customer), (cc:CreditCard) WHERE c.customer_id = 1234 AND cc.card_number = "1234567890123456" 
CREATE (c)-[:OWNS]->(cc)
```

#### 9. View the graph: Refresh the Neo4j Browser and click on the "Graph" tab to see the nodes and their relationship.


#### 10. Create an "Address" node: Use the following command to create an "Address" node:
```
CREATE (:Address {address_id: 123, street: "123 Main St", city: "San Francisco", state: "CA", zip_code: "94101"})
```

#### 11. Create a relationship between "Customer" and "Address" nodes: Use the following command to create a "LIVES_AT" relationship between the "Customer" and "Address" nodes:
```
MATCH (c:Customer), (a:Address) WHERE c.customer_id = 1234 AND a.address_id = 123 
CREATE (c)-[:LIVES_AT]->(a)
```

#### 12. View the graph: Refresh the Neo4j Browser and click on the "Graph" tab to see the nodes and their relationships.

#### 13. Retrieve all "Customer" nodes: Use the following command to retrieve all "Customer" nodes:

```
MATCH (c:Customer) RETURN c
```

#### 14. Retrieve all "CreditCard" nodes: Use the following command to retrieve all "CreditCard" nodes:

```
MATCH (cc:CreditCard) RETURN cc
```

#### 15. Retrieve all "Address" nodes: Use the following command to retrieve all "Address" nodes:

```
MATCH (a:Address) RETURN a
```

#### 16. Retrieve a "Customer" node by its ID: Use the following command to retrieve a "Customer" node by its ID:

```
MATCH (c:Customer {customer_id: 1234}) RETURN c
```

#### 17. Retrieve a "CreditCard" node by its card number: Use the following command to retrieve a "CreditCard" node by its card number:
```
MATCH (cc:CreditCard {card_number: "1234567890123456"}) RETURN cc
```
#### 18. Create an index on the "name" property of the "Customer" nodes:
```
CREATE INDEX ON :Customer(name)
```
#### 19. Retrieve all "Customer" nodes sorted by their names: Use the following command to retrieve all "Customer" nodes sorted by their names:
```
MATCH (c:Customer) RETURN c ORDER BY c.name
```
#### 20. Update the "balance" property of a "CreditCard" node: Use the following command to update the "balance" property of a "CreditCard" node:
```
MATCH (cc:CreditCard {card_number: "1234567890123456"}) SET cc.balance = 9000
```
#### 21. Retrieve all "CreditCard" nodes sorted by their balances in descending order: Use the following command to retrieve all "CreditCard" nodes sorted by their balances in descending order:
```
MATCH (cc:CreditCard) RETURN cc ORDER BY cc.balance DESC
```


#### 22. Retrieve all "Customer" nodes and their associated "CreditCard" nodes: Use the following command to retrieve all "Customer" nodes and their associated "CreditCard" nodes:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) RETURN c, cc
```
#### 23. Retrieve all "Customer" nodes and their associated "Address" nodes: Use the following command to retrieve all "Customer" nodes and their associated "Address" nodes:
```
MATCH (c:Customer)-[:LIVES_AT]->(a:Address) RETURN c, a
```
#### 24. Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance greater than 5000:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance > 5000 RETURN c, cc
```
#### 25. Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance between 5000 and 10000:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance > 5000 AND cc.balance < 10000 RETURN c, cc
```
#### 26. Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance less than 5000:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance < 5000 RETURN c, cc
```


#### 27 . Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance less than 5000 and are of "Visa" card type:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance < 5000 AND cc.card_type = "Visa" RETURN c, cc
```
#### 28. Create a "Merchant" node: Use the following command to create a "Merchant" node:
```
CREATE (:Merchant {merchant_id: 1, name: "Amazon", location: "Seattle"})
```
#### 29. Create a "Transaction" node: Use the following command to create a "Transaction" node:
```
CREATE (:Transaction {transaction_id: 1, amount: 100, transaction_date: "2022-04-08"})
```
#### 30. Create a relationship between "CreditCard" and "Merchant" nodes: Use the following command to create a "PURCHASED_FROM" relationship between the "CreditCard" and "Merchant" nodes:
```
MATCH (cc:CreditCard {card_number: "1234567890123456"}), (m:Merchant {merchant_id: 1}) CREATE (cc)-[:PURCHASED_FROM]->(m)
```
#### 31. Create a relationship between "Transaction" and "CreditCard" nodes: Use the following command to create a "MADE" relationship between the "Transaction" and "CreditCard" nodes:
```
MATCH (cc:CreditCard {card_number: "1234567890123456"}), (t:Transaction {transaction_id: 1}) CREATE (cc)-[:MADE]->(t)
```
#### 32. Retrieve all "Transaction" nodes and their associated "CreditCard" and "Merchant" nodes: Use the following command to retrieve all "Transaction" nodes and their associated "CreditCard" and "Merchant" nodes:
```
MATCH (t:Transaction)<-[:MADE]-(cc:CreditCard)-[:PURCHASED_FROM]->(m:Merchant) RETURN t, cc, m
```
#### 33. Retrieve all "Customer" nodes and their associated "Transaction" nodes: Use the following command to retrieve all "Customer" nodes and their associated "Transaction" nodes:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard)-[:MADE]->(t:Transaction) RETURN c, t
```
#### 34. Use the following command to retrieve all "Customer" nodes with "Transaction" nodes that have an amount greater than 50:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard)-[:MADE]->(t:Transaction) WHERE t.amount > 50 RETURN c, cc, t
```
#### 35. Use the following command to retrieve all "Customer" nodes with "Transaction" nodes that have an amount between 50 and 150:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard)-[:MADE]->(t:Transaction) WHERE t.amount > 50 AND t.amount < 150 RETURN c, cc, t
```
#### 36. Use the following command to retrieve all "Customer" nodes with "Transaction" nodes that have an amount less than 150:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard)-[:MADE]->(t:Transaction) WHERE t.amount < 150 RETURN c, cc, t
```


#### 37. Use the following command to retrieve all "Customer" nodes with "Transaction" nodes that have an amount less than 150 and were made to the "Amazon" merchant:

 ```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard)
MATCH (cc)-[:PURCHASED_FROM]->(m:Merchant {name: "Amazon"})
MATCH (cc)-[:MADE]->(t:Transaction)
WHERE t.amount < 150
RETURN c, cc, m, t
```
#### 38. Create an index on the "card_number" property of the "CreditCard" nodes:
```
CREATE INDEX ON :CreditCard(card_number)
```
#### 39. Use the following command to retrieve all "CreditCard" nodes with a balance greater than 5000 using the index:
```
MATCH (cc:CreditCard) WHERE cc.balance > 5000 RETURN cc
```
#### 40. Use the following command to retrieve all "CreditCard" nodes with a balance less than 5000 using the index:
```
MATCH (cc:CreditCard) WHERE cc.balance < 5000 RETURN cc
```
#### 41. Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance greater than 5000 using the index:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance > 5000 RETURN c, cc
```
#### 42. Use the following command to retrieve all "Customer" nodes with "CreditCard" nodes that have a balance less than 5000 using the index:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) WHERE cc.balance < 5000 RETURN c, cc
```
#### 43. Use the following command to retrieve the total number of "Customer" nodes:
```
MATCH (c:Customer) RETURN count(c)
```
#### 44. Use the following command to retrieve the average age of all "Customer" nodes:
```
MATCH (c:Customer) RETURN avg(c.age)
```
#### 45. Use the following command to retrieve the total balance of all "CreditCard" nodes:
```
MATCH (cc:CreditCard) RETURN sum(cc.balance)
```
#### 46. Use the following command to retrieve the number of "CreditCard" nodes grouped by their card type:
```
MATCH (cc:CreditCard) RETURN cc.card_type, count(cc)
```
#### 47. Use the following command to retrieve all "Customer" nodes and their associated "CreditCard" nodes, sorted by the customer's age:
```
MATCH (c:Customer)-[:OWNS]->(cc:CreditCard) RETURN c, cc ORDER BY c.age
```

#### 48. Delete a "Customer" node and all of its relationships: Use the following command to delete a "Customer" node and all of its relationships:
```
MATCH (c:Customer {customer_id: 1234}) DETACH DELETE c
```
#### 49. Delete a "CreditCard" node and all of its relationships: Use the following command to delete a "CreditCard" node and all of its relationships:
```
MATCH (cc:CreditCard {card_number: "1234567890123456"}) DETACH DELETE cc
```
#### 50. Delete an "Address" node and all of its relationships: Use the following command to delete an "Address" node and all of its relationships:
```
MATCH (a:Address {address_id: 123}) DETACH DELETE a
```
