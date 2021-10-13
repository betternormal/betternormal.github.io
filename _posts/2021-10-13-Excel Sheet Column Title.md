---
layout: post
title: "Excel Sheet Column Title"
author: "praconfi"
tags: leetcode
---

# Excel Sheet Column Title
A -> 1  
B -> 2  
C -> 3  
...  
Z -> 26  
AA -> 27  
AB -> 28   
...
 

Example 1:

Input: columnNumber = 1
Output: "A"

Example 2:

Input: columnNumber = 28
Output: "AB"

Example 3:

Input: columnNumber = 701
Output: "ZY"

Example 4:

Input: columnNumber = 2147483647
Output: "FXSHRXW"
## my solution
문제를 잘못 읽어서 다시 풀어야함
```js
const excelSheetColumnTitle = ( excelString ) => {
    const numPair = {'A': 1,'B': 2,'C': 3,'D': 4,'E': 5,'F': 6,'G': 7,'H': 8,'I': 9,'J': 10,'K': 11,'L': 12,'M': 13,'N': 14,'O': 15,'P': 16,'Q': 17,'R': 18,'S': 19,'T': 20,'U': 21,'V': 22,'W': 23,'X': 24,'Y': 25,'Z': 26,}
    let excelArr = excelString.toUpperCase().split('');
    let pow = excelArr.length-1;
    let result = excelArr.reduce((acc, curr)=>  acc += numPair[curr]* (26 ** pow--), 0);
    return result;
}
```

