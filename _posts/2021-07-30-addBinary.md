---
layout: post
title: "addBinary"
author: "praconfi"
tags: leetcode
---

# addBinary

## my solution
```js
const addBinary = (a, b) => {
    let result = parseInt(a, 2) + parseInt(b, 2);
    return result.toString(2)
}
```