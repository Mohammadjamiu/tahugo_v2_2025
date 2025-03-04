---
title: "How to Insert Ads Dynamically, for Example, After Every 3 Paragraphs in Hugo"
description: "Learn how to dynamically insert Ezoic ads after every three paragraphs in your Hugo posts using shortcodes or modifying the single.html template."
image: "/images/insert-ads-dynamically-hugo.png"
slug: insert-ads-dynamically-hugo
postdate: March 4, 2025
weight: 465
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

When using Hugo with Ezoic ads, you may want to insert ads dynamically within `{{ .Content }}`,

such as after every three paragraphs, instead of manually placing them in each post.

Hugo does not provide a built-in way to achieve this, so you need a custom solution to automate the process.

## **The Solution/Fix**

There are two main ways to insert ads dynamically:

1. **Using a shortcode** (for manual control in individual posts).
2. **Modifying `single.html`** (for automatic insertion across all posts).

### **Method 1: Using a Shortcode**

A shortcode allows you to wrap your post content and dynamically insert ads at the specified intervals.

#### **Step 1: Create the Shortcode File**

Run the following command to create the shortcode file:

```bash
mkdir -p layouts/shortcodes
touch layouts/shortcodes/adsense.html
```

#### **Step 2: Add the Code to `adsense.html`**

Insert this logic inside `layouts/shortcodes/adsense.html`:

```html
{{ $adCode := `<script async src="https://your-ezoic-ad-script.js"></script>` }}
{{ $content := .Inner }}
{{ $paragraphs := split $content "</p>" }}
{{ $interval := 3 }}  <!-- Insert ad every 3 paragraphs -->

{{ range $index, $paragraph := $paragraphs }}
  {{ $paragraph | safeHTML }}</p>
  {{ if and (ne $index 0) (eq (mod $index $interval) 0) }}
    {{ $adCode | safeHTML }}
  {{ end }}
{{ end }}
```

#### **Step 3: Use the Shortcode in Your Posts**

When writing a post in Markdown, wrap the content inside the shortcode:

```md
{{</* adsense */>}}
Lorem ipsum dolor sit amet, consectetur adipiscing elit.

Pellentesque habitant morbi tristique senectus et netus et malesuada fames.

Sed ut perspiciatis unde omnis iste natus error sit voluptatem accusantium.

Curabitur non nulla sit amet nisl tempus convallis quis ac lectus.

Integer nec odio. Praesent libero. Sed cursus ante dapibus diam.
{{</* /adsense */>}}
```

This will ensure that an ad is dynamically inserted after every **third paragraph** within that specific post.

### **Method 2: Editing `single.html` for Automatic Ads**

If you want ads to appear **automatically** in every blog post, modify `single.html` instead of using a shortcode.

#### **Step 1: Open `single.html`**

Navigate to `layouts/_default/single.html` and replace `{{ .Content }}` with the following code:

```html
{{ $adCode := `<script async src="https://your-ezoic-ad-script.js"></script>` }}
{{ $content := .Content }}
{{ $paragraphs := split $content "</p>" }}
{{ $interval := 3 }}  <!-- Insert ad every 3 paragraphs -->

{{ range $index, $paragraph := $paragraphs }}
  {{ $paragraph | safeHTML }}</p>
  {{ if and (ne $index 0) (eq (mod $index $interval) 0) }}
    {{ $adCode | safeHTML }}
  {{ end }}
{{ end }}
```

This method ensures that **all blog posts** will have an ad inserted dynamically

after every three paragraphs without requiring any manual modifications.

## **FAQ**

### **1. Can I insert ads after every 4 or 5 paragraphs instead?**

Yes, simply change `{{ $interval := 3 }}` to your desired number (e.g., `4` or `5`).

### **2. Do I have to use a shortcode, or can I automate ads for all posts?**

If you want **automatic** ad insertion, use **Method 2 (Editing `single.html`)**. If you want more control over where ads appear, use **Method 1 (Shortcode)**.

### **3. What happens if my post has fewer than 3 paragraphs?**

No ad will be inserted because the condition `(eq (mod $index $interval) 0)` won’t be met.
