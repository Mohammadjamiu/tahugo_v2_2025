---
title: "Resolving the EPERM: Operation Not Permitted Error Caused by Concurrent Next.js Instances"
slug: resolving-the-eperm-operation-not-permitted-error-caused-by-concurrent-next-js-instances
description: "Learn how I resolved the 'EPERM: Operation Not Permitted' error in a Next.js 15 project caused by running both the development server and build process simultaneously. Find the step-by-step solution to fix this issue."
image: /images/resolving-the-eperm-operation-not-permitted-error-caused.png
postdate: February 21, 2025
categorylabel: Tech Stuff
categories: '["How-to-tech"]'
weight: 454
categorylink: /categories/how-to-tech
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

I was working on a Next.js 15 project using `pnpm`, and when I tried to run the build command (`pnpm build`), I encountered the following error:

```
uncaughtException [Error: EPERM: operation not permitted, open 'C:\Users\USER\Desktop\My Projects\tooabstractive\.next\trace'] {
  errno: -4048,
  code: 'EPERM',
  syscall: 'open',
  path: 'C:\\Users\\USER\\Desktop\\My Projects\\tooabstractive\\.next\\trace'
}
 ELIFECYCLE  Command failed with exit code 1.
```

This error occurred because I was also running an instance of the app using `pnpm dev` (the development server) at the same time.

Once I closed the dev server, the issue was resolved, and the build process worked as expected.

### What I Learned

1. **Close the Development Server:**
   I realized that running the development server (`pnpm dev`) while also attempting to build the project (`pnpm build`) caused a conflict, as both processes tried to access and modify the same files in the `.next` folder.

   - I stopped the development server by closing the terminal where `pnpm dev` was running or by pressing `Ctrl + C` in that terminal.

2. **Run the Build Command:**
   After closing the development server, I ran `pnpm build` again, and the build process completed successfully without the "EPERM: operation not permitted" error.
3. **Avoid Running Multiple Instances Simultaneously:**
   To prevent this issue from occurring in the future, I made sure to avoid running both the development server and the build process simultaneously.

   This way, only one instance has access to the `.next` folder at a time, preventing conflicts and permission issues.

By ensuring that only one process is accessing the `.next` folder at a time, I was able to successfully build my Next.js project without encountering the "EPERM: operation not permitted" error.
