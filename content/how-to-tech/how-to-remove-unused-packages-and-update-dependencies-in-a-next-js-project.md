---
title: How to Remove Unused Packages and Update Dependencies in a Next.js Project
description: In this article, I explain how I removed unused packages and
  updated outdated dependencies in my Next.js project, using tools like
  npm-check to clean up and keep my dependencies up to date.
image: /images/how-to-remove-unused-packages-and-update-dependencies-in-a-next.js-project.jpeg
slug: how-to-remove-unused-packages-and-update-dependencies-in-a-next-js-project
postdate: February 21, 2025
weight: 459
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

**The Problem I Faced: Losing Track of Unused Packages and Outdated Dependencies**

I realized that my project was becoming difficult to manage due to a clutter of unused and outdated packages.

I had installed several packages, some of which I no longer needed, and others were out of date.

The issue arose because I was unsure which packages were actively being used in my code and which ones were just taking up space.

This made it harder to keep the project optimized and maintainable.

Additionally, with packages that I didn’t need anymore, my dependency tree was unnecessarily large, which could also lead to potential issues in performance and security.

I wanted to clean up my project by removing unused dependencies and updating outdated packages.

But, without a clear way to check which packages were in use, I was unsure how to go about it.

### **Steps I Took to Clean Up Unused Packages and Keep My Dependencies Up-to-Date**

To solve this problem, I followed these steps:

#### **Install `npm-check` Tool:**

The first step I took was to install the `npm-check` tool globally.

This tool helps identify which packages are outdated, missing, or unused in my project. I installed it using the following command:

```
npm install -g npm-check

```

#### **Run `npm-check`:**

Once `npm-check` was installed, I navigated to my project directory in the terminal and ran the command:

```bash
npm-check
```

This command analyzed my `node_modules` folder and `package.json` file, generating a report that highlighted the following:

- Packages with updates available.
- Packages that were potentially unused.
- Packages that were missing from `package.json` but still referenced in the code.

![how-to-remove-unused-packages-and-update-dependencies-in-a-next.js-project.jpeg](/images/how-to-remove-unused-packages-and-update-dependencies-in-a-next.js-project.jpeg)

#### **Identify Unused Packages:**

After running the check, I noticed several packages flagged as **"NOTUSED"**. For example, packages like `mdast-util-toc`, `rehype-parse`, and `remark` were no longer being used in the code.

The tool suggested that I review my code before removing them, but based on my inspection, I confirmed they were not required.

#### **Remove Unused Packages:**

- Since I was confident the unused packages weren’t needed, I uninstalled them with the following commands:

  ```bash
  npm uninstall mdast-util-toc
  npm uninstall rehype-parse
  npm uninstall remark
  ```

  I repeated this process for all unused packages flagged by the tool.

#### **Update Outdated Packages:**

The tool also notified me of several packages with updates available, such as `next`, `react`, `tailwindcss`, and `eslint`.

To ensure my project was up-to-date, I followed the provided commands to update these packages:

````
 ```bash
 npm install next@15.0.4 --save
 npm install react@19.0.0 --save
 npm install tailwindcss@3.4.16 --save-dev
 npm install eslint@9.16.0 --save-dev
 ```

 This ensured that my project was using the latest versions of these dependencies, reducing the risk of bugs and vulnerabilities.
````

#### **Address Missing Packages:**

During the check, I also noticed that the `site` package was missing from my `package.json` but was still referenced in several files.

Since it was required by my project, I added it back by installing it:

````jsx
```bash
 npm install site --save
 ```;
````

After making the changes, I ran my application to ensure everything was still working correctly.

I also ran `npm-check` again to confirm that there were no more unused packages and that everything was up-to-date.
