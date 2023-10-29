  
# MongoDB Lab 2 (Intermediate Lab) 

# Part 1: Launch an MongoDB server

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
output
```perl
'switched to db productdb'
```

This will create a new database called "productdb" if it does not already exist, or switch to the "productdb" database if it does exist.

## Step 5: Delete a database
To delete a database in MongoDB, use the `dropDatabase()` method on the database object. For example, to delete the "mydb" database, run the following command:
```perl
use productdb
db.dropDatabase()
```

## Step 6: Create a new collection
To create a new collection in MongoDB, use the `db.createCollection()` method followed by the name of the collection you want to create. For example, to create a new collection called "products", run the following command:
```arduino
db.createCollection("products")

```
Output
```css
{ok: 1}

```

This will create a new collection called "products" in the "productdb" database.
## Step 7: Insert data into the collection
To insert data into the "products" collection, use the `db.products.insertOne()` method followed by a JSON object representing the data you want to insert. For example, to insert a new product into the "products" collection, run the following command:
```json
db.products.insertOne({
    "name": "Product 1",
    "price": 10.0,
    "category": "Category 1"
})

```
Output
```css
{
  acknowledged: true,
  insertedId: ObjectId("643070ef92a85fbdb1811d9c")
}
```

This will insert a new document into the "products" collection with the "name", "price", and "category" fields set to the specified values.
## Step 8: Insert multiple documents into the collection
To insert multiple documents into the "products" collection, use the `db.products.insertMany()` method followed by an array of JSON objects representing the data you want to insert. For example, to insert two new products into the "products" collection, run the following command:
```json
db.products.insertMany([    
            {        "name": "Product 2",        "price": 20.0,        "category": "Category 1"    },   
            {        "name": "Product 3",        "price": 30.0,        "category": "Category 2"    } ,  
            {        "name": "Product 4",        "price": 30.0,        "category": "Category 4"    }])

```
Output
```css
 {
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("6430712692a85fbdb1811d9d"),
    '1': ObjectId("6430712692a85fbdb1811d9e"),
    '2': ObjectId("6430712692a85fbdb1811d9f")
  }
}
```

This will insert two new documents into the "products" collection with the "name", "price", and "category" fields set to the specified values.


## Step 9: Update documents in the collection
To update documents in the "products" collection, use the `db.products.updateOne()` or `db.products.updateMany()` method followed by a filter query and an update query. For example, to update the price of a single product in the "products" collection, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1"},
    {"$set": {"price": 15.0}}
)

```
Output
```css
 {
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
This will update the price of the "Product 1" document in the "products" collection to 15.0.

## Step 10: Delete documents from the collection
To delete documents from the "products" collection, use the `db.products.deleteOne()` or `db.products.deleteMany()` method followed by a filter query. For example, to delete a single product from the "products" collection, run the following command:
```json
db.products.deleteOne({"name": "Product 4"})

```
Output
```json
{
  acknowledged: true,
  deletedCount: 1
}
```
This will delete the "Product 4" document from the "products" collection.
These are just some basic steps for creating a product database in MongoDB using the MongoDB shell. There are many more advanced features and techniques you can use with MongoDB and Pymongo to create more complex databases and applications.


 
--------
## In-Class Excise - Complete the following Step using the nba database
 

