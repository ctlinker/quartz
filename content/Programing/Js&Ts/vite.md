---
title: The Vite Framework
tags:
  - javascript
  - typescript
  - frontend
  - build-tool
  - web
---
# Vite

---

# What is Vite?

**Vite** is a modern frontend build tool created by Evan You and the Vue ecosystem.

It provides:

- Development server
    
- Hot Module Replacement (HMR)
    
- Production bundling
    
- Plugin system
    
- Environment variable handling
    
- Framework integrations


Vite is designed around **native ES Modules** during development.

Think:

```text
Source Code

    ↓

Vite Dev Server

    ↓

Browser ES Modules

    ↓

Production Build

    ↓

Optimized Assets
```

---

# Why Use Vite?

✅ Extremely fast startup

✅ Instant HMR

✅ Native ESM development

✅ Simple configuration

✅ Supports many frameworks

✅ Great TypeScript support

✅ Modern replacement for older bundlers like Webpack in many projects

---

# Supported Frameworks

Vite works with:

- Vanilla JavaScript
    
- TypeScript
    
- React
    
- Vue
    
- Svelte
    
- Solid
    
- Preact
    
- Lit


---

# Creating a Project

Using npm:

```bash
npm create vite@latest
```

Interactive setup:

```text
Project name:
Framework:
Variant:
```

Example:

```bash
npm create vite@latest my-app -- --template react-ts
```

Templates:

```text
vanilla
vanilla-ts

react
react-ts

vue
vue-ts

svelte
svelte-ts
```

---

# Project Layout

Typical Vite application:

```text
my-app/

├── public/
│   └── favicon.ico
│
├── src/
│   ├── main.ts
│   ├── App.tsx
│   ├── components/
│   └── assets/
│
├── index.html
│
├── vite.config.ts
├── package.json
├── tsconfig.json
└── node_modules/
```

---

# Entry Point

Unlike older tools, `index.html` is the entry point.

```text
Browser

   ↓

index.html

   ↓

src/main.ts

   ↓

Application
```

Example:

```html
<!doctype html>

<html>

<body>

<div id="root"></div>

<script type="module" src="/src/main.ts"></script>

</body>

</html>
```

---

# Application Entry

`src/main.ts`

```ts
import App from "./App.ts";

const app = new App();

app.mount("#root");
```

Framework examples differ.

React:

```tsx
import React from "react";
import ReactDOM from "react-dom/client";

import App from "./App";

ReactDOM
    .createRoot(
        document.getElementById("root")!
    )
    .render(<App />);
```

---

# Development Server

Install dependencies:

```bash
npm install
```

Start development:

```bash
npm run dev
```

Output:

```text
Local:

http://localhost:5173/
```

---

# package.json Scripts

Typical:

```json
{
    "scripts": {
        "dev": "vite",
        "build": "vite build",
        "preview": "vite preview"
    }
}
```

Commands:

Development:

```bash
npm run dev
```

Production build:

```bash
npm run build
```

Preview build:

```bash
npm run preview
```

---

# Hot Module Replacement (HMR)

Vite updates modules without refreshing the page.

Example:

```ts
console.log("Hello");
```

Change code:

```ts
console.log("Hello Vite");
```

Browser updates instantly.

---

# Assets

## Public Folder

Files inside:

```text
public/
```

are copied directly.

Example:

```text
public/logo.png
```

Access:

```html
<img src="/logo.png">
```

---

## src/assets

Processed by Vite.

Example:

```text
src/assets/logo.png
```

Import:

```ts
import logo from "./assets/logo.png";
```

---

# CSS

Import CSS:

```ts
import "./style.css";
```

Vite supports:

- CSS
    
- PostCSS
    
- CSS Modules
    
- preprocessors
    

---

# Environment Variables

Files:

```text
.env

.env.local

.env.production
```

Example:

```env
VITE_API_URL=https://api.example.com
```

Access:

```ts
console.log(
    import.meta.env.VITE_API_URL
);
```

Only variables starting with:

```text
VITE_
```

are exposed to client code.

---

# Vite Configuration

File:

```text
vite.config.ts
```

Example:

```ts
import { defineConfig } from "vite";

export default defineConfig({

    server:{
        port:3000
    }

});
```

---

