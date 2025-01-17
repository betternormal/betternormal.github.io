---
layout: post
author: "praconfi"
tags: DataStructure
title: "Binary Search Tree"
---
# summary
### 이진탐색트리는 두가지 성질을 가지고 있다.  
1. 모든 노드는 왼쪽가지에 포함되는 어떤 숫자보다도 큰 숫자가 된다.  
2. 모든 노드는 그 노드의 오른쪽 가지에 포함되는 어떤 숫자보다 작은 숫자가 된다.  
### 이 두개의 성질로부터 다음 조건이 성립된다.
- 이진 탐색트리의 `최소노드`는 최상단에 있는 노드로부터 `왼쪽` 가지만 따라가면 나오는 가장끝에 있는 노드가 된다.  
- `최대노드`는 최상단의 노드로부터 `오른쪽` 가지만 계속 따라가면 가장 끝에 있는 노드가 된다.  
이진탐색트리를 사용하면 효율적인 탐색이 가능하지만, 트리가 직선에 가까운 형태가 되면 선형탐색과 마찬가지로 탐색효율이 나빠진다.

### Big O

- balanced binary search tree: `O(log(n))`  
- unbalanced binary search tree `O(n)`  
    최악의 경우 연결리스트와 같은 구조가 된다


# Binary Search Tree

이진탐색트리는 최대 2개의 자식만 갖는 트리이다. 트리구조는 재귀적이므로 자식노드 역시 최대 2개의 자식을 갖는다. 이진 탐색 트리에서는 노드의 값이 정렬 방법에 따라 순서가 존재한다. 노드의 왼쪽 서브트리에는 노드의 값보다 작은값이, 오른쪽 서브트리에는 노드의 값과 같거나 큰값이 존재한다.

![Untitled (4)](https://user-images.githubusercontent.com/64571546/104245953-8191ff80-54a8-11eb-9f89-a766d77cb652.png)


이진탐색트리를 순회하는 방법은 크게 `깊이우선탐색(DFS, Depth-First-Search)`과 `너비우선탐색(BFS, Breadth-First-Search)`알고리즘이 존재한다.

## 사용예시
- 분류알고리즘이나 데이터베이스 인덱스, JPEG 인코더 등..  
- 데이터베이스 인덱스는 빠른 탐색을 위해 이중탐색 트리를 활용하고 있다.  
- JPEG인코더는 허프만 코딩(Huggman Coding)을 활용하는데 허프만 코딩은 이중 탐색 트리를 활용한다.  
- 트리보다 빠르게 필요한 자료를 꺼내올 수 있다.

### 이진 탐색 트리의 특징
1. 트리의 각 노드가 갖는 자식노드의 수가 2개 이하가 되어야 한다.
2. 모든 노드는 왼쪽 가지에 포함되는 어떤 숫자보다 큰 숫자가 된다.
3. 모든 노드는 오른족 가지에 포함되는 어떤 숫자보다 작은 숫자가 된다.  
    => 위 특징으로부터 성립되는 조건
  - 이진탐색트리의 최소노드는 왼쪽가지의 끝에 있다.  
  - 이진탐색트리의 최대노드는 오른쪽가지의 끝에 있다.  

## 조회, 추가, 삭제
 
1. 추가: 노드 추가위치를 최상단 노드부터 탐색해나간다. 추가하려는값이 현재노드보다 작으면 왼쪽, 크면 오른쪽으로 이동한다.
2. 삭제: 자식노드가 없는 노드는 대상노드만 삭제하면 된다. 자식노드가 하나인경우노드를 삭제하고 자식노드를 이동시킨다. 자식노드가 두개인 경우 삭제된 자리에 왼쪽가지에서의 최대노드를 이동시킨다.
3. 탐색: 최상단 노드부터 값을 비교하면서 왼쪽, 오른족으로 탐색해나간다. 트리의 높이만큼 비교하기때문에 노드가 n개 이고 트리가 균형잡힌 경우라면 최대log2n회의 비교로 이동할 수 있다. 그래서 시간복잡도는 O(log n)이 된다. 단, 트리가 한쪽으로 치우쳐서 직선에 가까운 모양인 경우에는 O(n)이 될 수 있다.

## 이진탐색트리의 순회방법

### 1. DFS(깊이 우선 탐색, Depth-First Search)

![Untitled (5)](https://user-images.githubusercontent.com/64571546/104245981-8d7dc180-54a8-11eb-9300-8e0fee1e7a87.png)
루트를 시작으로 깊이 들어갔다가, 가장깊은 depth에 도달했을 때 다시 나오고 또 다시 다른 노드를 깊이 들어가는 방식을 반복하며 전체 트리를 순회한다.  
  

### 2. BFS(너비 우선 탐색, Breadth-First Search)
![Untitled (6)](https://user-images.githubusercontent.com/64571546/104246006-95d5fc80-54a8-11eb-8aff-3795799a8a7a.png)
sibling을 먼저 탐색하고, 그 후 다음 depth로 들어가 해당 depth의 sibling을 탐색하는 방식으로 전체 트리를 순회한다.


### 종류
- 정 이진 트리(Full Binary Tree)  
- 완전 이진 트리(Complete Binary Tree)  
- 포화 이진 트리(Perfect Binary Tree)  
- 

### 탐색방법
- 전위 순회(Preorder Traversal): 부모 → 좌 → 우  
- 중위 순회(Inorder Traversal): 좌 → 부모 → 우  
- 후위 순회(Postorder Traversal): 좌 → 우 → 부모  
   

## Methods
- `insert(value)` - 이진 탐색 트리에 노드를 추가합니다.
- `contains(value)` - 이진 탐색 트리에 해당 노드가 존재하는지 여부를 반환합니다.
- `inorder(callback)` - 이진 탐색 트리를 중위순회 합니다.

```js
class BinarySearchTreeNode {
    constructor(value) {
    this.value = value;
    this.left = null;
    this.right = null;
    }

    insert(value) {
    if (value < this.value) {
        if (this.left === null) {
        this.left = new BinarySearchTreeNode(value);
        } else {
        this.left.insert(value);
        }
    } else if (value > this.value) {
        if (this.right === null) {
        this.right = new BinarySearchTreeNode(value);
        } else {
        this.right.insert(value);
        }
    } else {
        // do nothing: The tree already contains this value
    }
    }

    contains(value) {
    if (value === this.value) {
        return true;
    }
    if (value < this.value) {
        return !!(this.left && this.left.contains(value));
    }
    if (value > this.value) {
        return !!(this.right && this.right.contains(value));
    }
    }

    inorder(callback) {
    if (this.left) {
        this.left.inorder(callback);
    }
    callback(this.value);
    if (this.right) {
        this.right.inorder(callback);
    }
    }
}

module.exports = BinarySearchTreeNode;
```

## Ref
 [Binary Search Tree](http://en.wikipedia.org/wiki/Binary_search_tree)