

# Data Sturcture *Tree* : *Deep Dive*


## Basic of Tree

![](https://i.imgur.com/VmGjzlW.png)

### Terminology
- `Node` : 트리를 구성하는 기본 원소
	- `Root Node` : 트리에서 부모가 없는 최상위 노드, 시작점
	- `Parent Node` : 루트 노드 방향으로 직접 연결된 부모 노드
	- `Child Node` : 루트 노드 반대 방향으로 직접 연결된 자식 노드
	- `Sibling Node` : 같은 부모 노드를 가지는 노드
	- `Leaf Node` : 자식이 없는 노드
	- `Internal Node` : leaf 노드가 아닌 노드
- `Edge` : 노드와 노드를 연결하는 간선
- `Path` : 노드 A to B로 이르는 길 사이에 있는 노드 리스트 (순서)
- `Length` : 출발 노드로 부터 도착까지 가는 간선의 개수
- `Level` : 해당 노드에서부터 루트 경로까지 연결되는 길이
- `Height` : 가장 긴 루트 경로의 길이 (depth)
- `Degree` : 각 노드의 자식의 개수 (차수)
- `Degree Of Tree` : 트리의 최대 차수 (노드들 중 최대 차수)
- `Rooted Tree` : 루트가 정의된 트리
- `UnRooted Tree` : 루트가 정의되지 않은 트리


### Concept
- 트리는 하나의 `Root`를 가진다.
- 트리는 0개 이상의 `Child Node`를 가진다.
-  `Child Node`들 또한 0개 이상의 노드를 가질 수 있다.

부모 노드 밑에 여러 자식 노드가 연결되고, 자식 노드에 다시 자식 노드가 연결되는 **재귀적** 형태의 자료구조. 나무와 비슷한 형태를 보이므로 Tree 구조라고 한다.


## Binaray Tree


**이진 트리**란 자식 노드의 개수 (= 차수)를 **최대 2개로 제한**하는 트리. 루트 노드를 중심으로 2 개의 서브트리로 나뉘어지며 이또한 모두 이진 트리이다.

2개의 자식을 가지므로, 2개의 포인터를 가진 노드들의 연결로 구현될 수 있다.

### Full Binanry Tree 정 이진 트리
- 모든 트리의 노드는 자식을 2개가지거나 가지지 않는다.

### Perfect Binary Tree 포화 이진 트리
- 모든 `leaf node`의 높이가 같고 말단이 아닌 노드는 모두 2개의 자식을 가진다.
- 높이의 최대치가 `N` 이아면 `2^n - 1` 개의 노드를 가진다.
- 포화이진트리는 당연히 정이진트리이다.

### Complete Binary Tree 완전 이진 트리
- 모든 리프노드의 높이가 최대 1 차이
- 자식을 채울 때는 무조건 왼쪽부터

완전 이진 트리는 이와 같은 성질 때문에 **배열을 이용하여 구현** 가능하다. 1번부터 시작하는 인덱스에서
- `N` 번쨰 노드의 왼쪽 자식은 `2N`,
- `N` 번째 노드의 오른쪽 자식은 `2N+1`
- `N` 번째 노드의 부모 노드는 `N//2`

### Traversal in Binary Tree
그리디하게 생각하면된다.
`(왼쪽 자식, 자신, 오른쪽 자식) = (L, M, R)`

- 중위 순회 (In-order) : L M R
- 전위 순회 (Pre-order) : M L R
- 후위 순회 (Post-order) : L R M
- 레벨 순서 순회 (Level-order) : BFS

## Binaray Search Tree (BST)

![](https://i.imgur.com/DqGt44a.png)


### Concept

이진 탐색 트리는 이진 트리의 일종이며 데이터를 저장하는데 특별한 규칙이 있는 형태의 자료구조이다. 이하 BST 

1. BST의 노드에 저장된 키는 유일하다.
2. 부모의 키가 왼쪽 자식 노드의 키보다 크다
3. 부모의 키가 오른쪽 자식 노드의 키보다 작다
4. 왼쪽 / 오른쪽 서브트리 또한 모두 BST이다.

BST의 탐색 / 삽입 / 삭제 시간은 이상적인 경우 모두 `O(log N)`의 시작 복잡도를 가진다. 재귀적으로 현재 위치한 노드를 기준으로 2개의 선택지중에 골라 들어간다. 하지만 이는 well-balance 된 `Skewed Tree`가 아닌 경우에 해당하는 이상적인 경우이다. 최악의 경우 `O(N)` 으로 모든 노드를 LinkedList와 같이 탐색해야할 수 있겠다.

![](https://i.imgur.com/zo2BfQf.png)

```kotlin  
data class Node(
	var value: Int,
	var left: Node? = null,
	var right: Node? = null
)  
  
class BinarySearchTree {  
    private var root: Node? = null  
  
    fun insert(value: Int) {  
        root = insertNode(root, value)  
    }
  
    private fun insertNode(current: Node?, value: Int): Node {  
        current ?: Node(value)

        if (value < current.value) {  
            current.left = insertNode(current.left, value)  
        } else if (value > current.value) {  
            current.right = insertNode(current.right, value)  
        }        return current  
    }  
  
    fun search(value: Int): Node? {  
        return searchNode(root, value)
    }
  
    private fun searchNode(curr: Node?, value: Int): Node? = {  
        if (curr == null || curr.value == value) {  
            return curr  
        }
	    val next = if(value < curr.value) curr.left else curr.right
        return searchNode(next, value)
    }
}
```

-> Kotlin으로 간략하게 구현해본 BST

### Balanced Tree : AVL & Red-Black

AVL 트리와 Red-Black 트리는 모두 자가 균형 BST의 일종으로, 삽입과 삭제 연산 시 트리가 불균형해지는 것을 방지하여 탐색 시간을 최소화 한다.

#### AVL Tree
높이 균형을 유지하는 자가 균형 이진 검색 트리이다. 
- 트리의 각 노드는 왼쪽 서브트리와 오른쪽 서브트리의 높이 차이가 1보다 작거나 같도록 균형을 유지
- AVL 트리에서 삽입과 삭제 연산 시에는 균형을 맞추기 위해 회전 연산을 사용 

AVL 트리는 엄격한 균형을 이루고 있기에 빠른 조회가 가능하다. balancing 하는 경우 각 노드에 대해 BF(balancing point)를 저장하여 균형을 유지하므로 추후 기술할 RB트리에 비해 비용이 든다. 따라서 검색이 많은 경우에 적합하다.

#### Red-Black Tree
각 노드가 '색'이라는 정보를 가진 자가 균형 이진 검색 트리이다.
각 노드는 빨간색 또는 검은색 중 하나의 색을 가지며 아래 5가지 규칙을 따른다.

1.  루트 노드는 검은색이다.
2.  모든 리프 노드는 검은색이다.
3.  어떤 빨간색 노드의 두 자식 노드도 모두 검은색이다.
4.  모든 노드에 대해 해당 노드에서 하위 리프 노드까지의 경로상에 있는 검은색 노드의 수는 모두 같다.
5.  새로 삽입되는 노드는 항상 빨간색이다.

AVL 트리와는 달리 Red-Black 트리는 노드에 색 정보를 추가하여 AVL 트리보다 조금 덜 엄격한 조건을 만족하기 때문에. Red-Black 트리는 삽입과 삭제 연산이 적은 경우에 적합한 자료구조이다.

- Java/Kotlin Collection의 `TreeMap`
- C++ 의 `Map`
자료 구조가 RB 트리로 구현되어있다. (HashTable이 아님)

자세한 로직은 복잡하므로 직접 찾아보는 것을 추천


## Binary Heap

자료구조의 일종으로 Tree 의 형식을 하고 있으며, Tree 중에서도 배열에 기반한 `Complete Binary Tree`를 말한다. 

⚠️ 배열에 트리의 값들을 넣어줄 때, 0 번째는 건너뛰고 1 번 index 부터 루트노드가 시작된다. 

이는 노드의 고유번호 값과 배열의 index 를 일치시켜 혼동을 줄이기 위함 

### Max Heap, Min Heap
`힙(Heap)`에는 `최대힙(max heap)`, `최소힙(min heap)` 두 종류가 있다.

`Max Heap`이란, 각 노드의 값이 해당 children 의 값보다 **크거나 같은** `complete binary tree`를 말한다. ( Min Heap 은 그 반대이다.)

`Max Heap`에서는 Root node 에 있는 값이 제일 크므로, 최대값을 찾는데 소요되는 연산의 time complexity 이 O(1)이다. `Min Heap`도 마찬가지.

그리고 `complete binary tree`이기 때문에 배열을 사용하여 효율적으로 관리할 수 있다. (즉, random access 가 가능하다. 하지만 heap 의 구조를 계속 유지하기 위해서는 제거된 루트 노드를 대체할 다른 노드가 필요하다. 여기서 heap 은 맨 마지막 노드를 루트 노드로 대체시킨 후, 다시 **heapify** 과정을 거쳐 heap 구조를 유지한다. 

이런 경우에는 결국 O(log n)의 시간복잡도로 최대값 또는 최소값에 접근할 수 있게 된다.

## Segment Tree

세그먼트 트리는 **구간 합**을 빠르게 구하기 위한 자료구조이다. 

구간 합을 구하는 것은 배열에서 특정 구간의 원소들의 합을 계산하는 것으로, 이진 트리의 형태의 세그먼트 트리를 사용하면 배열에서 어떤 구간의 합을 `O(log n)`의 시간 복잡도로 빠르게 계산할 수 있음

### how?
- 각 노드는 해당 노드가 커버하는 구간의 합을 저장
- 루트 노드는 전체 배열의 구간 합을 저장
- 각 노드의 자식 노드는 해당 노드의 구간을 반으로 나눈 뒤 각각의 구간 합을 저장

원하는 구간안에 있는 최상위의 노드들의 값들을 더함으로써 빠르게 구간합을 구할 수 있다.

또한, lazy propagation 기법을 사용하여 업데이트 연산의 시간 복잡도를 O(log n)으로 줄일 수 있다고 함.