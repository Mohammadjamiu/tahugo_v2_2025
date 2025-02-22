---
title: "Where Should Your `middleware.ts` File Be Located in a Next.js 15 Project?"
slug: "nextjs-middleware-file-location"
description: "Having trouble placing your `middleware.ts` file correctly in a Next.js 15 project? The right placement depends on whether you're using the `src` directory or not. This article explains the correct location and how to structure middleware properly for optimal performance."
postdate: February 22, 2025
categorylabel: "Tech Stuff"
categories: '["How-to-tech"]'
image: "/images/nextjs-middleware-file-location.png"
weight: 463
categorylink: "/categories/how-to-tech"
type: "posts"
author: "Your Name"
author_credit: false
author_credit_name: ""
author_credit_info: ""
author_credit_image: "/images/your-profile-image.png"
Affliate_Links: false
draft: false
mathjax: false
Google_Ads: true
---

Middleware in Next.js is a powerful tool for handling route protection, authentication, and redirects before the page even loads.

Unlike solutions that rely on `useEffect` or `useRouter`, middleware runs at the edge, ensuring a seamless experience without flickering UI issues.

## **Problem:** Middleware Not Working Due to Incorrect Placement

If your `middleware.ts` file isn’t working, it’s likely placed incorrectly in your project structure.

## **Solution:** Correct Middleware Placement Based on Your Project Structure

### ✅ **If You Are Using the `src` Directory:**

Place `middleware.ts` inside `src`, at the same level as the `app` folder:

```
/src
  ├── app/
  ├── middleware.ts
```

#### ✅ **If You Are Not Using the `src` Directory:**

Place `middleware.ts` in the root of your project, at the same level as the `pages` or `app` folder:

```
/
  ├── app/ (or pages/)
  ├── middleware.ts
```

### **Key Takeaways**

- **One `middleware.ts` file per project** – Next.js only supports a single middleware file.
- **Modular Middleware Approach:** Even though Next.js only allows one middleware file,

  you can break it into multiple functions by creating separate files and importing them into `middleware.ts`.

- **Performance Boost:** Middleware runs before the page loads,

  ensuring smoother user experience compared to `useEffect`-based protections.

### **Example Middleware File**

```ts
import { NextResponse } from "next/server";
import type { NextRequest } from "next/server";

export function middleware(req: NextRequest) {
  const isAuthenticated = Boolean(req.cookies.get("token"));

  if (!isAuthenticated) {
    return NextResponse.redirect(new URL("/login", req.url));
  }
  return NextResponse.next();
}
```

### **Common Questions (FAQs)**

**1. What happens if I place `middleware.ts` in the wrong directory?**  
Next.js won’t recognize it, meaning your middleware logic won’t execute.

**2. Can I have multiple `middleware.ts` files?**  
No, Next.js only supports a single `middleware.ts` file.

However, you can modularize it by importing functions from other files.

**3. Can middleware protect API routes?**  
No, middleware is only for handling requests to pages, not API routes (`/api`).

Use API route handlers (`app/api`) for API-specific protection.

**4. How can I verify my middleware is running correctly?**  
Add a `console.log` inside your middleware function and check your server logs to ensure it executes.

For more details, check out the [Next.js middleware documentation](https://nextjs.org/docs/app/building-your-application/routing/middleware).
