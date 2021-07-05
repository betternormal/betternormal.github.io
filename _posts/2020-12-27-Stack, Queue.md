---
layout: post
author: "praconfi"
title: "Stack, Queue"
date: 2020-12-27 11:25
categories: DataStructure 
tags: DataStructure
---



스택과 큐는 실생활에서도 흔히 볼 수 있는 형태의 자료구조로 간단한 자료구조이다.

서로 비슷하면서도 다른 쌍둥이같은 두 자료구조는 간단한 만큼 많은 부분에서 활용되기 때문에 중요하다.

### **1. Stack**
![Untitled (2)](https://user-images.githubusercontent.com/64571546/103162556-6cc13500-4835-11eb-9495-135e1ee697de.png)

Stack이란 LIFO(Last In First Out)에 따라 동작하는 동적인 데이터 구조를 의미한다. 가장 늦게 추가된 자료가 가장 먼저 나가게된다.

예를들면 접시 더미와 같다. 새로운 접시가 쌓일 때도 맨 위에서 쌓이고, 접시를 가져갈 때도 맨 위에서 가지고 가는 것과 같습니다.

 

### 1. 배열을 이용한 스택

배열을 사용하기 위해서는 먼저 크기를 정해서 생성해야 한다.

배열 에는 연속적인 인덱스가 존재하는데 인덱스는 0부터 1,2,3..으로 배열의 크기 미만까지 새로운 요소가 들어올때마다 늘어나게 된다.

스택을 만들때는 마지막 요소를 가리키는 무언가가 있으면 좋은데 그 역할을 '포인터' 라는것이 한다.

자료를 배열에 추가하고 뺄 때마다 포인터를 이용해서 어느위치에 추가해야 하는지, 어느위치에서 빼야하는지 알 수 있다.

### 2. 연결리스트를 이용한 스택

연결리스트는 이어져있다. 머리(Head)에서 시작해서 다음 노드를 향하는 포인터를 통해서 이어져 있는것이 특징이다. 연결리스트에서는 새로 추가되는 요소가 맨뒤 꼬리(Tail)에 붙는다. 이대로 사용해서 꼬리를 제거 할 수도 있지만 그렇게되면 바로접근하기가 어려워진다. 

그렇기 때문에 연결리스트를 이용해 스택을 구현할 때는 역순으로 새로운 요소를 추가할 때마다 머리(Head)에 붙여야 한다. 그렇게되면 머리를 제거하면 다음노드가 머리가 된다. 순환해서 꼬리를 찾아야 할 필요가 없어진다.

![_2020-12-23__7 21 16](https://user-images.githubusercontent.com/64571546/103162571-a2feb480-4835-11eb-80f3-2b4a6e124575.png)


![Untitled (3)](https://user-images.githubusercontent.com/64571546/103162581-b6aa1b00-4835-11eb-970a-eaa5052e4a17.png)


Methods

- `push(element)` - 요소를 스택의 최상단에 추가한다.
- `pop()` - 스택의 최상단에서 요소를 제거하고 반환한다.
- `size()` - 스택의 현재 요소 개수를 반환한다.

```jsx
class Stack {
  constructor() {
    this.storage = {};
    this.top = -1;
  }

  size() {
    return this.top + 1;
  }

  push(element) {
    this.top += 1;
    this.storage[this.top] = element;
  }

  pop() {
    if (this.size() <= 0) {
      return;
    }

    const result = this.storage[this.top];
    delete this.storage[this.top];
    this.top -= 1;
    
    return result;
  }
}

module.exports = Stack;
```

### **2. Queue**
![Untitled (4)](https://user-images.githubusercontent.com/64571546/103162593-e0634200-4835-11eb-87e6-5237e8b3d948.png)
큐는 FIFO(First In First Out) 구조로 데이터를 저장하는 방식이다. 가장 먼저 저장된 자료가 가장먼저 나간다. 

예를들면 매장 앞에 서는 줄과 같이 작동한다. 사람들이 맨 끝에 줄을 서고, 맨 앞에서부터 매장에 들어가는 것과 같다.
![_2020-12-23__7 21 36](https://user-images.githubusercontent.com/64571546/103162595-e2c59c00-4835-11eb-8dd4-a536bde3eac9.png)
![Untitled (5)](https://user-images.githubusercontent.com/64571546/103162596-e48f5f80-4835-11eb-9b87-12790481e7de.png)


### Methods

- `enqueue(element)` - 요소를 큐의 뒤에 추가합니다.
- `dequeue()` - 요소를 큐의 앞에서 제거하고 반환합니다.
- `size()` - 큐의 현재 요소 개수를 반환합니다.

```jsx
class Queue {
  constructor() {
    this.storage = {};
    this.front = 0;
    this.rear = 0;
  }

  size() {
    return this.rear - this.front;
  }

  enqueue(element) {
    this.storage[this.rear] = element;
    this.rear += 1;
  }

  dequeue() {
    if (this.size() === 0) {
      return;
    }

    const result = this.storage[this.front];
    delete this.storage[this.front];
    this.front += 1;

    return result;
  }
}

module.exports = Queue;
```

> ## 스택과 큐의 차이점
- 스택은 최상단 에서만 자료의 추가 및 삭제가 이루어 지지만 큐는 앞쪽에서 자료가 꺼내지고, 뒤에서 새로운 자료가 추가된다.

- 스택 에서는 가장 마지막으로 추가된 자료만 알려주면 되지만 큐는 맨앞에 있는 자료를 알려주면 된다. 

- 큐에는 들어오는 곳과 나가는 곳의 위치가 다를수도 있다. 그래서 스택과 달리 이를 가리키는 포인터가 두개 필요할 수 있다.
