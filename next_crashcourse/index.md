---
marp: true
title: Next 13/14 Crashcourse
transition: fade
theme: default
class: invert
# backgroundColor: black
---

# <!--fit-->Next 14 Crash Course

## Why are you making me write b*ckend code? 😡

---

# App Router Basics 💫

![bg right](https://images.unsplash.com/photo-1592609931041-40265b692757?q=80&w=1000&auto=format&fit=crop&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D)

---

# Terminology

🌲 Tree\
🎋 Subtree\
🫚 Root\
🍁 Leaf

![bg right fit](./images/tree)

---

# <!--fit-->Folder Structure

---

# Groups 📦

You can group folders in app directory using `(folder_name)` naming scheme.
![bg left fit](./images/groups)

---

# Dynamic segment 🐌

You can use dynamic segments using `[id]` naming scheme.\
Then use your custom url param in `Page` component like so:

```typescript
export default function Page({ params }: { params: { slug: string } }) {
  return <div>My Post: {params.slug}</div>;
}
```

---

# Error Handling ❗

You can create an `error.tsx` file inside nested route.

```typescript
"use client"; // Error components must be Client Components

export default function Error({
  error,
  reset,
}: {
  error: Error & { digest?: string };
  reset: () => void;
}) {
  return (
    <div>
      <h2>Something went wrong!</h2>
      <button
        onClick={() => reset()}
      >
        Try again
      </button>
    </div>
  );
}
```

---

# Loading Component ⏳

Create a loading state by adding a `loading.tsx` file inside a folder.

```typescript
export default function Loading() {
  // You can add any UI inside Loading, including a Skeleton.
  return <LoadingSkeleton />;
}
```

---

# Parallel Routes 🔀

Parallel Routes allows you to simultaneously or conditionally render one or more
pages within the same layout. They are useful for highly dynamic sections of an
app, such as dashboards and feeds on social sites.

![bg right fit](./images/parallel-routes.avif)

---

# Parallel Routes - Default component

You can define a `default.tsx` file to render as a fallback for unmatched slots
during the initial load or full-page reload.

```typescript
export default function Default() {
  return null;
}
```

---

# Intercepting Routes

Intercepting routes can be defined with the (..) convention, which is similar to
relative path convention ../ but for segments.

![bg right fit](./images/intercepting-routes-soft-navigate.avif)

---

# Layout Component

A layout is UI that is shared between multiple pages. On navigation, layouts
preserve state, remain interactive, and do not re-render. Layouts can also be
nested.

```typescript
export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en">
      <body>{children}</body>
    </html>
  );
}
```

---

# Page Component

A page is UI that is unique to a route. You can define pages by exporting a
component from a `page.tsx` file. Use nested folders to define a route and a
page.js file to make the route publicly accessible.

```typescript
// `app/page.tsx` is the UI for the `/` URL
export default function Page() {
  return <h1>Hello, Home page!</h1>;
}
```

---

# Route Handlers && route file

![bg right fit](./images/route-special-file.avif)

---

# <!--fit-->Data Fetching

---

# Fetch API

Next.js extends the native fetch Web API to allow you to configure the caching
and revalidating behavior for each fetch request on the server. React extends
fetch to automatically memoize fetch requests while rendering a React component
tree.

---

# Server Side

```typescript
async function getData() {
  const res = await fetch("https://api.example.com/...");
  // The return value is *not* serialized
  // You can return Date, Map, Set, etc.

  if (!res.ok) {
    // This will activate the closest `error.js` Error Boundary
    throw new Error("Failed to fetch data");
  }

  return res.json();
}

export default async function Page() {
  const data = await getData();

  return <main></main>;
}
```

---

# Client Side

If you need to fetch data in a client component, you can call a Route Handler
from the client. Route Handlers execute on the server and return the data to the
client. This is useful when you don't want to expose sensitive information to
the client, such as API tokens.

---

# <!--fit-->Data Mutations

---

# Server Actions

Server Actions are asynchronous functions that are executed on the server.\
They can be used in Server and Client Components to handle form submissions\
and data mutations in Next.js applications.

---

# Server Components

Server Components can use the inline function level or module level "use server"
directive. To inline a Server Action, add "use server" to the top of the
function body:

```typescript
// Server Component
export default function Page() {
  // Server Action
  async function create() {
    'use server'
 
    // ...
  }
 
  return (
    // ...
  )
}
```

---

# Client Components

Client Components can only import actions that use the module-level "use server"
directive.

```typescript
// app/actions.ts
"use server";

export async function create() {
  // ...
}
```

```typescript
// app/components/button.tsx
import { create } from '@/app/actions'
 
export function Button() {
  return (
    // ...
  )
}
```

---

# Caching & Revalidating

[HERE](https://nextjs.org/docs/app/building-your-application/caching)

---

# <!--fit-->Cheatsheet

---

## Routing

![](./images/decision-tree)

---

# Modals

https://nextjs.org/docs/app/building-your-application/routing/parallel-routes#modals

---

# Importing

Server Side Component -> Default Import\
Cilent Side Component -> Named Import or Default Import

---

# Client vs Server

- Use sever as much as possible
- Don't use global store -> logic is better handled on the server
- Server actions and async components should be enough for most of API
  integration needs

---

# <!--fit-->Q&A
