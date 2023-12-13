---
layout: post
author: "praconfi"
tags: 'git'
title: "Commit Rule"
---

- Write a concise subject line.
- Start the subject line with a `capital letter`
- No period at the end of the subject line.
- Use the `present` tense or `imperative mood` in the subject line
- Separate the body(Optional) of the text from the subject line
- In the body, explain "what" and "why" using STAR format
- Include the issue number in the footer(Optional)

```
// Type of Commits

feat:     The new feature being added to a particular application
fix:      A bug fix (this correlates with PATCH in SemVer)
style:    Feature and updates related to styling
refactor: Refactoring a specific section of the codebase
test:     Everything related to testing
docs:     Everything related to documentation
chore:    Regular code maintenance
```

```
// Example

chore : JsonProperty 설정

Add login functionality for users

Users previously had no way to log into the site. This commit adds basic login 
functionality. Still, some more features, like 'forgot password' and email 
verification, will be added later.

Closes #42
```