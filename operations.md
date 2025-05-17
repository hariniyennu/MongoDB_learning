## 🗂️ 1. Collection Creation
A Collection in MongoDB is like a table in SQL, but it gets created only when you insert data. You can explicitly create it or let MongoDB do it automatically.
- Method 1: Explicit Creation
```js
db.createCollection("posts");
```
- Method 2: Implicit Creation during Insert
If the collection doesn't exist, it gets created automatically:
```js
db.posts.insertOne({
  title: "First Post",
  content: "This is the content of the first post."
});
```

## ✏️ 2. Inserting Documents
A Document is a record in MongoDB, stored in BSON format (like JSON).
- Method 1: Insert a Single Document
```js
db.posts.insertOne({
  title: "Introduction to MongoDB",
  category: "Database",
  tags: ["MongoDB", "Database", "NoSQL"],
  date: new Date()
});
```
- Method 2: Insert Multiple Documents
```js
db.posts.insertMany([
  {
    title: "Post Title 2",
    category: "Event",
    tags: ["Events", "News"],
    date: new Date()
  },
  {
    title: "Post Title 3",
    category: "Technology",
    tags: ["Tech", "Innovation"],
    date: new Date()
  }
]);
```
## 🔍 3. Finding Documents
To retrieve data, you use find() and findOne().

Find All Documents:
```js
db.posts.find();
```
Find One Document:
```js
db.posts.findOne();
```
Filter by Field:
```js
db.posts.find({ category: "Technology" });
```
## 🔎 4. Projection (Selecting Specific Fields)
You can control which fields are returned by using Projections.

Syntax: { field_name: 1 } to include, { field_name: 0 } to exclude.

Include Only Title and Date:
```js
db.posts.find({}, { title: 1, date: 1 });
```
Exclude _id from the Result:
```js
db.posts.find({}, { _id: 0, title: 1, date: 1 });
```
Exclude a Specific Field:
```js
db.posts.find({}, { category: 0 });
```

## 🔥 Update Operations
In MongoDB, you can update documents using two main methods:
1. updateOne() - Updates the first matching document.
2. updateMany() - Updates all matching documents

### 1️⃣ updateOne()
The updateOne() method updates the first document that matches the query filter.

It accepts two parameters:
- The query object to specify the document.
- The update object with the modifications.

Example 1: Update the "likes" of "Post Title 1" to 2.
```js
db.posts.updateOne(
  { title: "Post Title 1" },        // Query: Find the document with this title
  { $set: { likes: 2 } }            // Update: Set the likes to 2
);
```
Example 2: If the document is not found, insert it using upsert.
```js
db.posts.updateOne(
  { title: "Post Title 5" },        // Query: Find Post Title 5
  {
    $set: {
      title: "Post Title 5",
      body: "Body of the post.",
      category: "Event",
      likes: 5,
      tags: ["news", "events"],
      date: Date()
    }
  },
  { upsert: true }                  // If not found, insert it
);
```
- upsert: true makes MongoDB insert the document if it is not found.

### 2️⃣ updateMany()
The updateMany() method updates all documents that match the filter.
- Use this if you want to mass-update multiple documents.
Example: Increase the likes count of all documents by 1.
```js
db.posts.updateMany(
  {},                       // Query: Empty, so it matches all documents
  { $inc: { likes: 1 } }    // Update: Increment likes by 1
);
```
- $inc is an increment operator that adds the specified value to the field.

## 🗑️ Delete Operations
In MongoDB, documents can be removed from the database using:
1. deleteOne() - Deletes the first matching document.
2. deleteMany() - Deletes all matching documents.

### 1️⃣ deleteOne()
The deleteOne() method deletes the first document that matches the query.

Example: Delete the document with the title "Post Title 5".
```js
db.posts.deleteOne({ title: "Post Title 5" });
```
- Only the first matching document is deleted, even if there are multiple matches.

### 2️⃣ deleteMany()
The deleteMany() method deletes all documents that match the query.

Example: Delete all posts under the "Technology" category.
```js
db.posts.deleteMany({ category: "Technology" });
```
- If multiple documents match the filter, all of them are removed.

## 🚀 Summary of CRUD Operations:
| Operation  | Method                         | Purpose                                |
| ---------- | ------------------------------ | -------------------------------------- |
| **Create** | `insertOne()` / `insertMany()` | Insert new documents                   |
| **Read**   | `find()` / `findOne()`         | Retrieve documents from the collection |
| **Update** | `updateOne()` / `updateMany()` | Modify existing documents              |
| **Delete** | `deleteOne()` / `deleteMany()` | Remove documents from the collection   |
