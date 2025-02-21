---
title: "How to Use Next.js 14 and 15 in Separate Branches and Deploy to Netlify"
description: "Learn how to manage Next.js 14 and 15 in a single GitHub repo using branches, fix git push upstream errors, and deploy the correct branch to Netlify."
image: "/images/how-to-use-next.js-14-and-15-in-separate-branches-and-deploy-to-netlify.png"
slug: how-to-use-next.js-14-and-15-in-separate-branches-and-deploy-to-netlify
postdate: February 21, 2025
weight: 456
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

I deployed my project using Next.js 15 and React 19 (experimental).

While testing on Netlify, I noticed the blog posts on the site loaded slower compared to a project using Next.js 14.2.3.

I decided to revert to Next.js 14.2.3 for better performance but wanted to keep Next.js 15 on my GitHub in the main branch while working on the older version in a new branch.

## **How I Go About It**

1. Created a Branch for Next.js 14

   I created a new branch called `nextjsV14` in my local Next.js 15 project:

   ```bash
   git checkout -b nextjsV14
   ```

2. Set Up Next.js 14.2.3

   To spin up a fresh Next.js 14.2.3 project:

   - I deleted everything in the Next.js 15 project folder except `.git` and `.gitignore`. This retained the repository’s tracking history.
   - Ran:
     ```bash
     pnpx create-next-app@14.2.3 .
     ```
     I used `pnpx` because I prefer `pnpm`. If you use npm, you can run:
     ```bash
     npx create-next-app@14.2.3 .
     ```
     The `.` specifies that the installation should happen in the current directory.

3. Fixed `.gitignore` and Installed Dependencies

   - I deleted and recreated `.gitignore` to ensure proper formatting, adding entries like `node_modules` to exclude unnecessary files from being pushed.
   - Installed dependencies with:
     ```bash
     pnpm install
     ```
     (or `npm install` if you prefer).

4. Tested Locally

   - Started the development server:
     ```bash
     pnpm dev
     ```
     (or `npm run dev` for npm users).
   - Verified the project at `localhost:3000`.

5. Committed and Pushed Changes

   - Staged and committed the files:
     ```bash
     git add .
     git commit -m "Initialized Next.js 14.2.3 project"
     ```
   - Attempted to push but encountered an error:
     ```bash
     fatal: The current branch nextjsV14 has no upstream branch.
     To push the current branch and set the remote as upstream, use:
         git push --set-upstream origin nextjsV14
     ```
   - Fixed the error by setting the upstream branch:
     ```bash
     git push --set-upstream origin nextjsV14
     ```
   - This pushed the code to the `nextjsV14` branch. Any future changes can now be pushed using `git push`.

6. Updated Netlify
   - Logged into the Netlify dashboard, unlinked the repository, and linked it again to switch the branch from `main` to `nextjsV14`.

So here are the steps I took to successfully maintained both Next.js 15 and 14.2.3 projects in the same repository,

improved performance with the older version, and deployed it on Netlify.
