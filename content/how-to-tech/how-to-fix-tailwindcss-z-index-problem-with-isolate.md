---
title: "How to Fix TailwindCSS z-index Problem with `isolate`"
description: "Fix TailwindCSS z-index issues by adding the isolate class to the parent container. It scopes z-index values, ensuring elements like sticky navbars display correctly."
image: "/images/isolate-tailwindcss-to-fix-z-index-issue.png"
slug: how-to-fix-tailwindcss-z-index-problem-with-isolate
postdate: February 21, 2025
weight: 455
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

I was building a website with a sticky navbar that had a `z-index` of `z-10`. Later, I added a `div` with some text in the main content section.

When I scrolled up, I realized that the text appeared **above** the navbar, even though I had increased the navbar’s z-index and reduced the z-index of the content.

I even tried using the `!important` flag (e.g., `!z-`) on the z-index, which worked sometimes, but it felt messy and unreliable.

Before using the isolate, here is how the text goes over the navbar.
![Before adding isolate tailwindcss class](/images/when-there-is-no-isolate.jpeg "Before adding isolate tailwindcss class")

## The Solution

I followed these steps to fix the issue:

1. **Locate the Parent Container**: I identified the main parent `div` that holds all the content below the navbar.
2. **Add the `isolate` Class**: I added the `isolate` class to this parent `div`.

   This class ensures that the z-index of its children doesn’t interfere with elements outside this container, like the navbar.

3. **Tested the Fix**: After applying the `isolate` class, I noticed that the text no longer appeared above the navbar, even when its z-index was set higher.

   The `isolate` class scoped the z-index properly, ensuring no overlap.

### Example Implementation in Next.js

Here’s the exact code I used:

```jsx
export default function Home() {
  return (
    <div>
      {/* Sticky Navbar */}
      <header className="sticky top-0 z-10 bg-blue-500 p-4 text-white">
        Sticky Navbar
      </header>

      {/* Main Content */}
      <main className="relative isolate p-4">
        <div className="relative z-20 bg-gray-100 p-8">
          <h1 className="text-2xl font-bold">Main Content</h1>
          <p>
            This content has a higher z-index but won’t overlap the navbar
            because the `isolate` class is applied to the parent container.
          </p>
        </div>
      </main>
    </div>
  );
}
```

After using the isolate, here is how the text goes below the navbar.
![After adding isolate tailwindcss class](/images/when-there-is-isolate.jpeg "After adding isolate tailwindcss class")

### Why It Works

By adding the `isolate` class to the parent container (`<main>`), the z-index values of its children (`<div>` with `z-20`) become relative to other elements **within that container**.

This prevents them from interfering with elements outside, like the sticky navbar.
