  
# MongoDB Lab 2 (Intermediate) 

This manual covers MongoDB basic CRUD operations


## Step 1: Install MongoDB Community Version
The first step in creating a MongoDB database is to install MongoDB on your machine. You can download MongoDB from the official MongoDB website.
https://www.mongodb.com/docs/manual/administration/install-community/

## Step 2: Start the MongoDB server
After installing MongoDB, you need to start the MongoDB server. To start the server, open a command prompt or terminal window and run the following command, you might have to add the path of mongod into your local environment first before excuting the command:
```
mongod

```
This will start the MongoDB server on the default port 27017.
## Step 3: Connect to the MongoDB server
To connect to the MongoDB server, open a new command prompt or terminal window and run the following command, you might have to add the path of mongo into your local environment first before excuting the command:
```
mongo

```
This will open the MongoDB shell and connect to the MongoDB server running on the default port.
## Step 4: Create a new database
To create a new database in MongoDB, use the `use` command followed by the name of the database you want to create. For example, to create a new database called "productdb", run the following command:
```perl
use productdb

```
This will create a new database called "productdb" if it does not already exist, or switch to the "productdb" database if it does exist.
## Step 5: Create a new collection
To create a new collection in MongoDB, use the `db.createCollection()` method followed by the name of the collection you want to create. For example, to create a new collection called "products", run the following command:
```arduino
db.createCollection("products")

```
This will create a new collection called "products" in the "productdb" database.
## Step 6: Insert data into the collection
To insert data into the "products" collection, use the `db.products.insertOne()` method followed by a JSON object representing the data you want to insert. For example, to insert a new product into the "products" collection, run the following command:
```json
db.products.insertOne({
    "name": "Product 1",
    "price": 10.0,
    "category": "Category 1"
})

```
This will insert a new document into the "products" collection with the "name", "price", and "category" fields set to the specified values.
## Step 7: Insert multiple documents into the collection
To insert multiple documents into the "products" collection, use the `db.products.insertMany()` method followed by an array of JSON objects representing the data you want to insert. For example, to insert two new products into the "products" collection, run the following command:
```json
db.products.insertMany([    
            {        "name": "Product 2",        "price": 20.0,        "category": "Category 1"    },   
            {        "name": "Product 3",        "price": 30.0,        "category": "Category 2"    } ,  
            {        "name": "Product 4",        "price": 30.0,        "category": "Category 4"    }])

```
This will insert two new documents into the "products" collection with the "name", "price", and "category" fields set to the specified values.
## Step 8: Query the collection
To query the "products" collection, use the `db.products.find()` method. For example, to retrieve all documents in the "products" collection, run the following command:
```lua
db.products.find()

```
This will return a cursor to all documents in the "products" collection.
## Step 9: Update documents in the collection
To update documents in the "products" collection, use the `db.products.updateOne()` or `db.products.updateMany()` method followed by a filter query and an update query. For example, to update the price of a single product in the "products" collection, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1"},
    {"$set": {"price": 15.0}}
)

```
This will update the price of the "Product 1" document in the "products" collection to 15.0.
## Step 10: Delete documents from the collection
To delete documents from the "products" collection, use the `db.products.deleteOne()` or `db.products.deleteMany()` method followed by a filter query. For example, to delete a single product from the "products" collection, run the following command:
```json
db.products.deleteOne({"name": "Product 4"})

```
This will delete the "Product 4" document from the "products" collection.
These are just some basic steps for creating a product database in MongoDB using the MongoDB shell. There are many more advanced features and techniques you can use with MongoDB and Pymongo to create more complex databases and applications.


## Step 11: Create an index on a field
To create an index on a field in the "products" collection, use the `db.products.createIndex()` method followed by the name of the field you want to index. For example, to create an index on the "name" field in the "products" collection, run the following command:
```json
db.products.createIndex({"name": 1})

```
This will create an ascending index on the "name" field in the "products" collection.

## Step 12: Query with a filter and projection
To query the "products" collection with a filter and projection, use the `db.products.find()` method followed by a filter query and a projection. For example, to retrieve the name and price of all products in the "Category 1" category, run the following command:
```lua
db.products.find(
    {"category": "Category 1"},
    {"_id": 0, "name": 1, "price": 1}
)

```
This will return a cursor to all documents in the "products" collection with the "category" field set to "Category 1", with only the "name" and "price" fields included in the results.
## Step 13: Limit the number of results
To limit the number of results returned by a query, use the `limit()` method on the cursor returned by the `find()` method. For example, to retrieve only the first two products in the "products" collection, run the following command:
```scss
products = db.products.find().limit(2)
for product in products:
    print(product)

```
This will return a cursor to the first two documents in the "products" collection.
## Step 14: Skip results
To skip a certain number of results before returning the remaining results, use the `skip()` method on the cursor returned by the `find()` method. For example, to retrieve all products in the "products" collection except for the first two, run the following command:
```scss
products = db.products.find().skip(2)
for product in products:
    print(product)

