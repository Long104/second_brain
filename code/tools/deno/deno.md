---
date: 2024-10-24T00:00:00.000Z
tags:
  - deno
  - command
  - tool
hubs:
  - '[[]]'
urls:
  - null
---
# deno

- **Deno** is not a package manager. Deno is a **runtime** for JavaScript and TypeScript, similar to **Node.js**,
  but with some key **differences** and **modern** features.
  While Deno is designed to run JavaScript and TypeScript, it does not have a built-in package manager like **npm** (which is used by Node.js).:
  - **Module Imports**: Instead of using a **package manager** like npm, Deno uses **URLs** to directly import
    modules from **remote locations** (like GitHub, Deno Land, etc.) or locally.

## command

- **create nextjs app**

```bash

deno run -A npm:create-next-app@latest

```

