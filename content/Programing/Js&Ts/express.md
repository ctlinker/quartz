---
title: The Express.js Framework
tags:
  - javascript
  - web
  - http
  - framework
---

# Express.js

---

# What is Express?

**Express.js** is a minimal and flexible web framework for **Node.js**.

It provides:

- HTTP server abstraction
    
- Routing
    
- Middleware pipeline
    
- Request/response helpers
    
- API building tools

Express is built on top of Node's native:

```text
Node.js

    +

http module

    +

Express Router

    +

Middleware
```

---

# Why Use Express?

✅ Simple API

✅ Huge ecosystem

✅ Easy REST API development

✅ Flexible architecture

✅ Works well with JavaScript / TypeScript

✅ Large community

Unlike opinionated frameworks like NestJS, Express does not force:

- project structure
    
- database choice
    
- ORM
    
- authentication system
    
- validation library

You assemble your stack yourself.

---

# Installation

Create project:

```bash
mkdir my-api
cd my-api

npm init -y
```

Install Express:

```bash
npm install express
```

TypeScript setup:

```bash
npm install -D typescript ts-node @types/node @types/express
```

---

# Minimal Server

`index.js`

```javascript
const express = require("express");

const app = express();

app.get("/", (req, res) => {
    res.send("Hello World");
});

app.listen(3000, () => {
    console.log("Server running on port 3000");
});
```

Run:

```bash
node index.js
```

---

# Request Lifecycle

```text
Client

   │

Node HTTP Server

   │

Express Application

   │

Middleware Stack

   │

Router

   │

Controller

   │

Response

```

---

# Express Application

Create an app:

```javascript
const app = express();
```

The app handles:

- routes
    
- middleware
    
- configuration
    
- server lifecycle
    

---

# Middleware

Middleware is a function executed during the request lifecycle.

```text
Request

 ↓

Middleware 1

 ↓

Middleware 2

 ↓

Route Handler

 ↓

Response
```

Basic middleware:

```javascript
app.use((req, res, next) => {

    console.log(req.method);

    next();

});
```

`next()` passes control to the next middleware.

---

# Built-in Middleware

## JSON Parser

```javascript
app.use(express.json());
```

Allows:

```json
{
    "name": "Cat"
}
```

to become:

```javascript
req.body.name
```

---

## URL Encoded Forms

```javascript
app.use(
    express.urlencoded({
        extended: true
    })
);
```

Handles:

```html
<form>
```

data.

---

## Static Files

```javascript
app.use(
    express.static("public")
);
```

Example:

```text
public/
 ├── index.html
 ├── style.css
```

Available:

```text
/static/style.css
```

---

# Routes

## GET

```javascript
app.get("/users", (req, res) => {

    res.send("Users");

});
```

---

## POST

```javascript
app.post("/users", (req, res) => {

    const user = req.body;

    res.json(user);

});
```

---

## PUT

```javascript
app.put("/users/:id", (req, res) => {

});
```

---

## DELETE

```javascript
app.delete("/users/:id", (req, res) => {

});
```

---

# Route Parameters

Route:

```javascript
app.get(
    "/users/:id",
    (req, res) => {

        console.log(req.params.id);

    }
);
```

Request:

```text
/users/42
```

Result:

```javascript
req.params.id === "42"
```

---

# Query Parameters

Request:

```text
/users?page=2
```

Code:

```javascript
app.get("/users", (req,res)=>{

    const page = req.query.page;

});
```

Result:

```javascript
page === "2"
```

---

# JSON Response

```javascript
app.get("/api/user", (req,res)=>{

    res.json({
        id: 1,
        name: "Cat"
    });

});
```

Express automatically sets:

```http
Content-Type: application/json
```

---

# Response Methods

```javascript
res.send("text");

res.json(object);

res.status(404);

res.redirect("/login");

res.download(file);

res.end();
```

---

# Routers

Large applications should split routes.

Structure:

```text
src/

routes/
    users.js

controllers/
    users.js

index.js
```

---

Create router:

```javascript
const router = express.Router();

router.get("/", (req,res)=>{
    res.send("Users");
});

module.exports = router;
```

Mount:

```javascript
app.use(
    "/users",
    router
);
```

Result:

```text
GET /users
```

---

# Controllers

Routes should not contain business logic.

Bad:

```javascript
app.get("/users", async(req,res)=>{

    // database logic
    // validation
    // authentication

});
```