# Path Aliases

Instead of:

```ts
import Button from "../../../components/Button";
```

Use:

```ts
import Button from "@/components/Button";
```

Configuration:

```ts
import path from "node:path";

export default defineConfig({

    resolve:{
        alias:{
            "@": path.resolve(__dirname,"src")
        }
    }

});
```

---

# Backend Proxy

Useful during development.

Frontend:

```text
localhost:5173
```

Backend:

```text
localhost:8080
```

Configuration:

```ts
export default defineConfig({

server:{
    proxy:{
        "/api":{
            target:"http://localhost:8080",
            changeOrigin:true
        }
    }
}

});
```

Now:

```ts
fetch("/api/users")
```

goes to:

```text
http://localhost:8080/api/users
```

---

# Production Build

Command:

```bash
npm run build
```

Creates:

```text
dist/

├── index.html
├── assets/
│   ├── app.js
│   └── style.css
```

This folder can be served by:

- Nginx
    
- Apache
    
- Go HTTP server
    
- Node server
    
- CDN
    

---

# Vite + Go Backend

Common architecture:

```text
Frontend

Vite
 |
 |
build
 |
 ↓
dist/


Backend

Go Chi / Fiber / Gin
 |
 ↓
API
```

Production:

```text
Browser

   ↓

Nginx

   ├── /      → Vite dist/
   |
   └── /api  → Go server
```

---

# Vite + PHP Backend

Example:

```text
project/

frontend/

    src/
    vite.config.ts


backend/

    public/
    index.php
```

Development:

```text
Vite
localhost:5173

        ↓

PHP API
localhost:8000
```

Production:

```text
Apache/Nginx

    ↓

PHP + dist/
```

---

# Plugins

Install:

```bash
npm install -D plugin-name
```

Example:

React:

```bash
npm install @vitejs/plugin-react
```

Config:

```ts
import react from "@vitejs/plugin-react";

export default defineConfig({

plugins:[
    react()
]

});
```

---

# TypeScript Support

Vite supports TS natively.

Example:

```ts
interface User {
    id:number;
    name:string;
}

const user:User = {
    id:1,
    name:"Cat"
};
```

Important:

Vite **transpiles** TypeScript but does not type-check by default.

Use:

```bash
npm run build
```

or:

```bash
tsc --noEmit
```

for checking.

---

# Common Folder Structure

Large application:

```text
src/

├── main.ts
├── App.tsx
│
├── components/
│
├── pages/
│
├── layouts/
│
├── hooks/
│
├── services/
│
├── api/
│
├── stores/
│
├── types/
│
└── utils/
```

---

# SPA Routing

Vite itself does not provide routing.

Use:

React:

```bash
npm install react-router-dom
```

Vue:

```bash
npm install vue-router
```

Example:

```text
/users/42
/settings
/dashboard
```

All routes eventually load:

```text
index.html
```

---

# Static Deployment

After:

```bash
npm run build
```

Deploy:

```text
dist/

index.html

assets/
```

Examples:

- GitHub Pages
    
- Netlify
    
- Cloudflare Pages
    
- Nginx
    
- Apache
    

---

# Vite vs Webpack

||Vite|Webpack|
|---|---|---|
|Dev Server|Native ESM|Bundle first|
|Startup|Very fast|Slower|
|Config|Simple|Complex|
|Ecosystem|Modern|Mature|
|Production|Rollup-based|Webpack bundling|

---

# Best Practices

- Keep source code inside `src/`.
    
- Use `public/` only for static files that do not need processing.
    
- Use environment variables for API URLs and configuration.
    
- Never expose secrets in `VITE_*` variables (they are public).
    
- Use TypeScript for larger projects.
    
- Split large applications by feature.
    
- Keep API calls separated from UI components.
    
- Use production builds (`npm run build`) before deployment.
    
- Configure backend proxies during development to avoid CORS issues.
    

---

# Typical Vite Workflow

```text
Create Project

      ↓

npm install

      ↓

npm run dev

      ↓

Develop with HMR

      ↓

npm run build

      ↓

Deploy dist/
```

Vite is essentially the frontend equivalent of lightweight backend tools like **Chi**, **Slim**, or **Express**: it provides the infrastructure and development workflow while leaving the application architecture to the developer.