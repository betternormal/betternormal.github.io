---
layout: post
title: "Best Time to Buy and Sell Stock"
author: "praconfi"
tags: leetcode
---

# Best Time to Buy and Sell Stock

## my solution

```js
// 각자리 순회하면서 뒷자리들과의 최대이익을 구한다.
// max값을 갱신한다.
const BestTimetoBuyandSellStock = (prices) => {
	let maxBenefit= 0;
	for(let i=0; i<prices.length; i++) {
	    let buy = prices.shift();
	    let benefit = Math.max(...prices.map((item)=> item - buy));
	    if (benefit > maxBenefit) {
		    maxBenefit = benefit
	    }
	}
	return maxBenefit;
}
```