---
date: 2024-10-30T00:00:00.000Z
tags:
  - javascript
  - fetch
  - react
  - nextjs
  - bearer
  - handle
hubs:
  - '[[]]'
urls:
  - null
---
# fetch

```javascript

"use server";

async function Fetch() {
 const response = await fetch("http://localhost:8080/test");
 if (!response.ok) {
  throw new Error("cannot fetch");
 }

 return response.json();
}

export default async function Page() {
 const result = await Fetch();

 return (
  <div>
   {result.map((res, index):any => (
    <div key={index}> {res.name} </div>
   ))}
  </div>
 );
}

```

```javascript

"use server";

async function Fetch() {
 const response = await fetch("http://localhost:8080/test");
 if (!response.ok) {
  throw new Error("cannot fetch");
 }

 return response.json();
}

export default async function Page() {
 const result = await Fetch();

 return (
  <div>
   {result.map((res, index):any => (
    <div key={index}> {res.name} </div>
   ))}
  </div>
 );
}
```

```javascript

'use client'

import {useState} from "react"

async function Fetch() {
  const response = await fetch("http://localhost:8000/api");
  if (!response.ok) {
    throw new Error("cannot fetch");
  }

  return response.json()
}

export default function Page() {
[value,setValue] = useState([])


  const initResult = async () => {
    try {
  const result = await Fetch()
  setValue(result)

      } catch (error) {
        console.log(error)
        }
    }

  useEffect(() => {
    initResult()

    },[])

  return <div>
    {result.map((res,index) => (
    <div> res.name  </div>
      )}
  </div>
  }
```

## fetch with Bearer

```javascript
// utils/api.js

export async function postWithBearer(url, data, token) {
  try {
    const response = await fetch(url, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Authorization: `Bearer ${token}`, // Add the Bearer token
      },
      body: JSON.stringify(data), // Convert data to JSON string
    });

    if (!response.ok) {
      throw new Error(`Request failed: ${response.status}`);
    }

    return await response.json(); // Parse JSON response
  } catch (error) {
    console.error("Error:", error);
    return null;
  }
}
```

```typescript


"use client";

import React, { useEffect, useState } from "react";
import Cookies from "js-cookie";

export async function postWithBearer(
 url: string,
 token: string,
): Promise<any[] | undefined> {
 try {
  const response = await fetch(url, {
   method: "GET",
   headers: {
    "Content-Type": "application/json",
    Authorization: `Bearer ${token}`,
   },
  });

  if (!response.ok) {
   throw new Error(`Request failed: ${response.status}`);
  }

  return await response.json();
 } catch (error) {
  console.error("Error:", error);
 }
}

const Page = () => {
 const [result, setResult] = useState<any[]>([]);

 useEffect(() => {
  const fetchData = async () => {
   const token = Cookies.get("jwt");

   if (token) {
    try {
     const data = await postWithBearer(
      "http://localhost:8080/users",
      token,
     );
     if (data) {
      setResult(data);
     }
    } catch (error) {
     console.error("Error fetching data:", error);
    }
   }
  };

  fetchData();
 }, []);

 return (
  <>
   {result.map((value: any) => (
    <div key={value.id}>{value.name}</div>
   ))}
  </>
 );
};

export default Page;

```

## reset FormData and retrieve FormData

```typescript
(event.currentTarget as HTMLFormElement)?.reset();

const formData = new FormData(event.currentTarget);
const { email, password, name, confirmPassword } = Object.fromEntries(formData);
```

## create handlechange

```javascript

const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  const { name, value } = e.target;
  setCategory((prev) => ({
    ...prev,
    [name]: value,
  }));
};



<input
  type="text"
  name="name"
  value={category.name}
  onChange={handleChange}
  className="border border-gray-400 text-indigo-300"
/>

```

```typescript
const handleChange = (e: React.ChangeEvent<HTMLInputElement>) => {
  const { name, value } = e.target;
  setNewExpense((prev: any) => ({
    ...prev,
    [name]: value,
  }));
};

const handleSubmit = async (event: React.FormEvent<HTMLFormElement>) => {
  event.preventDefault();

  const response = await fetchPost("transactions", newExpense);
  setNewExpense(response);
};
```

```javascript

const useInput = (initialValue: string) => {
  const [value, setValue] = useState(initialValue);
  const onChange = (e: React.ChangeEvent<HTMLInputElement>) => setValue(e.target.value);
  return { value, onChange };
};

// Usage
const nameInput = useInput("");
<input {...nameInput} className="border border-gray-400 text-indigo-300" />;

```

## for isNan problem

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
