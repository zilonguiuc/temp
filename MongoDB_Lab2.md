  
# MongoDB Lab 2 (Intermediate Lab) 

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
output
```perl
'switched to db productdb'
```

This will create a new database called "productdb" if it does not already exist, or switch to the "productdb" database if it does exist.
## Step 5: Create a new collection
To create a new collection in MongoDB, use the `db.createCollection()` method followed by the name of the collection you want to create. For example, to create a new collection called "products", run the following command:
```arduino
db.createCollection("products")

```
Output
```css
{ok: 1}

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
Output
```css
{
  acknowledged: true,
  insertedId: ObjectId("643070ef92a85fbdb1811d9c")
}
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
## Step 8: Query the collection
To query the "products" collection, use the `db.products.find()` method. For example, to retrieve all documents in the "products" collection, run the following command:
```lua
db.products.find()

```

Output
```css
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 10,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9f"),
  name: 'Product 4',
  price: 30,
  category: 'Category 4'
}
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


## Step 11: Create an index on a field
To create an index on a field in the "products" collection, use the `db.products.createIndex()` method followed by the name of the field you want to index. For example, to create an index on the "name" field in the "products" collection, run the following command:
```json
db.products.createIndex({"name": 1})

```
Output
```json
'name_1'
```
This will create an ascending index on the "name" field in the "products" collection.

--------
Note: Indexes in MongoDB are similar to indexes in other databases, in that they help to improve the performance of queries by allowing the database to quickly locate the relevant data. An index is essentially a data structure that is created on one or more fields in a collection, which can be used to optimize queries on those fields.

When you create an index on a field in MongoDB, the database creates a separate data structure that contains the indexed field's values, along with a reference to the document that contains each value. This index data structure is stored separately from the actual data in the collection, and is optimized for efficient lookups and sorting.

When you query a collection, MongoDB will first check to see if there is an appropriate index available for the query. If there is, it will use the index to quickly locate the relevant documents and return the results. This can be much faster than scanning the entire collection for the relevant data, especially for large collections.

--------

## Step 12: Query with a filter and projection
To query the "products" collection with a filter and projection, use the `db.products.find()` method followed by a filter query and a projection. For example, to retrieve the name and price of all products in the "Category 1" category, run the following command:
```lua
db.products.find(
    {"category": "Category 1"},
    {"_id": 0, "name": 1, "price": 1}
)

```
Output
```lua
{
  name: 'Product 1',
  price: 15
}
{
  name: 'Product 2',
  price: 20
}
```

This will return a cursor to all documents in the "products" collection with the "category" field set to "Category 1", with only the "name" and "price" fields included in the results.

--------
Note: In MongoDB, a projection is a query operation that selects a subset of fields from the documents in a collection. When you run a projection query, MongoDB returns only the selected fields for each matching document, instead of returning the entire document.
 
In MongoDB, you can specify a projection using the `find()` method and passing a document as the second argument that specifies which fields to include or exclude from the results. For example, the following code selects only the `name` and `age` fields from the `users` collection:
```javascript
db.products.find({}, { name: 1, price: 1, _id: 0 })

```
In this example, the first argument `{}` selects all documents in the `users` collection. The second argument `{ name: 1, price: 1, _id: 0 }` specifies that only the `name` and `price` fields should be returned, and that the `_id` field should be excluded. The `1` value indicates that the field should be included in the results, while the `0` value indicates that the field should be excluded.  (or you can simply omit "_id" in the projection and still get the same results.)


 --------


## Step 13: Limit the number of results
To limit the number of results returned by a query, use the `limit()` method on the cursor returned by the `find()` method. For example, to retrieve only the first two products in the "products" collection, run the following command:
```scss
products = db.products.find().limit(2)
 