Better:

```text
Route

 ↓

Controller

 ↓

Service

 ↓

Database
```

Example:

```javascript
exports.listUsers = async(req,res)=>{

    const users = await userService.list();

    res.json(users);

};
```

---

# Services

Contain business logic.

```javascript
class UserService {

    async create(data){

        // validation
        // rules
        // database calls

    }

}
```

---

# Error Handling Middleware

Express errors use four parameters:

```javascript
app.use(
    (err, req, res, next)=>{

        console.error(err);

        res.status(500)
           .json({
                error:"Internal error"
           });

    }
);
```

---

# Async Errors

Common pattern:

```javascript
try {

    const data = await service();

    res.json(data);

}
catch(err){

    next(err);

}
```

---

# Authentication Middleware

Example:

```javascript
function auth(req,res,next){

    const token =
        req.headers.authorization;

    if(!token){

        return res.status(401).send();

    }

    next();
}
```

Use:

```javascript
app.get(
    "/profile",
    auth,
    profileController
);
```

---

# Environment Variables

Install:

```bash
npm install dotenv
```

`.env`

```env
PORT=3000

DB_HOST=localhost

JWT_SECRET=mysecret
```

Load:

```javascript
require("dotenv").config();

console.log(
    process.env.PORT
);
```

---

# Typical Project Layout

```text
my-api/

src/

├── index.js
│
├── routes/
│   └── users.js
│
├── controllers/
│   └── users.js
│
├── services/
│   └── users.js
│
├── middleware/
│   └── auth.js
│
├── models/
│
└── config/

package.json

package-lock.json

.env
```

---

# TypeScript Layout

```text
src/

├── app.ts
├── server.ts
│
├── routes/
├── controllers/
├── services/
├── middleware/
├── types/
└── utils/
```

---

# CORS

Install:

```bash
npm install cors
```

Use:

```javascript
const cors = require("cors");

app.use(cors());
```

Specific origin:

```javascript
app.use(cors({

    origin:"https://example.com"

}));
```

---

# Request Object

Common properties:

|Property|Purpose|
|---|---|
|`req.params`|URL parameters|
|`req.query`|Query string|
|`req.body`|Request body|
|`req.headers`|HTTP headers|
|`req.cookies`|Cookies|
|`req.method`|HTTP method|
|`req.path`|URL path|

---

# Response Object

Common methods:

|Method|Purpose|
|---|---|
|`res.send()`|Send text/HTML|
|`res.json()`|Send JSON|
|`res.status()`|Set status|
|`res.redirect()`|Redirect|
|`res.cookie()`|Set cookie|
|`res.clearCookie()`|Remove cookie|

---

# Common Packages

## Development

```bash
npm install -D nodemon
```

Automatic restart:

```bash
nodemon src/index.js
```

---

## Validation

```bash
npm install zod
```

or

```bash
npm install joi
```

---

## Authentication

```bash
npm install jsonwebtoken bcrypt
```

---

## Database

Examples:

```bash
npm install prisma
```

or

```bash
npm install mongoose
```

---

# Express vs [[Slim Framework|Slim]] vs [[chi|Chi]]

||Express|Slim|Chi|
|---|---|---|---|
|Language|JavaScript|PHP|Go|
|Runtime|Node.js|PHP|Go|
|Foundation|Node HTTP|PSR HTTP|net/http|
|Style|Middleware|Middleware|Middleware|
|Main Use|Web apps/API|Web/API|API/services|
|Ecosystem|Very large|PHP ecosystem|Go ecosystem|

---

# Best Practices

- Use `express.Router()` to split routes.
    
- Keep controllers thin.
    
- Put business logic in services.
    
- Validate all incoming data.
    
- Use environment variables for secrets.
    
- Add centralized error handling.
    
- Use async/await instead of nested callbacks.
    
- Add security middleware (`helmet`, CORS configuration, rate limiting).
    
- Separate configuration from application code.
    
- Use TypeScript for larger projects.
    

---

# Typical Express Request Flow

```text
Client

    │

Node.js HTTP Server

    │

Express App

    │

Global Middleware

    │

Router

    │

Controller

    │

Service

    │

Database

    │

JSON Response
```

Express is essentially the JavaScript equivalent of Chi or Slim: a thin HTTP layer that gives you routing and middleware while leaving architecture decisions to the developer.