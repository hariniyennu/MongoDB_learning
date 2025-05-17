## 🔍 1️⃣ Indexing & Search
MongoDB uses indexes to make queries faster, similar to the way a book index allows you to quickly find information instead of reading every page.

Atlas Search, powered by Apache Lucene, extends the capabilities of traditional MongoDB indexes with full-text search.

### ✅ Creating an Index:
1. Go to your MongoDB Atlas Dashboard.
2. Click your Cluster name → Search tab.
3. Click Create Search Index.
4. Choose the Database and Collection (e.g., sample_mflix → movies).
5. If you name your index "default", you don't have to specify it during querying.
6. Click Create Search Index and wait for it to complete.


### ✅ Querying with $search:
To use the search index, $search is used as the first stage in the aggregation pipeline.

Example: Searching for movies with "star wars" in the title:
```js
db.movies.aggregate([
  {
    $search: {
      index: "default", // optional if index is named "default"
      text: {
        query: "star wars",
        path: "title"
      },
    },
  },
  {
    $project: {
      title: 1,
      year: 1,
      _id: 0
    }
  }
])
```
💡 Explanation:
- $search: Searches for the string "star wars" in the title field.
- $project: Returns only the title and year fields in the result.

✅ Other Types of Search:
- Wildcard Search:
```javascript
db.movies.aggregate([
  {
    $search: {
      text: {
        query: "star*",
        path: "title",
        fuzzy: {}
      }
    }
  }
])
```
- Phrase Search:
```javascript
db.movies.aggregate([
  {
    $search: {
      text: {
        query: "\"star wars\"",
        path: "title"
      }
    }
  }
])
```
## 🗂️ 2️⃣ Schema Validation
By default, MongoDB is schema-less, meaning documents can have any structure.

However, you can enforce structure using JSON Schema Validation during collection creation.

✅ Example:
Creating a collection with schema validation:
```javascript
db.createCollection("posts", {
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["title", "body"],
      properties: {
        title: {
          bsonType: "string",
          description: "Title of post - Required."
        },
        body: {
          bsonType: "string",
          description: "Body of post - Required."
        },
        category: {
          bsonType: "string",
          description: "Category of post - Optional."
        },
        likes: {
          bsonType: "int",
          description: "Post like count. Must be an integer - Optional."
        },
        tags: {
          bsonType: ["string"],
          description: "Must be an array of strings - Optional."
        },
        date: {
          bsonType: "date",
          description: "Must be a date - Optional."
        }
      }
    }
  }
})
```
✅ Explanation:
- bsonType: Defines the data type for each field.
- required: Lists the mandatory fields (title, body).
- description: Provides additional info (not mandatory, but useful).

### ✅ Inserting Documents with Schema Validation:
If you try to insert a document that does not match the schema, MongoDB will reject it.
Example of a valid insertion:
```javascript
db.posts.insertOne({
  title: "My First Post",
  body: "This is the content of my post.",
  category: "News",
  likes: 10,
  tags: ["MongoDB", "Database"],
  date: new Date()
})
```
Example of an invalid insertion (missing "title"):
```javascript
db.posts.insertOne({
  body: "Content without a title.",
  category: "News"
})
```
💡 Error: Document fails schema validation because "title" is required.

### ✅ Modifying Schema Validation Rules:
You can also modify the schema after creation using the collMod command:
```javascript
db.runCommand({
  collMod: "posts",
  validator: {
    $jsonSchema: {
      bsonType: "object",
      required: ["title", "body", "category"],
      properties: {
        title: {
          bsonType: "string"
        },
        body: {
          bsonType: "string"
        },
        category: {
          bsonType: "string"
        }
      }
    }
  }
})
```
