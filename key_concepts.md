# ✅ Key Concepts of MongoDB
## 🔹 1️⃣ Documents:
- A Document is the basic unit of data in MongoDB, similar to a row in a SQL database.
- Documents are stored in BSON (Binary JSON) format, which is efficient for both storage and data retrieval.
- They support different types of data like strings, numbers, arrays, and even other documents (nested).
```js
{
  "_id": ObjectId("507f191e810c19729de860ea"),   // Unique ID for the document
  "name": "Harini",
  "age": 22,
  "skills": ["Python", "Flask", "Machine Learning"]
}
```
### 🔹 The _id field is automatically generated if you don't provide it, and it acts as the primary key.

## 🔹 2️⃣ Collections:
- A Collection is a group of documents, similar to a table in SQL.
- Unlike SQL tables, collections do not enforce schemas, which means documents in the same collection can have different structures.
Example:
If you create a collection named users, it can contain:
```js
// Document 1
{ 
  "name": "Harini", 
  "age": 22 
}

// Document 2
{ 
  "name": "Amit", 
  "age": 24, 
  "gender": "Male" 
}
```
### 🔹 Notice that Document 2 has an extra field called gender, but Document 1 does not. MongoDB allows this flexibility.

## 🔹 3️⃣ Databases:
- MongoDB organizes its data into Databases.
- A Database is a container for collections, and each collection holds documents.
- You can have multiple databases in a single MongoDB instance, just like you can have multiple databases in MySQL.

Example:
A database named StudentRecords can have different collections like:
- Students → stores all student information
- Courses → stores course details
- Exams → stores exam results

## Summary
| **Concept**     | **MongoDB**                | **SQL (Relational Database)**   |
| --------------- | -------------------------- | ------------------------------- |
| **Row**         | Document                   | Row                             |
| **Table**       | Collection                 | Table                           |
| **Database**    | Database                   | Database                        |
| **Schema**      | Dynamic and Flexible       | Strict and Predefined           |
| **Joins**       | Rarely used, embedded docs | Commonly used for relationships |
| **Scalability** | Horizontally scalable      | Vertically scalable             |
| **Storage**     | BSON (Binary JSON)         | Tabular format                  |

