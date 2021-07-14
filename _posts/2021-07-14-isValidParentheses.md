---
layout: post
title: "isValidParentheses"
author: "praconfi"
tags: leetcode
---

# isValidParentheses

## my solution
```js
const isValidParentheses = (str) => {
    let pair = {
        '[' : ']',
        '{' : '}',
        '(' : ')',
    }
    let openers = Object.keys(pair);
    let stack = []
    for(let i=0; i<str.length; i++) {
        if(openers.includes(str[i])) {
            stack.push(str[i])
        } else {
            if(str[i] === pair[stack[stack.length-1]]) {
            stack.pop();
            } else {
                return false;
            }
        } 
    }
    return true;
}
```