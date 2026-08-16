---
title: The Chi Framework
tags:
  - go
  - framework
  - programming
  - web
  - http
---
# Chi v5

---
# What is Chi?

**Chi** is a lightweight, idiomatic HTTP router for Go.

It is built on Go's standard **`net/http`** package and follows the philosophy of keeping things simple.

Think of it as

```text
Go
    +
net/http
    +
Powerful Router
    +
Middleware
```

Unlike larger frameworks, Chi **does not replace the standard library**—it extends it.

---

# Why Use Chi?

✅ Lightweight

✅ Fast

✅ Idiomatic Go

✅ Middleware support

✅ Nested routing

✅ URL parameters

✅ REST friendly

✅ Built on `net/http`

---

# Installation

```bash
go get github.com/go-chi/chi/v5
```

Optional middleware package

```bash
go get github.com/go-chi/chi/v5/middleware
```

---

# Minimal Server

```go
package main

import (
    "net/http"

    "github.com/go-chi/chi/v5"
)

func main() {
    r := chi.NewRouter()

    r.Get("/", func(w http.ResponseWriter, r *http.Request) {
        w.Write([]byte("Hello World"))
    })

    http.ListenAndServe(":8080", r)
}
```

---

# Request Lifecycle

```text
Client

    │

net/http

    │

Chi Router

    │

Middleware

    │

Handler

    │

Response
```

---

# Router Creation

```go
r := chi.NewRouter()
```

The router implements

```go
http.Handler
```

so it can be passed directly to

```go
http.ListenAndServe()
```

---

# HTTP Methods

```go
r.Get("/", handler)

r.Post("/", handler)

r.Put("/", handler)

r.Patch("/", handler)

r.Delete("/", handler)

r.Head("/", handler)

r.Options("/", handler)
```

---

# Handler Function

```go
func handler(w http.ResponseWriter, r *http.Request) {

}
```

Parameters

|Parameter|Purpose|
|---|---|
|`http.ResponseWriter`|Sends the response|
|`*http.Request`|Incoming request|

---

# Writing Responses

Plain text

```go
w.Write([]byte("Hello"))
```

Status code

```go
w.WriteHeader(http.StatusCreated)
```

Headers

```go
w.Header().Set("Content-Type", "application/json")
```

JSON

```go
json.NewEncoder(w).Encode(data)
```

---

# Route Parameters

```go
r.Get("/users/{id}", handler)
```

Retrieve parameter

```go
id := chi.URLParam(r, "id")
```

Request

```text
/users/42
```

Result

```text
id == "42"
```

---

# Query Parameters

```
GET /users?page=2
```

```go
page := r.URL.Query().Get("page")
```

---

# Reading JSON

```go
type User struct {
    Name string `json:"name"`
}

var user User

err := json.NewDecoder(r.Body).Decode(&user)
```

Always close request bodies if you've replaced or wrapped them, though the server normally handles the original body.

---

# Returning JSON

```go
w.Header().Set("Content-Type", "application/json")

json.NewEncoder(w).Encode(user)
```

---

# Route Groups

```go
r.Route("/api", func(r chi.Router) {

    r.Get("/users", users)

    r.Post("/users", createUser)

})
```

Produces

```text
/api/users
```

---

# Nested Routes

```go
r.Route("/users", func(r chi.Router) {

    r.Get("/", list)

    r.Post("/", create)

    r.Route("/{id}", func(r chi.Router) {

        r.Get("/", show)

        r.Put("/", update)

        r.Delete("/", remove)

    })

})
```

---

# Mounting Routers

Split large applications.

```go
r.Mount("/api", apiRouter())

r.Mount("/admin", adminRouter())
```

---

# Middleware

Middleware runs before and/or after handlers.

```text
Request

↓

Logger

↓

Recovery

↓

Authentication

↓

Handler

↓

Response
```

---

# Using Middleware

```go
r.Use(middleware.Logger)

r.Use(middleware.Recoverer)
```

Multiple middleware

```go
r.Use(
    middleware.Logger,
    middleware.Recoverer,
)
```

---

# Built-in Middleware

```go
middleware.Logger

middleware.Recoverer

middleware.Timeout

middleware.RealIP

middleware.RequestID

middleware.Compress

middleware.Heartbeat
```

Example

```go
r.Use(middleware.Timeout(30 * time.Second))
```

---

# Per-Route Middleware

```go
r.With(AuthMiddleware).
    Get("/admin", adminHandler)
```

---

# Middleware Groups

```go
r.Group(func(r chi.Router) {

    r.Use(AuthMiddleware)

    r.Get("/profile", profile)

})
```

---

# URL Patterns

```text
/users

/users/{id}

/articles/{slug}

/static/*
```

Catch-all

```go
r.Get("/files/*", handler)
```

---

# Serving Static Files

```go
fs := http.FileServer(http.Dir("./public"))

r.Handle("/static/*", http.StripPrefix("/static/", fs))
```

---

# Not Found Handler

```go
r.NotFound(func(w http.ResponseWriter, r *http.Request) {

    http.Error(w, "Not Found", http.StatusNotFound)

})
```

---

# Method Not Allowed

```go
r.MethodNotAllowed(func(w http.ResponseWriter, r *http.Request) {

    http.Error(w, "Method Not Allowed", http.StatusMethodNotAllowed)

})
```

---

# Context

Store values in request context.

```go
ctx := context.WithValue(
    r.Context(),
    "user",
    user,
)

r = r.WithContext(ctx)
```

Retrieve

```go
user := r.Context().Value("user")
```

> **Prefer using custom typed keys instead of strings** to avoid collisions.

---

# Typical Project Layout

```text
my-api/

cmd/
    api/
        main.go

internal/
    handlers/
    middleware/
    services/
    repository/

pkg/

public/

go.mod

go.sum
```

---

# Typical Request Flow

```text
Client

        │

net/http

        │

Chi Router

        │

Middleware

        │

Handler

        │

Service

        │

Repository

        │

Database

        │

JSON Response
```

---

# Common Status Codes

|Code|Meaning|
|--:|---|
|200|OK|
|201|Created|
|204|No Content|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|500|Internal Server Error|

---

# Best Practices

- Build on `net/http` instead of abstracting it away.
    
- Keep handlers focused on HTTP concerns.
    
- Move business logic into services.
    
- Return JSON consistently for APIs.
    
- Use middleware for authentication, logging, recovery, CORS, and request timeouts.
    
- Group related routes with `Route()` and split large applications with `Mount()`.
    
- Use typed context keys instead of string keys.
    
- Prefer `json.NewEncoder()` and `json.NewDecoder()` over manual marshaling when writing directly to `http.ResponseWriter` or reading from `r.Body`.
    
- Organize packages following Go conventions (`cmd/`, `internal/`, `pkg/`).
    

---

# Chi vs Slim

|Feature|Chi v5|Slim 4|
|---|---|---|
|Language|Go|PHP|
|Foundation|`net/http`|PSR-7 / PSR-15|
|Router|Built-in|Built-in|
|Middleware|Yes|Yes|
|Dependency Injection|Optional|Optional|
|Performance|Very High|High|
|Primary Use|APIs, web services, microservices|APIs, web applications, microservices|

Chi embraces Go's philosophy: small abstractions, explicit code, and maximum compatibility with the standard library. If you already know `net/http`, learning Chi is mostly about gaining a richer router and a clean middleware pipeline rather than learning an entirely new framework.