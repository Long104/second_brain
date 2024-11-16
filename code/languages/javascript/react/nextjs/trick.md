---
date: 2024-11-11T00:00:00.000Z
tags:
  - nextjs
  - javscript
  - react
  - time
  - trick
hubs:
  - '[[]]'
urls:
  - null
---
# trick

## format do mm-dd-tt

```javascript
  date: new Date().toISOString().split("T")[0],
```

    1. new Date(): Creates a new Date object with the current date and time.
    2. .toISOString(): Converts the date to an ISO 8601 string in the format YYYY-MM-DDTHH:mm:ss.sssZ (for example, "2023-11-11T15:23:45.678Z").
    3. .split("T"): Splits the string into two parts using "T" as the separator, resulting in an array like ["2023-11-11", "15:23:45.678Z"].
    4. [0]: Selects the first part of the array, which is the date portion ("2023-11-11"), without the time.

The result is a string representing just the date in the format YYYY-MM-DD.

## for input element

```typescript

             value={
              newExpense.amount === 0 ? "" : newExpense.amount
             }

             onChange={(e) =>
              setNewExpense({
               ...newExpense,
               // amount: parseFloat(e.target.value),
               amount: isNaN(parseFloat(e.target.value))
                ? 0
                : parseFloat(e.target.value),
              })
             }
```

## for reset

```typescript
if (event.target instanceof HTMLFormElement) {
  event.target.reset();
}
```

## time

```javascript
const now = new Date();
const currentHours = now.getHours();
const currentMinutes = now.getMinutes();
const currentSeconds = now.getSeconds();

const fullISODate = `${new Date("2024-11-12").toISOString().split("T")[0]}T${currentHours}:${currentMinutes}:${currentSeconds}Z`;
console.log(fullISODate);
```

## apos

```javascript
&apos;
```

## data state

```css
data - [(state = checked)];
```
