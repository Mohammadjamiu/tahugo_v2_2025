---
title: "Fixing Apex Domain Issues on Next.js Vercel Deployment with Namecheap"
slug: "fixing-apex-domain-issues-nextjs-vercel"
description: "Learn how to fix the apex domain not working issue when deploying a Next.js app on Vercel with Namecheap DNS settings."
postdate: February 22, 2025

categorylabel: "Tech Stuff"
categories: '["How-to-tech"]'
image: "/images/fixing-apex-domain-issues-nextjs-vercel.png"
weight: 462
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

I purchased a domain name from Namecheap to use for my **Turborepo** projects, which include two Next.js applications.

One is the **main site**, which should be accessible at **monoed.africa**, while the other is a subdomain project, accessible at **cv-resume-builder.monoed.africa**.

After deploying both projects separately on Vercel, I configured the domain settings as follows:

- **Main site domain (monoed.africa) setup in Vercel:**

1.  - **Type:** A
    - **Host:** @
    - **Value:** 76.76.21.21

2.  - **Type:** CNAME
    - **Host:** www
    - **Value:** cname.vercel-dns.com

Vercel then refreshed and applied an SSL certificate.

However, a problem arose when accessing **monoed.africa** in the browser—it failed to load and showed a “cannot reach page” error.

Meanwhile, **www.monoed.africa** and the default **monoed.vercel.app** domain worked perfectly.

## Problem Analysis

The issue was that the **Apex domain (monoed.africa)** was not correctly pointing to the Vercel deployment.

The A record (**76.76.21.21**) did not resolve correctly, causing the domain to be inaccessible without the “www.” prefix.

Many users I sent the domain to instinctively typed **monoed.africa**, expecting it to work, but it did not.

I had to find a solution to ensure the apex domain worked correctly.

## Solution: Correcting the Namecheap DNS Settings

To fix the issue, I followed these steps:

### 1. Remove the Incorrect A Record

- In **Namecheap Advanced DNS**, delete the **A record** with:
  - **Host:** @
  - **Value:** 76.76.21.21

![Vercel Incorrect Apex Namecheap](/images/vercel-apex-domain-issue.jpeg)
![Vercel Incorrect Apex Namecheap](/images/vercel-incorrect-apex.jpeg)

### 2. Add a CNAME Record for the Apex Domain

- Create a **CNAME record** instead:
  - **Host:** @
  - **Value:** **[your Vercel domain]**, e.g., **monoed.vercel.app**

### 3. Ensure the www Subdomain Record is Set Correctly

- Add a **CNAME record** for www:
  - **Host:** www
  - **Value:** cname.vercel-dns.com

### 4. Configure Redirects in Vercel

- Go to your Vercel domain dashboard and set up redirection:
  - Either redirect **monoed.africa** to **www.monoed.africa**, or
  - Redirect **www.monoed.africa** to **monoed.africa**

### 5. Check DNS Propagation

- Use [DNS Checker](https://dnschecker.org/) to verify if the changes have propagated.
- If the new settings are not visible, wait for **up to 48 hours** for full propagation.

### 6. Subdomain Setup for the Secondary Next.js Project

For the second project (**cv-resume-builder.monoed.africa**), I added:

- **Type:** CNAME
- **Host:** cv-resume-builder
- **Value:** cname.vercel-dns.com

After these changes, **both the apex domain and subdomains started working correctly.**

## In Summary

- **Primary Issue:** The apex domain (**monoed.africa**) was not resolving because the A record (76.76.21.21) did not point correctly to the deployment.
- **Solution:** Replace the A record with a CNAME record pointing to the Vercel-provided domain.
- **Additional Setup:** Configure proper DNS settings and verify propagation before testing.

## FAQs

**1. Why wasn’t monoed.africa working without www?**

The A record (76.76.21.21) didn’t resolve correctly, causing an issue with apex domain resolution.

Changing it to a CNAME pointing to the Vercel deployment fixed the problem.

**2. What DNS records should I use for a Vercel deployment with a Namecheap domain?**

- For the **apex domain**, use a **CNAME** record:
  - **Host:** @
  - **Value:** _your Vercel-provided domain_ (e.g., **monoed.vercel.app**)
- For the **www subdomain**, use a **CNAME** record:
  - **Host:** www
  - **Value:** cname.vercel-dns.com

**3. How long does DNS propagation take?**

DNS propagation can take up to **48 hours**. Use [DNS Checker](https://dnschecker.org/) to monitor changes.

**4. How do I set up redirects between the apex domain and www subdomain on Vercel?**

- Go to **Vercel > Domains > Redirect Settings**
- Choose whether to redirect **monoed.africa** to **www.monoed.africa** or vice versa
- Save and test to ensure it works

By following these steps, I was able to resolve the **apex domain issue** and ensure that both my **apex and subdomains work correctly** on Vercel.
