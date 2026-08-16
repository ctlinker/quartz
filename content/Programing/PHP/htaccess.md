---
title: HTACCESS Cheatsheet
tags:
  - php
  - programming
  - cheatsheet
  - web
  - http
---
# `.htaccess` Cheatsheet

## What is `.htaccess`?

A `.htaccess` file is a **per-directory Apache configuration file**.

It lets you configure things like:

- URL rewriting
- Redirects
- Authentication
- Access control
- MIME types
- Caching 
- Compression    
- Error pages

Unlike `apache2.conf`, changes take effect immediately—no server restart required.

---

# Comments

```apache
# This is a comment
```

---

# Redirects

## Permanent Redirect (301)

```apache
Redirect 301 /old-page /new-page
```

Example:

```apache
Redirect 301 /about.html /about
```

---

## Temporary Redirect (302)

```apache
Redirect 302 /beta /new-beta
```

---

# Rewrite Engine

Most frameworks (Laravel, Symfony, Slim, etc.) use `mod_rewrite`.

Enable it:

```apache
RewriteEngine On
```

---

## Rewrite a URL

```
/user/42
↓

index.php?id=42
```

```apache
RewriteRule ^user/([0-9]+)$ index.php?id=$1 [L,QSA]
```

Meaning:

```
^            start
user/        literal
([0-9]+)     capture number
$            end
```

`$1`

means

```
first captured group
```

---

## Rewrite everything to index.php

Very common.

```apache
RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

RewriteRule ^ index.php [L]
```

Meaning:

If requested path is

- not a file
- not a directory

then serve

```
index.php
```

Perfect for routing.

---

# Rewrite Conditions

## HTTPS

Redirect HTTP → HTTPS

```apache
RewriteEngine On

RewriteCond %{HTTPS} off
RewriteRule ^ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

---

## Redirect www

```
www.example.com
↓

example.com
```

```apache
RewriteEngine On

RewriteCond %{HTTP_HOST} ^www\.(.*)$ [NC]
RewriteRule ^ https://%1%{REQUEST_URI} [R=301,L]
```

---

# Common Flags

|Flag|Meaning|
|---|---|
|L|Last rule|
|R|Redirect|
|R=301|Permanent redirect|
|R=302|Temporary redirect|
|NC|Case-insensitive|
|QSA|Append query string|
|QSD|Discard query string|
|F|Forbidden (403)|
|G|Gone (410)|

Example

```apache
RewriteRule ^private - [F,L]
```

returns

```
403 Forbidden
```

---

# Custom Error Pages

```apache
ErrorDocument 404 /404.html
```

```apache
ErrorDocument 403 /403.html
```

```apache
ErrorDocument 500 /500.html
```

---

# Directory Index

Default page

```apache
DirectoryIndex index.php
```

or

```apache
DirectoryIndex index.html index.php
```

---

# Disable Directory Listing

Instead of showing

```
/images/
```

contents:

```
cat.jpg
dog.jpg
```

show

```
403 Forbidden
```

```apache
Options -Indexes
```

---

# Enable Directory Listing

```apache
Options +Indexes
```

---

# Password Protect Directory

```apache
AuthType Basic
AuthName "Restricted"

AuthUserFile /path/to/.htpasswd

Require valid-user
```

---

# Block an IP

```apache
Require not ip 192.168.1.5
```

or

```apache
Require ip 192.168.1.0/24
```

---

# Allow Only One IP

```apache
Require ip 10.0.0.5
```

---

# Deny Access to File

Example

```
.env
```

```apache
<Files ".env">
    Require all denied
</Files>
```

---

# Deny Multiple Files

```apache
<FilesMatch "\.(env|ini|log)$">
    Require all denied
</FilesMatch>
```

---

# MIME Types

Serve WebAssembly

```apache
AddType application/wasm .wasm
```

JSON

```apache
AddType application/json .json
```

---

# Compression (mod_deflate)

```apache
AddOutputFilterByType DEFLATE text/html
AddOutputFilterByType DEFLATE text/css
AddOutputFilterByType DEFLATE application/javascript
```

---

# Cache Headers

```apache
<IfModule mod_expires.c>

ExpiresActive On

ExpiresByType image/png "access plus 1 year"
ExpiresByType text/css "access plus 1 month"
ExpiresByType application/javascript "access plus 1 month"

</IfModule>
```

---

# Security Headers

```apache
Header always set X-Frame-Options SAMEORIGIN

Header always set X-Content-Type-Options nosniff

Header always set Referrer-Policy no-referrer
```

---

# Force Download

```apache
AddType application/octet-stream .zip
```

---

# Deny Access by User-Agent

```apache
RewriteEngine On

RewriteCond %{HTTP_USER_AGENT} BadBot [NC]
RewriteRule .* - [F,L]
```

---

# Environment Variables

```apache
SetEnv APP_ENV production
```

---

# Enable CORS

```apache
Header set Access-Control-Allow-Origin "*"
```

Specific origin

```apache
Header set Access-Control-Allow-Origin "https://example.com"
```

---

# Variables

|Variable|Meaning|
|---|---|
|`%{REQUEST_URI}`|Requested path|
|`%{REQUEST_FILENAME}`|Physical file path|
|`%{HTTP_HOST}`|Host name|
|`%{HTTPS}`|HTTPS status|
|`%{QUERY_STRING}`|Query string|
|`%{REMOTE_ADDR}`|Client IP|
|`%{HTTP_USER_AGENT}`|Browser/User-Agent|
|`%{REQUEST_METHOD}`|GET, POST, etc.|

---

# Regular Expression Examples

|Pattern|Matches|
|---|---|
|`^$`|Empty path|
|`^about$`|`/about`|
|`^user/[0-9]+$`|`/user/42`|
|`^blog/(.*)$`|Everything after `/blog/`|
|`\.(jpg\|png)$`|`.jpg` or `.png`|
|`([A-Za-z]+)`|Letters|
|`([0-9]+)`|Numbers|

---

# Typical Front Controller (`index.php`) Configuration

```apache
RewriteEngine On

# Don't rewrite existing files
RewriteCond %{REQUEST_FILENAME} !-f

# Don't rewrite existing directories
RewriteCond %{REQUEST_FILENAME} !-d

# Route everything else through index.php
RewriteRule ^ index.php [L,QSA]
```

This is the pattern used by many PHP frameworks: the web server serves static files directly, while all other requests are handed to `index.php`, which acts as the application's router.