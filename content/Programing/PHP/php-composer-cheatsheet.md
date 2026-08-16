---
title: Composer For PHP
tags:
  - cheatsheet
  - programming
  - php
---
# 📦 PHP Composer Cheatsheet

##  What is Composer?

Composer is the **dependency manager for PHP**. It handles libraries your project depends on and autoloading.

---

## Project Setup

### Initialize a project

```bash
composer init
```

Creates `composer.json`.

---

### Install dependencies

```bash
composer install
```

- Reads `composer.json`
- Creates `vendor/`
- Generates `composer.lock`

---

### Add a package

```bash
composer require vendor/package
```

Example:

```bash
composer require monolog/monolog
```

---

### Remove a package

```bash
composer remove vendor/package
```

---

## Update dependencies

### Update everything

```bash
composer update
```

### Update specific package

```bash
composer update vendor/package
```

> [!DANGER]
> `composer upate` `WILL` suppress your deps if it cannot solve environment requirement; 
> eg: deps require 'php >= 8.3' env as 8.1.

---

## 📦 Autoloading

### Enable autoload (PSR-4)

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

Then run:

```bash
composer dump-autoload
```

---

### Use autoload in PHP

```php
require __DIR__ . '/vendor/autoload.php';

use App\Service\UserService;
```

See [[php-composer-deps-resolution|Composer Dependency Resolver]] for more info.

---

# Common project structure

```
project/
 ├── src/
 ├── vendor/
 ├── composer.json
 ├── composer.lock
 └── index.php
```

---

# 🔍 Useful commands

## Show installed packages

```bash
composer show
```

## Show a specific package

```bash
composer show monolog/monolog
```

## Check outdated packages

```bash
composer outdated
```

## Validate composer.json

```bash
composer validate
```

## Clear cache

```bash
composer clear-cache
```

---

# ⚙️ Version constraints

|Syntax|Meaning|
|---|---|
|`^1.2`|Compatible with >=1.2 <2.0|
|`~1.2`|>=1.2 <1.3|
|`1.2.*`|any patch version|
|`>=1.2`|minimum version|
|`*`|any version|

---

# 📦 composer.json minimal example

```json
{
  "name": "my/project",
  "require": {
    "php": ">=8.1",
    "monolog/monolog": "^3.0"
  },
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  }
}
```

---

# Pro tips

- Always commit `composer.lock` (important for reproducibility)
- Run `composer install` in production, not `update`
- Use `composer dump-autoload -o` for optimized autoloading
- Prefer `^` over exact versions unless necessary