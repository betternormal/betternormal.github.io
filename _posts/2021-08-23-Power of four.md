---
layout: post
title: "Power of four"
author: "praconfi"
tags: leetcode
---

# Power of four
Constraints:
-2<sup>31</sup> <= n <= 2<sup>31</sup> - 1
## my solution
```js
const powerOfFour = (n) => {
	for( let i=0; i<15; i++ ) {
		if(Math.pow(4, i) === n) {
		    return true;
		 }
	}    
	return false;
}
