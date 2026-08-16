---
title: PHP Cheatsheet
tags:
  - cheatsheet
  - php
  - programming
---
# PHP Cheatsheet

---

# 1. Variables & Types

PHP is **dynamically typed**, but modern PHP encourages **strict typing**.

```php
<?php

declare(strict_types=1);

$name = "Gemini";             // string
$age = 25;                    // int
$height = 1.82;               // float
$isDev = true;                // bool

$languages = ["PHP", "Go"];   // array
$nothing = null;              // null
```

## Scalar Types

```text
bool
int
float
string
```

## Compound Types

```text
array
object
callable
iterable
```

## Special Types

```text
mixed
null
void
never
```

---

# 2. Type Hinting

Modern PHP supports type declarations almost everywhere.

```php
function greet(string $name): string
{
    return "Hello $name";
}

function add(int $a, int $b): int
{
    return $a + $b;
}
```

Nullable types

```php
function findUser(int $id): ?User
{
    return null;
}
```

Union types

```php
function log(string|Stringable $msg): void
{
}
```

Mixed

```php
function dump(mixed $value): void
{
}
```

---

# 3. Classes

```php
class User
{
    public string $name;
    public int $age;

    public function __construct(string $name, int $age)
    {
        $this->name = $name;
        $this->age = $age;
    }
}
```

Constructor property promotion (PHP 8)

```php
class User
{
    public function __construct(
        public string $name,
        public int $age,
    ) {}
}
```

Readonly property

```php
class Config
{
    public function __construct(
        public readonly string $appName,
    ) {}
}
```

---

# 4. Visibility

```php
public
protected
private
```

```php
class Example
{
    public string $public;

    protected string $protected;

    private string $private;
}
```

---

# 5. Singleton Pattern

Useful for objects that should exist only once (database, configuration, logger).

```php
class Database
{
    private static ?Database $instance = null;

    private PDO $pdo;

    private function __construct()
    {
        $this->pdo = new PDO(
            "mysql:host=localhost;dbname=test",
            "user",
            "password"
        );
    }

    private function __clone() {}

    public function __wakeup()
    {
        throw new Exception("Cannot unserialize singleton.");
    }

    public static function instance(): Database
    {
        return self::$instance ??= new self();
    }

    public function connection(): PDO
    {
        return $this->pdo;
    }
}
```

Usage

```php
$db = Database::instance();
```

---

# 6. Superglobals

|Variable|Purpose|
|---|---|
|`$_GET`|URL query parameters|
|`$_POST`|POST form data|
|`$_REQUEST`|GET + POST + COOKIE|
|`$_FILES`|Uploaded files|
|`$_COOKIE`|Cookies|
|`$_SESSION`|Session storage|
|`$_SERVER`|Request/server information|
|`$_ENV`|Environment variables|
|`$GLOBALS`|Global variables|

Example

```php
$id = $_GET["id"] ?? null;

$email = $_POST["email"] ?? "";

$method = $_SERVER["REQUEST_METHOD"];
```

---

# 7. Sessions

Always start the session **before any output**.

## Start

```php
session_start();
```

or

```php
session_start([
    "cookie_lifetime" => 86400,
    "read_and_close" => false,
]);
```

---

## Write

```php
$_SESSION["user_id"] = 42;

$_SESSION["username"] = "Cat";

$_SESSION["admin"] = true;
```

---

## Read

```php
session_start();

if ($_SESSION["admin"] ?? false) {
    echo "Welcome!";
}
```

---

## Destroy

```php
session_start();

$_SESSION = [];

if (ini_get("session.use_cookies")) {
    $params = session_get_cookie_params();

    setcookie(
        session_name(),
        "",
        time() - 42000,
        $params["path"],
        $params["domain"],
        $params["secure"],
        $params["httponly"]
    );
}

session_destroy();
```

---

# 8. Arrays

```php
$colors = ["red", "green", "blue"];

$user = [
    "name" => "Cat",
    "age" => 24,
];
```

Access

```php
echo $colors[0];

echo $user["name"];
```

Loop

```php
foreach ($colors as $color) {
    echo $color;
}

foreach ($user as $key => $value) {
    echo "$key = $value";
}
```

---

# 9. Null Coalescing

```php
$username = $_GET["user"] ?? "Guest";
```

Equivalent to

```php
if (isset($_GET["user"])) {
    $username = $_GET["user"];
} else {
    $username = "Guest";
}
```

---

# 10. Nullsafe Operator

```php
$email = $user?->profile?->email;
```

Avoids

```php
if ($user && $user->profile) ...
```

---

# 11. Match Expression

```php
$status = match($code) {
    200 => "OK",
    404 => "Not Found",
    500 => "Server Error",
    default => "Unknown",
};
```

---

# 12. Exceptions

```php
try {
    doSomething();
}
catch (Exception $e) {
    echo $e->getMessage();
}
finally {
    cleanup();
}
```

Throw

```php
throw new RuntimeException("Something went wrong");
```

---

# 13. Common String Functions

```php
strlen($str)

trim($str)

strtolower($str)

strtoupper($str)

explode(",", $csv)

implode(",", $array)

str_replace("a", "b", $text)

sprintf("%d apples", 4)
```

---

# 14. Common Array Functions

```php
count($array)

array_keys($array)

array_values($array)

array_merge($a, $b)

array_map(...)

array_filter(...)

array_reduce(...)
```

---

# 15. Input Validation

Never trust user input.

Instead of

```php
$email = $_POST["email"];
```

Prefer

```php
$email = filter_input(
    INPUT_POST,
    "email",
    FILTER_VALIDATE_EMAIL
);
```

Integer

```php
$id = filter_input(
    INPUT_GET,
    "id",
    FILTER_VALIDATE_INT
);
```

---

# 16. Escaping Output

To prevent XSS

```php
echo htmlspecialchars(
    $username,
    ENT_QUOTES,
    "UTF-8"
);
```

Never print raw user input.

---

# 17. Include Files

```php
include "header.php";

require "config.php";

include_once "functions.php";

require_once "autoload.php";
```

- `include` → warning if missing, script continues.
    
- `require` → fatal error if missing.
    
- `*_once` → include only once.
    

---

# 18. Useful Magic Constants

```php
__FILE__

__DIR__

__LINE__

__FUNCTION__

__CLASS__

__METHOD__

__NAMESPACE__
```

---

# 19. Common Magic Methods

```php
__construct()

__destruct()

__invoke()

__toString()

__get()

__set()

__call()

__clone()

__sleep()

__wakeup()
```

---

# 20. Good Practices

- `declare(strict_types=1);` in every file.
    
- Prefer constructor property promotion.
    
- Use typed properties and return types.
    
- Validate all user input.
    
- Escape all HTML output.
    
- Use `require_once` for configuration and autoloaders.
    
- Prefer exceptions over returning `false`.
    
- Keep business logic out of templates.
    
- Use Composer for dependency management.
    
- Follow **PSR-12** coding style.