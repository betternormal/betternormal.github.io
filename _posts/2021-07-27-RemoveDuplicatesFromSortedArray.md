---
layout: post
title: "RemoveDuplicatesFromSortedArray"
author: "praconfi"
tags: leetcode
---

# RemoveDuplicatesFromSortedArray

## my solution

```js
const RemoveDuplicatesFromSortedArray = (arr) => {
	for(let i=0; i<arr.length-1; i++) {
		if(arr[i] === arr[i+1]) {
			arr.splice(i, 1)
			i = 0
		}
	}
	return arr.length
	}
}
```