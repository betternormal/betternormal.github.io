---
layout: post
title: "Move Zeroes"
author: "praconfi"
tags: leetcode
---

# Move Zeroes

## my solution
```js
const MoveZeroes = (arr) => {
	let count = 0	
  for(let i=0; i<arr.length; i++) {
      if(arr[i] === 0) {
        arr.splice(i, 1);
        count ++
        i--
      }
  }

  for(let j=0; j<count; j++ ){
      arr.push(0);
  }
  return arr;
}
```