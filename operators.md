## 🔍 1️⃣ Query Operators
MongoDB provides powerful query operators to filter and search data.
They are grouped into three main categories:

### ✅ Comparison Operators:
- $eq: Matches values that are equal to a specified value.
```js
db.posts.find({ likes: { $eq: 2 } })
```
- $ne: Matches values that are not equal to a specified value.
```javascript
db.posts.find({ category: { $ne: "Technology" } })
```
- $gt: Matches values greater than a specified value.
```javascript
db.posts.find({ likes: { $gt: 5 } })
```
- $gte: Matches values greater than or equal to a specified value.
```javascript
db.posts.find({ likes: { $gte: 5 } })
```
- $lt: Matches values less than a specified value.
```javascript
db.posts.find({ likes: { $lt: 10 } })
```
- $lte: Matches values less than or equal to a specified value.
```javascript
db.posts.find({ likes: { $lte: 10 } })
```
- $in: Matches any of the values specified in an array.
```javascript
db.posts.find({ category: { $in: ["News", "Technology"] } })
```

### ✅ Logical Operators:
- $and: Matches documents where both conditions are true.
```javascript
db.posts.find({ $and: [{ category: "News" }, { likes: { $gt: 5 } }] })
```
- $or: Matches documents where at least one condition is true.
```javascript
db.posts.find({ $or: [{ category: "News" }, { likes: { $gt: 5 } }] })
```
- $nor: Matches documents where neither condition is true.
```javascript
db.posts.find({ $nor: [{ category: "News" }, { likes: { $lt: 5 } }] })
```
- $not: Matches documents where the condition is not true.
```javascript
db.posts.find({ likes: { $not: { $gt: 10 } } })
```

### ✅ Evaluation Operators:
- $regex: Search using regular expressions.
```javascript
db.posts.find({ title: { $regex: /Post/i } })
```
- $text: Performs a text search.
```javascript
db.posts.find({ $text: { $search: "MongoDB" } })
```
- $where: Execute JavaScript expressions to filter data.
```javascript
db.posts.find({ $where: "this.likes > 5" })
```

## 🔄 2️⃣ Update Operators
### ✅ Field Operators:
- $set: Update a value.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $set: { likes: 10 } })
```
- $inc: Increment a field by a specified amount.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $inc: { likes: 1 } })
```
- $rename: Rename a field.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $rename: { "likes": "upvotes" } })
```
- $unset: Remove a field from the document.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $unset: { body: "" } })
```
- $currentDate: Set the field to the current date.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $currentDate: { lastUpdated: true } })
```

### ✅ Array Operators:
- $addToSet: Add an element to an array if it does not exist.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $addToSet: { tags: "newTag" } })
```
- $push: Add an element to an array.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $push: { tags: "extraTag" } })
```
- $pull: Remove all instances of a value from an array.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $pull: { tags: "news" } })
```
- $pop: Remove the first (-1) or last (1) element from an array.
```javascript
db.posts.updateOne({ title: "Post Title 1" }, { $pop: { tags: -1 } })
```

## 🔄 3️⃣ Aggregation Pipelines
Aggregation allows you to process data and return computed results. It consists of multiple stages, each performing an operation on the data.

✅ Example:
Find all posts with more than 1 like and group by category:
```javascript
db.posts.aggregate([
  { $match: { likes: { $gt: 1 } } },            // Stage 1: Filter
  { $group: { _id: "$category", totalLikes: { $sum: "$likes" } } }   // Stage 2: Group and Sum
])
```
### ✅ Common Stages in Aggregation:
1. $match - Filters the documents.
2. $group - Groups documents by a specified key.
3. $sort - Sorts the documents.
4. $project - Reshapes each document by including/excluding fields.
5. $limit - Limits the number of documents.
6. $lookup - Joins documents from different collections.
7. $count - Counts the number of documents.
8. $addFields - Adds new fields to documents.

Example
```js
db.posts.aggregate([
  { $match: { category: "News" } },                // Step 1: Filter News
  { $sort: { likes: -1 } },                        // Step 2: Sort by likes descending
  { $project: { title: 1, likes: 1, _id: 0 } },    // Step 3: Project only title and likes
  { $limit: 5 }                                    // Step 4: Limit to top 5
])
```