```
This will return a cursor to all documents in the "products" collection, except for the first two.
## Step 15: Sort results
To sort the results of a query, use the `sort()` method on the cursor returned by the `find()` method. For example, to retrieve all products in the "products" collection sorted by price in ascending order, run the following command:
```lua
products = db.products.find().sort("price")
for product in products:
    print(product)

```
This will return a cursor to all documents in the "products" collection, sorted by price in ascending order.
These are just a few more steps for working with a product database in MongoDB using the MongoDB shell. There are many more features and techniques you can use to create complex queries and manage your database.


 --------
 
 ## Step 16: Query with an OR condition
To query the "products" collection with an OR condition, use the `$or` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "Category 1" category with a price greater than or equal to 20.0 OR in the "Category 2" category with a price less than or equal to 10.0, run the following command:
```bash
db.products.find({
    "$or": [
        {"category": "Category 1", "price": {"$gte": 20.0}},
        {"category": "Category 2", "price": {"$lte": 10.0}}
    ]
})

```
This will return a cursor to all documents in the "products" collection that match either of the two conditions.
## Step 17: Query with an IN operator
To query the "products" collection with an IN operator, use the `$in` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "Category 1" OR "Category 2" categories, run the following command:
```bash
db.products.find({
    "category": {"$in": ["Category 1", "Category 2"]}
})

```
This will return a cursor to all documents in the "products" collection that have a "category" field value of either "Category 1" or "Category 2".
## Step 18: Query with a regular expression
To query the "products" collection with a regular expression, use the `$regex` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection with a name that starts with "Product", run the following command:
```bash
db.products.find({
    "name": {"$regex": "^Product"}
})

```
This will return a cursor to all documents in the "products" collection with a "name" field value that starts with "Product".
## Step 19: Query with an exists operator
To query the "products" collection with an exists operator, use the `$exists` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection that have a "description" field, run the following command:
```bash
db.products.find({
    "description": {"$exists": true}
})

```
This will return a cursor to all documents in the "products" collection that have a "description" field.
## Step 20: Query with a comparison operator
To query the "products" collection with a comparison operator, use operators such as `$lt`, `$lte`, `$gt`, and `$gte` in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection with a price less than or equal to 20.0, run the following command:
```bash
db.products.find({
    "price": {"$lte": 20.0}
})

```
This will return a cursor to all documents in the "products" collection that have a "price" field value less than or equal to 20.0.


 
## Step 21: Update multiple documents with a filter query
To update multiple documents in the "products" collection with a filter query, use the `updateMany()` method. For example, to update the price of all products in the "Category 1" category to 25.0, run the following command:
```bash
db.products.updateMany(
    {"category": "Category 1"},
    {"$set": {"price": 25.0}}
)

```
This will update the price of all documents in the "products" collection with the "category" field set to "Category 1" to 25.0.
## Step 22: Update a nested field
To update a nested field in a document in the "products" collection, use dot notation in the update query. For example, to update the "quantity" field of a product with a specific name and size, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "size": "small"},
    {"$set": {"details.quantity": 10}}
)

```
This will update the "quantity" field in the "details" sub-document of the "Product 1" document with the "size" field set to "small".
## Step 23: Increment a field value
To increment a field value in a document in the "products" collection, use the `$inc` operator in the update query. For example, to increment the "quantity" field of a product with a specific name and size by 5, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "size": "small"},
    {"$inc": {"details.quantity": 5}}
)

```
This will increment the "quantity" field in the "details" sub-document of the "Product 1" document with the "size" field set to "small" by 5.
## Step 24: Rename a field
To rename a field in a document in the "products" collection, use the `$rename` operator in the update query. For example, to rename the "category" field to "product_category" in a specific product document, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "size": "small"},
    {"$rename": {"category": "product_category"}}
)

```
This will rename the "category" field to "product_category" in the "Product 1" document with the "size" field set to "small".
## Step 25: Remove a field
To remove a field from a document in the "products" collection, use the `$unset` operator in the update query. For example, to remove the "details" sub-document from a specific product document, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "size": "small"},
    {"$unset": {"details": ""}}
)

```
This will remove the "details" sub-document from the "Product 1" document with the "size" field set to "small".

## Step 26: Delete a collection
To delete a collection from a database in MongoDB, use the `drop()` method on the collection object. For example, to delete the "products" collection from the current database, run the following command:
```scss
db.products.drop()

```
This will delete the "products" collection from the current database.
## Step 27: Delete a database
To delete a database in MongoDB, use the `dropDatabase()` method on the database object. For example, to delete the "mydb" database, run the following command:
```perl
use mydb
db.dropDatabase()

```
This will delete the "mydb" database from the MongoDB server. Note that you must switch to the database you want to delete before calling `dropDatabase()`.


 --------
 