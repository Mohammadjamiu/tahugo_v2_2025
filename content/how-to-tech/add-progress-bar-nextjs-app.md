---
title: "How to Add a Progress Bar to Your Next.js App for Better User Experience"
description: "Learn how to enhance the responsiveness of your Next.js app by adding a progress bar using the Next NProgress Bar package. Step-by-step guide included."
image: /images/add-progress-bar-nextjs-app.png
slug: add-progress-bar-nextjs-app
postdate: February 21, 2025
weight: 458
categorylink: /categories/how-to-tech
categorylabel: Tech Stuff
categories: '["How-to-tech"]'
type: posts
author: Mohammad Jamiu
author_credit: false
author_credit_name: ""
author_credit_info: ""
author_credit_image: /images/imgph.webp
Affliate_Links: false
draft: false
mathjax: false
Google_Ads: true
---

I noticed that my Next.js blog post page took some time to load, which made the website feel unresponsive.

Even though I’ve been optimizing the app by dynamically importing modules, tracking large package sizes, and making improvements, it still felt sluggish to users.

To address this, I decided to add a progress bar at the top of the page.

Interestingly, it gives a sense of activity, reducing the perception of unresponsiveness.

It’s funny how our brains work—just seeing a loading bar feels reassuring!

**I Followed These Steps...**  
To implement a progress bar in my Next.js 15 app, I used the _**Next NProgress Bar**_ package. Here’s how I did it:

1. **Install the Package**

   I installed the package using:

   ```bash
   pnpm i next-nprogress-bar
   ```

   If you’re using npm, you can run:

   ```bash
   npm i next-nprogress-bar
   ```

2. **Create a ProgressBarProvider Component**

   I followed the package documentation and created a provider component to wrap my application.

   This ensures that the progress bar is properly integrated without requiring the `use client` directive in my layout.

   Here's a link to the package documentation on npmjs. [https://www.npmjs.com/package/next-nprogress-bar](https://www.npmjs.com/package/next-nprogress-bar)

   ```js
   // /components/ProgressBarProvider.tsx
   "use client";

   import { AppProgressBar as ProgressBar } from "next-nprogress-bar";

   const Providers = ({ children }: { children: React.ReactNode }) => {
     return (
       <>
         {children}
         <ProgressBar
           height="4px"
           color="#fffd00"
           // This line above 👆
           options={{ showSpinner: false }}
           shallowRouting
         />
       </>
     );
   };

   export default Providers;
   ```

   Note: You can customize the progress bar color using HEX or HSL values.

3. **Import and use the Provider inside `layout.tsx`**  
   I imported the `Providers` component into the `layout.tsx` file to wrap the `{children}`.

   ```js
   // /app/layout.tsx
   import Providers from "@/components/ProgressBarProvider";
   // This line above 👆
   export const metadata = {
     title: "My Next.js App",
     description: "Optimized with a progress bar",
   };

   export default function RootLayout({
     children,
   }: {
     children: React.ReactNode,
   }) {
     return (
       <html lang="en">
         <body>
           <Providers>{children}</Providers>
           // This line above 👆
         </body>
       </html>
     );
   }
   ```

Wrapping the app this way avoids making the `layout.tsx` a client component, which is not ideal for performance.

After completing the setup, I ran my app locally to test the changes.

The progress bar now gives immediate feedback to users, significantly improving the perceived speed of my app.

While there’s still an initial cold start, the progress bar improves the user experience, making the site feel faster.

Hopefully, future updates in Next.js will address this issue. Thanks to the Next.js team for their contributions to the dev community!
