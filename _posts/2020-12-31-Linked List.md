---
layout: post
author: "praconfi"
tags: DataStructure
title: "Linked List"
---
# summary
Linked List는 자료구조의 하나로써 여러개의 값을 저장하기 위한 구조이다.  
여러개의 노드가 선형적으로 이어저 있는 구조이며 각 노드는 `데이터(value)`와 다음 노드의 `주소값(pointer)`으로 구성되어 있다.  
배열과는 다르게 데이터들이 메모리상의 떨어진 영역에 `흩어져서` 저장된다. 그렇기 때문에 원하는 데이터에 접근하기 위해서는 처음부터 순서대로 따라가야 한다.  
노드 추가시에는 추가할 위치에서 앞뒤 노드의 포인터값을 변경함으로써 이어지게 할 수 있다.  
노드 삭제시에도 삭제할 노드의 전 노드의 포인터를 삭제노드 다음노드로 변경하면 된다. 사용되어지지 않는 노드는 가비지 컬렉션에 의해 메모리 해제가 된다.  
|Access|Search|Insert|Delete|  
|------|---|---|---|  
|O(n)|O(n)|O(1)|O(1)|  



![Linked List](https://user-images.githubusercontent.com/64571546/103385080-56b8ba80-4b3c-11eb-9966-c929d23fb98f.png)



# 구조
![Untitled (8)](https://user-images.githubusercontent.com/64571546/103385088-5c160500-4b3c-11eb-93ea-76f2018abfd2.png)

#  vs 배열

배열은 데이터들이 물리적인 배열에 모여있는데 반해 연결리스트는 주소값으로 연결되어 있어 메모리의 연속된 위치에 저장되지 않아도 되며, 일반적으로 떨어진 영역에 흩어져서 저장된다.   
[**조회**] 배열은 각 데이터들의 주소가 정해져있기 때문에 속도가 빠르지만(**O(1)**) 연결리스트는 첫노드부터 차례대로 확인해 봐야하기 때문에 느리다(**O(n)**).

[**추가, 삭제**] 배열은 새로운 배열은 만들고 기존값을 옮기고 추가해야 하지만(**O(n)**) 연결리스트는 원하는 위치에 앞뒤노드들의 주소값만 수정하면 되기때문에 빠르(**O(1)**).

# Garbage Collection
연결리스트에서 중간의 노드를 제거할 때 연결을 끊게 되는데, 그때 사용되지 않는 노드는 가비지컬렉션에 의해 메모리해제가 된다.  
C, C++과 같은 언어에서는 직접 선언해야 하지만 자바스크립트에서는 가비지컬렉션이 아무도 참조하지 않은 메모리를 제거한다.


# 사용예시
- **음악 플레이리스트**: 음악을 들을 때 보통 플레이리스트로 듣고싶은 음악을 특정 순서대로 듣는다. 한곡씩 듣게되고 끝나면 다음곡으로 넘어간다. 

# 구현

![_2020-12-23__7 35 46](https://user-images.githubusercontent.com/64571546/103385092-5fa98c00-4b3c-11eb-88c9-a31b02051792.png)


- `addToTail(value)` - 주어진 값을 연결 리스트의 끝에 추가합니다.
- `remove(value)` - 주어진 값을 찾아서 연결을 해제(삭제)합니다
- `getNodeAt(index)` - 주어진 인덱스의 노드를 찾아서 반환합니다. 값이 아니라 노드를 반환해야 하는 것에 주의하세요. 해당 인덱스에 노드가 없다면 undefined를 반환합니다.
- `contains(value)` - 연결리스트에 주어진 값을 가지는 노드의 존재 여부를 반환합니다.
- `indexOf(value)` - 주어진 값의 인덱스를 반환합니다. 없을 경우 -1을 반환합니다.

```jsx
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class LinkedList {
  constructor() {
    this.head = null;
    this.tail = null;
    this._size = 0;
  }

  addToTail(value) {
    const newNode = new Node(value);

    if (this.head === null) {
      this.head = newNode;
      this.tail = newNode;
    } else {
      this.tail.next = newNode;
      this.tail = newNode;
    }

    this._size += 1;
  }

  remove(value) {
    const index = this.indexOf(value);
    if (index === -1) {
      return;
    }

    if (index === 0) {
      if (this.head === this.tail) {
        this.head = null;
        this.tail = null;
        this._size = 0;
      } else {
        this.head = this.head.next;
        this._size -= 1;
      }

      return;
    }

    const prevNode = this.getNodeAt(index - 1);
    const removedNode = prevNode.next;

    if (removedNode === this.tail) {
      prevNode.next = null;
      this.tail = prevNode;
      this._size -= 1;
      return;
    }

    prevNode.next = removedNode.next;
    this._size -= 1;
  }

  getNodeAt(index) {
    let counter = -1;

    let currentNode = this.head;
    while (currentNode) {
      counter += 1;
      if (index === counter) {
        return currentNode;
      }
      currentNode = currentNode.next;
    }

    return undefined;
  }

  contains(value) {
    return this.indexOf(value) !== -1;
  }

  indexOf(value) {
    let index = 0;

    let currentNode = this.head;
    while (currentNode) {
      if (currentNode.value === value) {
        return index;
      }
      index += 1;
      currentNode = currentNode.next;
    }

    return -1;
  }

  size() {
    return this._size;
  }
}

module.exports = LinkedList;
```
      
# Circular Linked List
![circular-linked-list](https://user-images.githubusercontent.com/64571546/127334240-496c0711-a56d-48d1-84df-29e7c54aef03.png)

리스트의 마지막 데이터가 선두의 데이터를 가리키도록 하면 리스트가 원형으로 연결된다. 이것을 '원형리스트' 또는'순환리스트'라고 한다. 원형리스트에는 선두나 후미라는 개념이 없다.
# Doubly Linked List 

![Untitled (9)](https://user-images.githubusercontent.com/64571546/103385096-62a47c80-4b3c-11eb-9aaf-0372a2402677.png)

이중연결리스트는 단일연결리스트에 포인터가 하나 더 있다는점에서 다르다.

이전노드를 가리키는 포인터, 다음 노드를 가리키는 포인터들을 통해 양방향으로 순환할 수 있다.

이전노드로 갈수있어서 좋긴하지만 그만큼 메모리 공간도 조금 더 차지한다. 

# Ref.
https://youtu.be/DzGnME1jIwY