```
Output
```scss
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
```
This will return a cursor to the first two documents in the "products" collection.
## Step 14: Skip results
To skip a certain number of results before returning the remaining results, use the `skip()` method on the cursor returned by the `find()` method. For example, to retrieve all products in the "products" collection except for the first two, run the following command:
```scss
products = db.products.find().skip(2)

```
Output
```scss
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
```
This will return a cursor to all documents in the "products" collection, except for the first two.
## Step 15: Sort results
To sort the results of a query, use the `sort()` method on the cursor returned by the `find()` method. For example, to retrieve all products in the "products" collection sorted by price in ascending order, run the following command:
```lua
products = db.products.find().sort("price")

```
Output
```lua
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
```
This will return a cursor to all documents in the "products" collection, sorted by price in ascending order.
These are just a few more steps for working with a product database in MongoDB using the MongoDB shell. There are many more features and techniques you can use to create complex queries and manage your database.


 --------
 
 ## Step 16: Query with an OR condition
To query the "products" collection with an OR condition, use the `$or` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "Category 1" category with a price greater than or equal to 20.0 OR in the "Category 2" category with a price less than or equal to 40.0, run the following command:
```bash
db.products.find({
    "$or": [
        {"category": "Category 1", "price": {"$gte": 20.0}},
        {"category": "Category 2", "price": {"$lte": 40.0}}
    ]
})

```
Output
```bash
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
```
This will return a cursor to all documents in the "products" collection that match either of the two conditions.
## Step 17: Query with an IN operator
To query the "products" collection with an IN operator, use the `$in` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "Category 1" OR "Category 2" categories, run the following command:
```bash
db.products.find({
    "category": {"$in": ["Category 1", "Category 2"]}
})

```
Output
```bash
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
```
This will return a cursor to all documents in the "products" collection that have a "category" field value of either "Category 1" or "Category 2".
## Step 18: Query with a regular expression
To query the "products" collection with a regular expression, use the `$regex` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection with a name that starts with "Product", run the following command:
```bash
db.products.find({
    "name": {"$regex": "^Product 1"}
})

```
Output
```bash
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
```

This will return a cursor to all documents in the "products" collection with a "name" field value that starts with "Product".
## Step 19: Query with an exists operator
To query the "products" collection with an exists operator, use the `$exists` operator in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection that have a "description" field, run the following command:
```bash
db.products.find({
    "description": {"$exists": true}
})

```
Output
```bash
Nothing returned
``` 
This will return a cursor to all documents in the "products" collection that have a "description" field.

```bash
db.products.find({
    "description": {"$exists": false}
})

```
Output
```bash
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9e"),
  name: 'Product 3',
  price: 30,
  category: 'Category 2'
}
``` 
This will return a cursor to all documents in the "products" collection that do not have a "description" field.
## Step 20: Query with a comparison operator
To query the "products" collection with a comparison operator, use operators such as `$lt`, `$lte`, `$gt`, and `$gte` in the filter query passed to the `find()` method. For example, to retrieve all products in the "products" collection with a price less than or equal to 20.0, run the following command:
```bash
db.products.find({
    "price": {"$lte": 20.0}
})

```
Output
```bash
{
  _id: ObjectId("643070ef92a85fbdb1811d9c"),
  name: 'Product 1',
  price: 15,
  category: 'Category 1'
}
{
  _id: ObjectId("6430712692a85fbdb1811d9d"),
  name: 'Product 2',
  price: 20,
  category: 'Category 1'
}
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
Output
```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 2,
  upsertedCount: 0
}

```
This will update the price of all documents in the "products" collection with the "category" field set to "Category 1" to 25.0.
## Step 22: Drop all documents in a collection
To drop all records from the "products" collection in MongoDB, you can use the deleteMany() method with an empty filter object {}. This will match all documents in the collection and delete them. Here's an example:

```bash 
db.products.deleteMany({})
```
Output
```bash 
{
  acknowledged: true,
  deletedCount: 6
}
```
This will delete all documents in the "products" collection.

