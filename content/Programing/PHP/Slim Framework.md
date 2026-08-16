---
tags:
  - php
  - programming
  - http
  - web
  - framework
title: The Slim Framework
---
# Slim Framework

---

# What is Slim?

**Slim** is a lightweight PHP micro-framework designed for building:

- REST APIs
    
- Web applications
    
- Microservices
    
- Backend services

Unlike Laravel or Symfony, Slim provides **routing and HTTP handling** without imposing a large project structure.

Think of it as:

```text
PHP
    +
Router
    +
Middleware
    +
PSR Standards
```

You choose the rest (ORM, template engine, authentication, logging, etc.).

---

# Why Use Slim?

✅ Lightweight

✅ Fast

✅ PSR compliant

✅ Excellent for APIs

✅ Easy to understand

✅ Composer-based

Unlike larger frameworks, Slim doesn't force you to use:

- Eloquent
    
- Twig
    
- Doctrine
    
- Blade
    

You only install what you need.

---

# Installation

Create a project

```bash
mkdir my-api

cd my-api

composer init
```

Install Slim

```bash
composer require slim/slim:^4
```

Install a PSR-7 implementation

```bash
composer require slim/psr7
```

A typical project also installs a DI container:

```bash
composer require php-di/php-di
```

---

# Typical Project Layout

```text
my-api/

app/
    Controllers/
    Middleware/
    Services/

config/

public/
    index.php
    .htaccess

vendor/

composer.json
```

---

# Entry Point

Everything begins in

```text
public/index.php
```

Example

```php
<?php

declare(strict_types=1);

use Slim\Factory\AppFactory;

require __DIR__ . '/../vendor/autoload.php';

$app = AppFactory::create();

$app->run();
```

---

# The Request Lifecycle

```text
Browser

    │

Apache / Nginx

    │

public/index.php

    │

Slim App

    │

Middleware

    │

Router

    │

Route Callback

    │

Response

    │

Browser
```

---

# Hello World

```php
use Psr\Http\Message\ResponseInterface;
use Psr\Http\Message\ServerRequestInterface;

$app->get("/", function (
    ServerRequestInterface $request,
    ResponseInterface $response
) {
    $response->getBody()->write("Hello World");

    return $response;
});

$app->run();
```

---

# Routes

GET

```php
$app->get("/users", UserController::class . ":index");
```

POST

```php
$app->post("/users", UserController::class . ":store");
```

PUT

```php
$app->put("/users/{id}", UserController::class . ":update");
```

DELETE

```php
$app->delete("/users/{id}", UserController::class . ":destroy");
```

ANY

```php
$app->any("/debug", function (...) {});
```

---

# Route Parameters

```php
$app->get("/users/{id}", function ($request, $response, $args) {

    $id = $args["id"];

    return $response;
});
```

URL

```text
/users/42
```

Produces

```text
$args["id"] == 42
```

---

# Reading Query Parameters

```
GET /users?page=2
```

```php
$params = $request->getQueryParams();

$page = $params["page"] ?? 1;
```

---

# Reading JSON

Client

```json
{
    "name":"Cat"
}
```

Server

```php
$data = json_decode(
    (string)$request->getBody(),
    true
);

$name = $data["name"];
```

---

# Returning JSON

```php
$data = [
    "message" => "Hello",
];

$response->getBody()->write(
    json_encode($data)
);

return $response
    ->withHeader("Content-Type", "application/json");
```

---

# Status Codes

```php
return $response->withStatus(404);
```

or

```php
return $response->withStatus(201);
```

Common codes

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

# Controllers

Instead of huge route closures.

```php
$app->get("/users", UserController::class . ":index");
```

Controller

```php
class UserController
{
    public function index($request, $response)
    {
        $response->getBody()->write("Users");

        return $response;
    }
}
```

---

# Middleware

Middleware executes **before and/or after** a route.

```text
Request

↓

Authentication

↓

Logging

↓

CORS

↓

Route

↓

Response
```

Example

```php
$app->add(function ($request, $handler) {

    $response = $handler->handle($request);

    return $response;
});
```

Common middleware

- Authentication
    
- Logging
    
- CORS
    
- Rate limiting
    
- Sessions
    
- Error handling
    

---

# Route Groups

```php
$app->group("/api", function ($group) {

    $group->get("/users", ...);

    $group->post("/users", ...);

});
```

Produces

```text
/api/users
```

---

# Dependency Injection

Instead of

```php
$userService = new UserService();
```

Slim commonly uses a DI container.

```php
$container->set(UserService::class, function () {

    return new UserService();

});
```

Controllers then receive dependencies through constructor injection.

---

# Error Handling

```php
$errorMiddleware = $app->addErrorMiddleware(
    true,
    true,
    true
);
```

Useful during development.

Disable detailed errors in production.

---

# PSR Standards

Slim follows PHP-FIG standards.

|Standard|Purpose|
|---|---|
|PSR-3|Logging|
|PSR-4|Autoloading|
|PSR-7|HTTP Messages|
|PSR-11|Dependency Injection|
|PSR-15|Middleware|

One of Slim's greatest strengths is that its components interoperate cleanly with other PSR-compliant libraries.

---

# Common Packages

```bash
composer require slim/slim
composer require slim/psr7
composer require php-di/php-di
composer require vlucas/phpdotenv
composer require monolog/monolog
```

Optional additions

- Twig (templating)
    
- Doctrine ORM
    
- Eloquent ORM
    
- PHPUnit
    
- PHPStan
    

---

# Typical Request Flow

```text
GET /users/42

        │

Apache

        │

public/index.php

        │

Slim App

        │

Middleware

        │

Router

        │

UserController::show()

        │

UserService

        │

Repository

        │

Database

        │

JSON Response
```

---

# Advantages

- Very lightweight
    
- Fast startup time
    
- Excellent for REST APIs
    
- Doesn't force an architecture
    
- Built around PSR standards
    
- Easy to integrate with existing projects
    
- Composer ecosystem
    

---

# Limitations

- Fewer built-in features than Laravel or Symfony
    
- You choose and configure many components yourself
    
- Less "convention over configuration," which means a bit more setup for larger applications
    

---

# Best Practices

- Use **`public/`** as the web root.
    
- Keep routes thin; put business logic in services.
    
- Return JSON consistently for APIs.
    
- Use middleware for cross-cutting concerns (authentication, logging, CORS).
    
- Enable detailed errors only in development.
    
- Organize code with PSR-4 namespaces and Composer autoloading.
    
- Use dependency injection instead of manually creating services.
    
- Keep controllers focused on HTTP concerns and delegate business logic to dedicated service classes.
    

Slim is an excellent choice when you want the flexibility of plain PHP with modern HTTP abstractions, without the weight and conventions of a full-stack framework.