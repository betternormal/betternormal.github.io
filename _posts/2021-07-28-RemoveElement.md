---
layout: post
title: "RemoveElement"
author: "praconfi"
tags: leetcode
---

# RemoveElement

## my solution

```js
// in-place with O(1) extra memory.
const RemoveElement = (arr, val) => {
    for(let i=0; i<arr.length; i++) {
        if(arr[i] === val) {
            arr.splice(i, 1);
            i--
        }
    }
    return arr.length;
}

```