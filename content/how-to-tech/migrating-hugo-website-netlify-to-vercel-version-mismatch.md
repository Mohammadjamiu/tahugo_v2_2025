---
title: "Migrating a Hugo Website from Netlify to Vercel: Resolving Deployment Errors Due to Hugo Version Mismatch"
slug: migrating-hugo-website-netlify-to-vercel-version-mismatch
postdate: February 20, 2025
description: Learn how to successfully migrate your Hugo website from Netlify to Vercel by addressing deployment errors caused by Hugo version mismatches.
categorylabel: Tech Stuff
categories: '["How-to-tech"]'
image: /images/migrating-hugo-website-netlify-to-vercel-version-mismatch.png
weight: 453
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

I recently decided to migrate my Hugo website from Netlify to Vercel to take advantage of Vercel's features.

After cloning the project and removing any Netlify-specific configurations, I attempted to deploy the site on Vercel.

However, I encountered deployment errors because Vercel was using a different Hugo version than my local environment.

My local Hugo version was:

```bash

hugo v0.125.7-b1d808bc373f53ad37c8966bb02a6aea095db5f8 windows/amd64 BuildDate=2024-05-08T14:46:24Z VendorInfo=gohugoio
```

To resolve this issue, I created a `vercel.json` file at the root of my project in Visual Studio Code (VSCode) with the following content:

```json
{
  "build": {
    "env": {
      "HUGO_VERSION": "0.125.7"
    }
  }
}
```

This configuration explicitly sets the Hugo version that Vercel should use during the build process. After adding this file and redeploying,

Vercel utilized the specified Hugo version, aligning with my local development environment and resolving the deployment issues.

By ensuring that both my local and Vercel environments use the same Hugo version, I was able to successfully migrate my website without further issues.
