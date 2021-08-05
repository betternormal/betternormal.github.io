---
layout: post
title: "numberOf1Bits"
author: "praconfi"
tags: leetcode
---

# numberOf1Bits

## my solution
```js
const numberOf1Bits = (num) => {
    let numStr = String(num);
    let result = 0;
    for(let i=0; i<numStr.length; i++){
        if(numStr[i] === '1'){
            result++
        }
    }
    return result;
}
```
## problem
String(11111111111111111111111111111101) 이 
"1.1111111111111112e+31" 로 표시된다.