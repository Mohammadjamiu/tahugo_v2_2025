---
title: "How to Automatically Sort Tailwind CSS Classes in React or Next.js"
description: "Learn how to use Prettier with the Tailwind CSS plugin to automatically sort and organize your CSS classes in React or Next.js for cleaner, consistent code."
image: /images/how-to-automatically-sort-tailwind-css-classes-in-react-or-nextjs.png
slug: how-to-automatically-sort-tailwind-css-classes-in-react-or-nextjs
postdate: February 21, 2025
weight: 457
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

When using Tailwind CSS in a React or Next.js app, the order of classes in the `className` property doesn’t seem to matter for functionality.

However, I noticed it can get messy and inconsistent, especially for readability and maintaining a clean codebase. For instance:

```jsx
<article className="gap-3 rounded-lg border p-5 hover:bg-muted/60 flex">
  {title}
</article>
```

Even though this works fine, the classes are out of order and less readable.

To fix this issue, I used Prettier with a Tailwind CSS plugin to automatically sort my classes in a consistent order:

1. **Install Dependencies**:  
   I installed Prettier and the Tailwind CSS plugin as devDependencies:

   ```bash
   pnpm install -D prettier prettier-plugin-tailwindcss
   ```

   > _(You can also use `npm install -D prettier prettier-plugin-tailwindcss` if you’re using npm. I prefer pnpm because it’s faster and more storage-efficient.)_

2. **Configure Prettier**:  
   I created a `.prettierrc` file in the root directory and added the following configuration:

   ```json
   {
     "plugins": ["prettier-plugin-tailwindcss"]
   }
   ```

3. **Class Sorting in Action**:  
   When I saved a file, Prettier automatically reordered the classes for better readability. For example:

   - **Before**:
     ```jsx
     <article className="gap-3 rounded-lg border p-5 hover:bg-muted/60 flex">
       {title}
     </article>
     ```
   - **After**:
     ```jsx
     <article className="flex gap-3 rounded-lg border p-5 hover:bg-muted/60">
       {title}
     </article>
     ```

   Another example:

   - **Before**:
     ```jsx
     <div className="lg:grid-cols-4 grid sm:grid-cols-3 grid-cols-2">
     ```
   - **After**:
     ```jsx
     <div className="grid grid-cols-2 sm:grid-cols-3 lg:grid-cols-4">
     ```

Now, all my Tailwind CSS classes are consistently ordered with minimal effort—Prettier and the plugin take care of it when I save my files!

Here’s a link to TailwindCSS page to read [more](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier).
