---
layout: post
title: "Selection sort"
author: "praconfi"
tags: Algorithm
---

# 선택정렬

### 선택정렬은 배열을 정렬하는 알고리즘의 하나이다.  
1. 주어진 배열중에 최소값을 찾는다.
2. 그 값을 맨 앞의 위치한 값과 교체한다.
3. 맨처음 위치를 뺀 나머지 배열을 같은 방법으로 교체한다.

![선택정렬](https://img1.daumcdn.net/thumb/R800x0/?scode=mtistory2&fname=https%3A%2F%2Ft1.daumcdn.net%2Fcfile%2Ftistory%2F256B9C34545081D835)

## 특징
1. 시간 복잡도는 O(n<sup>2</sup>)이다.
2. 알고리즘이 단순하다.
3. 메모리가 제한적인 경우에 사용시 성능상의 이점이 있다.

```js
const selectionSort = (array) => {
    const length = array.length;
    let minIndex, temp;
    for(let i=0; i<length; i++) {
        minIndex = i;
        for(j = i+1; j<length; j++) {
            if(array[j] < array[minIndex]){
                minIndex = j;
            }
        }
        temp = array[minIndex];
        array[minIndex] = array[i];
        array[i] = temp;
    }
    return array;
}
```

# Ref
[선택정렬](https://www.zerocho.com/category/Algorithm/post/57f728c85141fc5fe4f4ca89)
