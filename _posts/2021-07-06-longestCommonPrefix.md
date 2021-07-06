---
layout: post
title: "longestCommonPrefix"
author: "praconfi"
tags: leetcode
---

# longestCommonPrefix

## my solution

```js
const longestCommonPrefix = (words) => {
	let shortestStr = words.reduce((acc, curr) => acc.length <= curr.length ? acc: curr )
	for(let i=0; i<shortestStr.length; i++) {
		let same = words.every((item)=> item[i] === shortestStr[i])
		if(!same) {
			return shortestStr.substr(0, i);
		}
	}
}
```