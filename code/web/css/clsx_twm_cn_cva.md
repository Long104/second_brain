---
date: 2024-10-25T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# clsx_twm_cn_cva

- **tw-merge**: help with conflict
- **clsx**: help with condition css
- **cn**: combine clsx and tw-merge working together

- **cva**

```css
import { cva } from 'class-variance-authority';
import React from 'react';

// Step 1: Create the CVA instance for the button
const buttonStyles = cva(
  'px-4 py-2 rounded font-medium transition-colors', // Base classes
  {
    variants: {
      color: {
        primary: 'bg-blue-500 text-white hover:bg-blue-600',
        secondary: 'bg-gray-500 text-white hover:bg-gray-600',
      },
      size: {
        small: 'text-sm',
        medium: 'text-base',
        large: 'text-lg',
      },
    },
    defaultVariants: {
      color: 'primary',
      size: 'medium',
    },
  }
);

// Step 2: Use the CVA function in a React component
function Button({ color, size, children }) {
  return <button className={buttonStyles({ color, size })}>{children}</button>;
}

export default function App() {
  return (
    <div className="space-y-4">
      <Button color="primary" size="large">Primary Large Button</Button>
      <Button color="secondary" size="medium">Secondary Medium Button</Button>
      <Button color="primary" size="small">Primary Small Button</Button>
    </div>
  );
}

```
