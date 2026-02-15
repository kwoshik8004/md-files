# MongoDB (Basic to Advanced)

**MongoDB** is a powerful **NoSQL database** known for its flexible, **document-oriented storage** that is ideal for handling **large-scale**, **complex data**. 

> **MongoDB Atlas** (a cloud-based solution), **MongoDB Compass** (a GUI for data visualization) and the **MongoDB Shell** for command-line operations, users can efficiently perform **CRUD operations**.

The **MongoDB Aggregation Framework** enables advanced data analysis with **grouping**, **filtering** and **joining** capabilities. Perfect for scalable applications, MongoDB supports diverse operators and is optimized for modern data needs, making it a top choice for **dynamic, high-performance database** management.

## Basics of MongoDB
Before proceeding towards the MongoDB cheat sheet let's have a quick look on MongoDB basic.

| concept | details |
|--|--|
| What is MongoDB | MongoDB is a document-oriented NoSQL database that stores data in flexible, JSON-like documents |
| DataTypes in MongoDB | MongoDB supports various data types including string, integer, double, boolean, arrays, objects, dates, and null |
| What is ObjectId in MongoDB | ObjectId is a 12-byte hexadecimal number that uniquely identifies documents in a collection |
| MongoDB Atlas | MongoDB Atlas is a fully managed cloud database service. It provides automated backups, monitoring, and security features |
| MongoDB Compass | MongoDB Compass is a graphical user interface for MongoDB. It allows users to visualize data, run queries, and analyze performance |
| What is MongoDB Shell | MongoDB Shell is a command-line interface for interacting with MongoDB instances. It allows users to execute queries, perform administrative tasks, and manage databases |

## CRUD Operations in MongoDB
This section covers the basics of working with your MongoDB database using **CRUD operations**.

### Connect to MongoDB
``` bash
mongo
```
Open a terminal and start the **MongoDB shell** by typing mongo.

### Create and Use a Database
``` javascript
use blog
```
Create (if not exists) and use the `blog` database

### Create Collections
``` javascript
// Create a 'posts' collection
db.createCollection("posts")

// Create a 'users' collection
db.createCollection("users")
```

This creates two collections: posts for storing blog posts and users for storing user information.

### Insert Operations
Insert a single document into `posts` collection

``` javascript
db.posts.insertOne({
    title: "Introduction to MongoDB",
    content: "MongoDB is a NoSQL database.",
    author: "John Doe",
    tags: ["mongodb", "nosql", "database"]
})
```

Insert multiple documents into `users` collection

``` javascript
db.users.insertMany([
    {
        username: "johndoe",
        email: "johndoe@example.com",
        age: 30
    },
    {
        username: "janedoe",
        email: "janedoe@example.com",
        age: 28
    }
])
```

### Update Operations
Update a document in `users` collection

``` javascript
db.users.updateOne(
    { username: "johndoe" },
    { $set: { age: 31 } }
)
```

Update multiple documents in `posts` collection

``` javascript
db.posts.updateMany(
    { tags: "mongodb" },
    { $addToSet: { tags: "database" } }
)
```

### Delete Operations
Delete a document from `users` collection

``` javascript
db.users.deleteOne({ username: "janedoe" })
```

Delete multiple documents from `posts` collection

``` javascript
db.posts.deleteMany({ author: "John Doe" })
```

Drop the entire `users` collection

``` javascript
db.users.drop()
```

### Query Operations
Find all documents in `posts` collection

``` javascript
db.posts.find()
```

Find one document in `posts` collection

``` javascript
db.posts.findOne({ title: "Introduction to MongoDB" })
```

Find and modify a document in `posts` collection

``` javascript
db.posts.findOneAndUpdate(
    { title: "Introduction to MongoDB" },
    { $set: { content: "MongoDB is a flexible and scalable NoSQL database." } }
)
```

Find one and delete a document in `posts` collection

``` javascript
db.posts.findOneAndDelete({ author: "John Doe" })
```

Find one and replace a document in `posts` collection

``` javascript
db.posts.findOneAndReplace(
    { title: "Introduction to MongoDB" },
    { title: "MongoDB Overview", content: "A detailed guide to MongoDB." }
)
```

