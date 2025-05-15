## You have two options to set up MongoDB:

1. MongoDB Atlas (Cloud-based)
- MongoDB Atlas is a cloud-based solution provided by MongoDB for easy setup.
- It allows you to create clusters and manage your database online.
  Steps to Setup MongoDB Atlas:
  1. Go to MongoDB Atlas.
  2. Sign up and create a new project.
  3. Create a free-tier cluster.
  4. Add a database user with username and password.
  5. Whitelist your IP address (or allow access from anywhere).
  6. Get the connection string (mongodb+srv://<username>:<password>@cluster0.mongodb.net/test?retryWrites=true&w=majority).

2. Local Installation
- If you prefer working offline, you can install MongoDB locally.
- Download MongoDB Community Edition.
- Follow the installation steps for your OS (Windows/Mac/Linux).
- After installation, start the MongoDB server with:

```bash
mongod
```
- Open a new terminal and connect to the server with:
```bash
mongo
```