## Step 23: Insert nested documents in a collection
You can use the insertMany() method to insert three new documents into the products collection in the productdb database. Each document has a name, price, category, and details field, with nested fields for size and quantity. The documents represent products with different categories, sizes, quantities, and prices.
```bash 
db.products.insertMany([
  {
    name: "Product 1",
    price: 10,
    category: "Category 1",
    details: {
      size: "small",
      quantity: 5
    }
  },
  {
    name: "Product 2",
    price: 20,
    category: "Category 2",
    details: {
      size: "medium",
      quantity: 10
    }
  },
  {
    name: "Product 3",
    price: 30,
    category: "Category 3",
    details: {
      size: "large",
      quantity: 15
    }
  }
]);
```
Output
```bash 
{
  acknowledged: true,
  insertedIds: {
    '0': ObjectId("6430764492a85fbdb1811da0"),
    '1': ObjectId("6430764492a85fbdb1811da1"),
    '2': ObjectId("6430764492a85fbdb1811da2")
  }
}
```
insertion is successful.
## Step 24: Update a nested field
To update a nested field in a document in the "products" collection, use dot notation in the update query. For example, to update the "quantity" field of a product with a specific name and size, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "details.size": "small"},
    {"$set": {"details.quantity": 10}}
)

```
Output
```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
This will update the "quantity" field in the "details" sub-document of the "Product 1" document with the "details.size" field set to "small".
## Step 25: Increment a field value
To increment a field value in a document in the "products" collection, use the `$inc` operator in the update query. For example, to increment the "quantity" field of a product with a specific name and size by 5, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "details.size": "small"},
    {"$inc": {"details.quantity": 5}}
)

```
Output
```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
This will increment the "quantity" field in the "details" sub-document of the "Product 1" document with the "size" field set to "small" by 5. (so 10 increase to 15)
## Step 26: Rename a field
To rename a field in a document in the "products" collection, use the `$rename` operator in the update query. For example, to rename the "category" field to "product_category" in a specific product document, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "details.size": "small"},
    {"$rename": {"category": "product_category"}}
)

```
Output
```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```

This will rename the "category" field to "product_category" in the "Product 1" document with the "details.size" field set to "small".
## Step 27: Remove a field
To remove a field from a document in the "products" collection, use the `$unset` operator in the update query. For example, to remove the "details" sub-document from a specific product document, run the following command:
```bash
db.products.updateOne(
    {"name": "Product 1", "details.size": "small"},
    {"$unset": {"details": ""}}
)

```
Output
```bash
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}
```
This will remove the "details" sub-document from the "Product 1" document with the "details.size" field set to "small".

Try print out all collection one more time use db.products.find(), you will see below
```bash
db.products.find()
{
  _id: ObjectId("6430782c92a85fbdb1811da3"),
  name: 'Product 1',
  price: 10,
  product_category: 'Category 1'
}
{
  _id: ObjectId("6430782c92a85fbdb1811da4"),
  name: 'Product 2',
  price: 20,
  category: 'Category 2',
  details: {
    size: 'medium',
    quantity: 10
  }
}
{
  _id: ObjectId("6430782c92a85fbdb1811da5"),
  name: 'Product 3',
  price: 30,
  category: 'Category 3',
  details: {
    size: 'large',
    quantity: 15
  }
}
```

## Step 28: Delete a collection
To delete a collection from a database in MongoDB, use the `drop()` method on the collection object. For example, to delete the "products" collection from the current database, run the following command:
```scss
db.products.drop()

```
This will delete the "products" collection from the current database.
## Step 29: Delete a database
To delete a database in MongoDB, use the `dropDatabase()` method on the database object. For example, to delete the "mydb" database, run the following command:
```perl
use mydb
db.dropDatabase()

```
This will delete the "mydb" database from the MongoDB server. Note that you must switch to the database you want to delete before calling `dropDatabase()`.


 --------
 