### Query with Projections
Find documents with projection (only return 'title' and 'author' fields)

``` javascript
db.posts.find({}, { title: 1, author: 1 })
```

Query nested documents (e.g., find users with email ending in '.com')

``` javascript
db.users.find({ "email": /.*\.com$/ })
```

Query documents with null or missing fields

``` javascript
db.users.find({ email: null })
```

### Show Database Information

``` javascript
// Show available databases
show dbs

// Show collections in the current database
show collections
```

To see a list of available databases and their collections

## MongoDB Operators
**MongoDB operators** are like tools that help you work with your data effectively. They allow you to find specific information, make changes and analyze your data in MongoDB.

Mastering these operators gives you the ability to manage and explore your data more efficiently, uncovering valuable insights along the way.

### 1. Comparison Operators
Find documents where age is greater than 30 in `users` collection

``` javascript
db.users.find({ age: { $gt: 30 } })
```

Find documents where age is less than or equal to 28 in `users` collection

``` javascript
db.users.find({ age: { $lte: 28 } })
```

Find documents where title is equal to "MongoDB Overview" in `posts` collection

``` javascript
db.posts.find({ title: { $eq: "MongoDB Overview" } })
```

Find documents where age is not equal to 30 in `users` collection

``` javascript
db.users.find({ age: { $ne: 30 } })
```

In these queries, we utilize the **$gt (greater than)**, **$lt (less than)**, and **$eq (equality)** comparison operators to filter documents based on specific criteria. Additionally, we demonstrate the $ne (not equal) operator to find documents where a field does not match a specified value.

### 2. Logical Operators
Find documents where age is greater than 25 AND less than 35 in `users` collection

``` javascript
db.users.find({ $and: [ { age: { $gt: 25 } }, { age: { $lt: 35 } } ] })
```

Find documents where username is "johndoe" OR email is "janedoe@example.com" in `users` collection

``` javascript
db.users.find({ $or: [ { username: "johndoe" }, { email: "janedoe@example.com" } ] })
```

Find documents where age is NOT equal to 30 in `users` collection

``` javascript
db.users.find({ age: { $not: { $eq: 30 } } })
```

Find documents where age is neither 30 nor 31 in `users` collection

``` javascript
db.users.find({ age: { $nor: [ { $eq: 30 }, { $eq: 31 } ] } })
```

> We use the `$and` operator to find documents where **multiple conditions must be satisfied simultaneously**. <br> The `$or` operator is utilized to find documents where **at least one of the specified conditions is met**. <br> Using the `$not` operator, we **exclude documents where a specific condition is true**. <br>The `$nor` operator is used to find documents where **none of the specified conditions are met**.

### 3. Arithmetic Operators
Let's Add 5 to the age of all users in `users` collection

``` javascript
db.users.updateMany({}, { $add: { age: 5 } })
```

Let's Subtract 2 from the age of users aged 30 in `users` collection

``` javascript
db.users.updateMany({ age: 30 }, { $subtract: { age: 2 } })
```

Let's Multiply the age of users by 2 in `users` collection

``` javascript
db.users.updateMany({}, { $multiply: { age: 2 } })
```

Let's Divide the age of all users by 2 in `users` collection

``` javascript
db.users.updateMany({}, { $divide: { age: 2 } })
```

Let's Calculate the absolute value of the age of all users in `users` collection

``` javascript
db.users.updateMany({}, { $abs: { age: true } })
```

> We use the `$add`, `$subtract`, `$multiply` and `$divide` operators to perform **addition**, **subtraction**, **multiplication** and **division** respectively on numeric fields. <br> The `$abs` operator calculates the **absolute value** of numeric fields.

### 4. Field Update Operators
Let's Update the age of users to the maximum value of 40 in `users` collection

``` javascript
db.users.updateMany({}, { $max: { age: 40 } })
```

Let's Update the age of users to the minimum value of 20 in `users` collection

``` javascript
db.users.updateMany({}, { $min: { age: 20 } })
```

Let's Increment the age of users by 1 in `users` collection

