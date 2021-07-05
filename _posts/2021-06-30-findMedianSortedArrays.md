---
layout: post
title: "findMedianSortedArrays Post"
author: "praconfi"
tags: leetcode
---

# findMedianSortedArrays

##  my answer
```js
const findMedianSortedArrays = function(nums1, nums2) {
	let nums3 = nums1.concat(nums2);
	nums3 = nums3.sort();
	if(nums3.length % 2 === 1){
		// odd numbers
		return nums3[Math.floor(nums3.length /2)]
	} else {
		// even numbers
		return ( nums3[nums3.length/2 -1] + nums3[nums3.length/2] ) / 2
	}
};
```

ref: https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Math