---
layout: post
title: "romanToArabic"
author: "praconfi"
tags: leetcode
---

# palindromNumber

## my solution
```js
const romanToArabic = (romanNum) =>{
    romanNum = romanNum.toUpperCase()
    let romanNumObj = {"CM": 900,"M": 1000,"CD": 400,"D": 500,"XC": 90,"C": 100,"XL": 40,"L": 50,"IX": 9,"X": 10,"IV": 4,"V": 5,"I": 1,}
    let index = 0,  result = 0;
    for(let i in romanNumObj) {    
        index = romanNum.indexOf(i);
        while(index !== -1) {
            romanNum = romanNum.replace(i, '')
            result += parseInt(romanNumObj[i]);
            index = romanNum.indexOf(i);
        }
    }
    return result ;
} 
```