``` javascript
db.users.updateMany({}, { $inc: { age: 1 } })
```

Let's Multiply the age of users by 1.1 in `users` collection

``` javascript
db.users.updateMany({}, { $mul: { age: 1.1 } })
```

> We use the `$max` and `$min` operators to update fields to the **maximum** or **minimum** value respectively. <br> The `$inc` operator **increments numeric fields** by a specified value. <br> The `$mul` operator **multiplies numeric fields** by a specified value.

### 5. Array Expression Operators
Let's Find documents where 'tags' field is an array in `posts` collection

``` javascript
db.posts.find({ tags: { $isArray: true } })
```

Let's Find documents in `posts` collection where the size of the 'tags' array is 3

``` javascript
db.posts.find({ $expr: { $eq: [{ $size: "$tags" }, 3] } })
```

Let's Find the first element of the 'tags' array in each document of `posts` collection

``` javascript
db.posts.aggregate([
    { $project: { firstTag: { $arrayElemAt: ["$tags", 0] } } }
])
```

Let's Concatenate the 'tags' arrays of all documents in `posts` collection

``` javascript
db.posts.aggregate([
    { $group: { _id: null, allTags: { $concatArrays: "$tags" } } }
])
```

Let's Reverse the 'tags' array in all documents of `posts` collection

``` javascript
db.posts.updateMany({}, { $reverseArray: "$tags" })
```

> We use the `$isArray` operator to find documents **where a field is an array**. <br> The `$size` operator is used to **find documents based on the size of an array field**. <br> With `$arrayElemAt`, we retrieve **a specific element** from an array field. <br> The `$concatArrays` operator **concatenates arrays**. <br> Finally, `$reverseArray` **reverses the elements** of an array.

### 6. Array Update Operators
Let's Remove all occurrences of "mongodb" from the 'tags' array in `posts` collection

``` javascript
db.posts.updateMany({}, { $pull: { tags: "mongodb" } })
```

Let's Remove the last element from the 'tags' array in all documents of `posts` collection

``` javascript
db.posts.updateMany({}, { $pop: { tags: 1 } })
```

Let's Remove all occurrences of "nosql" and "database" from the 'tags' array in `posts` collection

``` javascript
db.posts.updateMany({}, { $pullAll: { tags: ["nosql", "database"] } })
```

Let's Add "newtag" to the end of the 'tags' array in a specific document in `posts` collection

``` javascript
db.posts.updateOne({ title: "Introduction to MongoDB" }, { $push: { tags: "newtag" } })
```

Let's Update the 'tags' array in all documents where "mongodb" is present with "updatedtag"

``` javascript
db.posts.updateMany({ tags: "mongodb" }, { $set: { "tags.$": "updatedtag" } })
```

### 7. String Expression Operators
Concatenate the 'title' and 'content' fields into a new field 'fullText' in `posts` collection

``` javascript
db.posts.aggregate([
    {
        $project: {
            fullText: { $concat: ["$title", " ", "$content"] }
        }
    }
])
```

Let's Compare the 'title' field case insensitively to "MongoDB" in `posts` collection

``` javascript
db.posts.find({ $expr: { $eq: [{ $strcasecmp: ["$title", "MongoDB"] }, 0] } })
```

Let's Convert the 'title' field to uppercase in `posts` collection

``` javascript
db.posts.updateMany({}, { $set: { title: { $toUpper: "$title" } } })
```

Let's Convert the 'title' field to lowercase in `posts` collection

``` javascript
db.posts.updateMany({}, { $set: { title: { $toLower: "$title" } } })
```

Let's Extract the first 5 characters from the 'title' field in `posts` collection

``` javascript
db.posts.aggregate([
    { $project: { firstFiveChars: { $substrCP: ["$title", 0, 5] } } }
])
```

> We use the `$concat` operator to **concatenate fields or strings**. <br> `$strcasecmp` compares **strings case insensitive**. <br> The `$toUpper` operator converts a string to **uppercase**. <br> `$toLower` converts a string to **lowercase**. <br> `$substrCP` extracts a substring from **a string based on code points**.
