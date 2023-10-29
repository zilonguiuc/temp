
  
# MongoDB Lab 2 (Intermediate Lab) 

This manual covers MongoDB basic CRUD operations


## Step 1: Open Local MongoDB Compass on your laptop or Open an Instance on GCP




This will create a new collection called "products" in the "productdb" database.
## Step 2: Load the following NBA data into the database
 

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



## Step 29: Delete a database
To delete a database in MongoDB, use the `dropDatabase()` method on the database object. For example, to delete the "mydb" database, run the following command:
```perl
use mydb
db.dropDatabase()

```
This will delete the "mydb" database from the MongoDB server. Note that you must switch to the database you want to delete before calling `dropDatabase()`.


 --------
 
