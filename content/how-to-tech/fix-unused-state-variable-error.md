---
title: "How to Fix 'Assigned a Value but Never Used' Error in React with TypeScript"
description: "This guide helps you troubleshoot and resolve the TypeScript ESLint error when a state variable is declared but never used in a React component."
image: "/images/fix-unused-state-variable-error.png"
slug: fix-unused-state-variable-error
postdate: March 4, 2025
weight: 467
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

I encountered the following error while working on a React project using TypeScript:

```sh
328:10  Error: 'displayAmount' is assigned a value but never used.  @typescript-eslint/no-unused-vars
```

The error happened because I declared a state variable with `useState`, but I never used it in my component.

TypeScript, with `@typescript-eslint/no-unused-vars`, enforces that all declared variables should be used to maintain clean and efficient code.

## **The Solution**

To fix this issue, I considered the following approaches:

### **1. Use the State Variable in JSX or Logic**

If `displayAmount` is necessary, ensure it is used somewhere in the component:

```tsx
const [displayAmount, setDisplayAmount] = useState(amount);

return <div>Amount: {displayAmount}</div>;
```

This way, TypeScript recognizes the variable as being used, and the error disappears.

### **2. Remove the Unused Variable**

If `displayAmount` is not needed, I removed it while keeping the state updater function:

```tsx
const [, setDisplayAmount] = useState(amount);
```

By using a comma (`[,]`), I ignored the first value (`displayAmount`), preventing ESLint from flagging it as unused.

### **3. Disable ESLint for This Line (Not Recommended)**

If, for some reason, I wanted to keep the variable but avoid the error, I could temporarily disable the rule:

```tsx
// eslint-disable-next-line @typescript-eslint/no-unused-vars
const [displayAmount, setDisplayAmount] = useState(amount);
```

However, I don't recommend this approach unless absolutely necessary,

as it bypasses TypeScript’s helpful checks.

## **FAQ**

### **1. Why does TypeScript warn about unused variables?**

TypeScript enforces clean code practices by warning developers about variables that are declared but not used.

This helps prevent unnecessary memory usage and keeps code readable.

### **2. What if I plan to use `displayAmount` later?**

If `displayAmount` will be used in future logic but isn't needed yet,

a simple workaround is a temporary console log:

```tsx
console.log(displayAmount); // Prevents unused variable warning
```

This keeps the variable in the code while avoiding the ESLint warning.

### **3. Should I always remove unused state variables?**

Yes, unless you plan to use them soon. Keeping unused variables can make the codebase messy and misleading for future maintenance.

### **4. What if I only need the state setter function?**

If you only need to update state but don't need the value itself, you can ignore the first element of the `useState` array:

```tsx
const [, setDisplayAmount] = useState(amount);
```

This ensures `setDisplayAmount` remains available while avoiding the warning.

### **5. Can I configure ESLint to ignore unused variables?**

Yes, you can modify your ESLint configuration to allow unused variables in some cases.

However, this is not recommended as it might hide potential coding issues.

If needed, you can add this rule to `.eslintrc.json`:

```json
{
  "rules": {
    "@typescript-eslint/no-unused-vars": ["warn", { "varsIgnorePattern": "^_" }]
  }
}
```

This allows variables prefixed with `_` (e.g., `_displayAmount`) to be ignored by ESLint.

This guide ensures your React project remains clean while resolving the `@typescript-eslint/no-unused-vars` error effectively.
