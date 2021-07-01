---
layout: post
title: "reverseInteger"
author: "praconfi"
tags: algorithm
---
# findMedianSortedArrays

##  my answer

```js
const reverseInteger = (number) => {
    if(number > 0) {
        let reverseNum = number.toString().split('').reverse().join('');
        return parseInt(reverseNum);
    } else if(number < 0) {
        let reverseNum = number.toString().substr(1).split('').reverse().join('')
        reverseNum = '-' + reverseNum;
        return parseInt(reverseNum);
    } else {
        return 0;
    }
}
```