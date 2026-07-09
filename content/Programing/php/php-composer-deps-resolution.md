---
title: Dependency Resolution Composer
tags:
  - programming
  - php
---
# How Composer Maps Files → Classes → Namespaces

Composer does not “scan files randomly”. It uses **autoload rules (usually PSR-4)** to map:

> Namespace → Folder path → PHP file → Class name

---

## 📦 PSR-4 Autoloading Rule

In `composer.json`:

```json
{
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

### 👉 Meaning:

- `App\` → root namespace
- `src/` → folder where code lives

So:

```
App\Foo\Bar → src/Foo/Bar.php
```

---

# The Core Mapping Rule

## 1. Namespace = folder structure

```
Namespace: App\Service\UserService
```

Becomes:

```
src/Service/UserService.php
```

---

## 2. Class name must match file name

Inside file:

```php
<?php

namespace App\Service;

class UserService
{}
```

👉 File MUST be:

```
UserService.php
```

---

## 3. Full resolution rule

Composer resolves like this:

```
App\X\Y\Z
↓
src/X/Y/Z.php
↓
class Z inside file
```

---

#  Concrete Example

## composer.json

```json
{
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

---

## File structure

```
project/
 ├── src/
 │    └── Controller/
 │         └── HomeController.php
 ├── vendor/
 └── composer.json
```

---

## File content

```php
<?php

namespace App\Controller;

class HomeController
{
    public function index()
    {
        return "Hello";
    }
}
```

---

## Usage in code

```php
require __DIR__ . '/vendor/autoload.php';

use App\Controller\HomeController;

$controller = new HomeController();
echo $controller->index();
```

---

# ⚠️ Common mistakes

### ❌ Namespace mismatch

```php
namespace App\Controllers; // wrong folder expectation
```

But file is:

```
App/Controller/HomeController.php
```

👉 This breaks autoloading.

---

### ❌ Wrong file name

```
class HomeController → Home.php ❌
```

Composer won’t find it.

---

### ❌ Forgetting dump-autoload

After changing autoload config:

```bash
composer dump-autoload
```

---

# When Composer “knows” your classes

Composer builds a map inside:

```
vendor/composer/autoload_psr4.php
```

This is why `vendor/autoload.php` can resolve everything instantly.

---

# Mental model (important)

Think of Composer autoload like:

> “A router for PHP classes”

```
Namespace → Route
Folder → Controller group
File → Endpoint handler
Class → Functionality
```