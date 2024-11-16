---
date: 2024-10-25T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# tailwind

## add child element

```css

const plugin = require('tailwindcss/plugin')

module.exports = {
  plugins: {
 plugin(function ({ addVariant }:any) {
        addVariant('child', '& > *');
        addVariant('child-hover', '& > *:hover');
    })
  }
```

```css
npm install -D autoprefixer

module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  }
}

```
