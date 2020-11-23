# Node js / Express js

Node js: a JavaScript Runtime

- Non-Blocking I/O calls on a single thread (asynchronous)
- Best for non-CPU intensive projects (REST API, Microservices, Real Time Services, CRUD Apps, Tools, etc.)
  Core Modules:

\*modules: files that have an export

Quickstart

```
mkdir app
cd app
npm init
npm install express --save
```

With MongoDB and mongoose
server.js

```
// Load Packages
const express = require("express");
const mongoose = require("mongoose");
const cors = require("cors");
const bodyParser = require("body-parser");

// Create Express Application
const app = express();
// Use environment defined port or 8080
const PORT = process.env.PORT || 8080;

// Allow CORS so that backend and frontend can be put on different servers
app.use(cors());
// body-parse middleware for JSON format
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// Connect to MongoDB
mongoose
  .connect(process.env.DATABASE_URL || "mongodb://127.0.0.1:27017/", {
    useNewUrlParser: true,
    useUnifiedTopology: true,
  })
  .then(() => console.log("MongoDB Connected."))
  .catch((err) => console.log(err));
//Define Routes
const usersRouter = require("./routes/users");
const wordsRouter = require("./routes/words");
app.use("/api/users", usersRouter);
app.use("/api/words", wordsRouter);

// Start Server
app.listen(PORT, () => {
  console.log("Server listening on port " + PORT);
});

```
