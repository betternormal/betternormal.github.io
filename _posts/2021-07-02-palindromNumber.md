---
layout: post
title: "palindromNumber"
author: "praconfi"
tags: leetcode
---

# palindromNumber

## my solution
```js
const palindromNumber = (num) => { 
    let reverseNum = num.toString().split('').reverse().join('');
    reverseNum = parseInt(reverseNum);
    return (num === reverseNum)
}
```