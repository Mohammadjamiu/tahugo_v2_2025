---
title: "How to Sync a Local Git Branch That Is Ahead of Remote Without Losing Changes"
description: "If your Git branch is ahead of the remote and you need to pull new changes without losing your local work, use git stash, git pull --rebase, and resolve conflicts safely."
image: "/images/sync-local-git-branch-with-remote.png"
slug: sync-local-git-branch-with-remote
postdate: March 4, 2025
weight: 466
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

I noticed that my **local branch** was ahead of `origin/main` by **2 commits**,

but I also needed to pull the latest changes from the remote repository. Running `git status` showed this:

```sh
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   package.json
        modified:   src/app/payment/page.tsx
        modified:   src/components/PaystackPayment.tsx
        modified:   ../../pnpm-lock.yaml

no changes added to commit (use "git add" and/or "git commit -a")
```

I didn't want to lose my local changes, but I also needed the latest updates from the remote repository. Simply running `git pull` might cause conflicts,

so I had to find a safe way to merge everything properly.

## **How I Fixed It**

Here’s exactly what I did to **keep my local changes** while also pulling the latest updates from the remote branch:

### **Step 1: Stash Local Changes (Optional but Recommended)**

Since I had **unstaged changes**, I needed to temporarily save them using `git stash`:

```sh
git stash
```

After running this, I got the following message:

```sh
Saved working directory and index state WIP on main: [commit-hash] Message
```

At this point, my working directory was clean, and I was ready to pull the latest changes safely.

### **Step 2: Pull the Latest Changes With Rebase**

Instead of a normal `git pull`, I used the `--rebase` flag to **apply my local changes on top of the latest remote changes**:

```sh
git pull origin main --rebase
```

This resulted in merge conflicts because Git couldn't automatically apply my changes:

```sh
Auto-merging apps/cv-resume-builder/src/app/(create)/layout.tsx
CONFLICT (content): Merge conflict in apps/cv-resume-builder/src/app/(create)/layout.tsx
Auto-merging apps/cv-resume-builder/src/app/(main)/layout.tsx
CONFLICT (content): Merge conflict in apps/cv-resume-builder/src/app/(main)/layout.tsx
Auto-merging apps/cv-resume-builder/src/app/(main)/page.tsx
CONFLICT (content): Merge conflict in apps/cv-resume-builder/src/app/(main)/page.tsx
error: could not apply [commit-hash]... added ramadan bonus banner
```

### **Step 3: Manually Resolve Merge Conflicts**

I opened each conflicting file in my code editor (e.g., VS Code) and **manually accepted the correct changes**. The conflicts were marked like this:

```js
<<<<<<< HEAD
// Local changes
const Banner = () => <h1>My Local Version</h1>;
=======
const Banner = () => <h1>Updated Remote Version</h1>;
>>>>>>> origin/main
```

I **chose the best version**, often combining both like this:

```js
const Banner = () => <h1>My Local Version + Updated Remote Version</h1>;
```

After resolving all conflicts, I staged the files:

```sh
git add .
```

Then I continued the rebase process:

```sh
git rebase --continue
```

This completed the rebase successfully.

### **Step 4: Apply Stashed Changes (If Any)**

Since I had stashed my changes earlier, I restored them with:

```sh
git stash pop
```

I checked `git status` to confirm everything was fine:

```sh
On branch main
Your branch is ahead of 'origin/main' by 2 commits.
nothing to commit, working tree clean
```

### **Step 5: Push Changes to Remote**

Finally, I pushed my updated branch to GitHub:

```sh
git push origin main
```

Now, my local branch was fully in sync with the remote branch, and none of my changes were lost. 🚀

## **FAQ**

### **1. What if I get "fatal: No rebase in progress"?**

That means Git has already completed the rebase. Run `git status` to check if everything is clean.

If you still have changes, try `git rebase --continue`.

### **2. What if I accidentally aborted the rebase?**

You can try `git reflog` to find your last working commit and reset your branch:

```sh
git reset --hard [commit-hash]
```

### **3. How can I avoid merge conflicts in the future?**

To minimize conflicts, always **pull with rebase** before making local changes:

```sh
git pull --rebase
```

Now, you know how to safely sync your local Git branch with the remote without losing your changes! 🚀
