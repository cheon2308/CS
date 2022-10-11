지금까지는 단순 구조, 선형 구조에 대해서 알아보았다.

이번 글에서는 **'비선형 구조'** 중 하나인 **'트리'**에 대해 알아보자!

#### **목차**

1. 개념 및 정의

2. 이진트리

3. 순회

4. 표현 및 저장

5. 연결 리스트

---

### **1. 개념 및 정의**

> **개념**

-   비선형 구조
-   원소들 간에 **1 : N** 관계를 가지는 자료구조이다.ㅣ
-   또한 원소들 간 **계층 관계를** 가지는 **계층형 자료구조**
-   상위 원소에서 하위 원소로 내려가며 확장되는 나무(트리) 모양의 구조

> **정의**

-   한 개 이상의 노드로 이루어진 **유한 집합**
    -   노드 중 최상위 노드 -> **루트(root)**
    -   나머지 노드들은 n개의 **분리 집합** T1... TN으로 분리될 수 있다.
-   이들 T1... TN은 각각 하나의 트리가 되며(재귀적 정의) 루트의 **부 트리(subtree)**라 한다.

![](https://blog.kakaocdn.net/dn/bfzD01/btrLYlLMv8v/yH2pj7IHxgFCkbcBkHEjX1/img.png)

> **용어 정리**

1.  **노드(node)**
    -   트리의 원소
    -   위의 경우 트리 T의 노드 - A, B, C, D, E, F, G, H, I, J, K
2.  **간선(edge)**
    -   노드를 연결하는 선으로서 **부모 노드**와 **자식 노드를 연결**
3.  **루트 노드(root node)**
    -   트리의 시작 노드
4.  **형제 노드(sibiling node)**
    -   같은 부모 노드의 자식 노드들
    -   B, C, D는 형제 노드
5.  **조상 노드**  
    -   간선을 따라 루트 노드까지 이르는 경로에 있는 모든 노드들
    -   K의 조상 노드 - F, B, A
6.  **서브 트리(subtree)**
    -   부모 노드와 연결된 간선을 끊었을 때 생성되는 트리
7.  **자손 노드**
    -   서브 트리에 있는 하위 레벨의 노드들
    -   B의 자손 노드 - E, F, K
8.  **차수(degree)**  
    -   **노드의 차수**
        -   노드에 연결된 자식 노드의 수
        -   B의 차수 = 2, C의 차수 =1
    -   **트리의 차수** 
        -   트리에 있는 노드의 차수 중에서 가장 큰 값
        -   트리 T의 차수 = 3
    -   **단말 노드(리프 노드)**
        -   차수가 0인 노드, 즉 자식 노드가 없는 노드
9.  **높이 (레벨)**
    -   **노드의 높이**
        -   루트에서 노드에 이르는 간선의 수, 노드의 레벨
        -   B의 높이 = 1, F의 높이 = 2
    -   **트리의 높이**  
        -   트리에 있는 노드의 높이 중에서 가장 큰 값, 최대 레벨
        -   트리 T의 높이 = 3

![](https://blog.kakaocdn.net/dn/bIBNje/btrL3Aah67x/OEzyhiXbPzGtQlRGBaOHqk/img.png)

---

### **2. 이진트리**

> **개념**

-   모든 노드들이 **2개의 서브 트리를 갖는 특별한 형태의** 트리
-   각 노드가 **자식 노드를 최대한 2개**까지만 가질 수 있는 트리
    -   왼쪽 자식 노드(left child node)
    -   오른쪽 자식 노드(right child node)

![](https://blog.kakaocdn.net/dn/cOPNUr/btrLWlFjwj3/t7pVkJ3kxXkl02K08QMm7K/img.png)

> **특성  
> **

-   레벨 i에서의 노드의 최대 개수는 **2**i**
-   높이가 h인 이진트리가 가질 수 있는 노드의 **최소 개수 = (h+1), 최대 개수 (2^(h+1) -1)**

> **종류**

**1. 포화 이진트리(Full Binary Tree)**

-   모든 레벨에 노드가 **포화상태**로 차 있는 이진 트리
-   높이가 h일 때, 최대의 노드 개수인 **(2^(h+1) -1)**의 노드를 가진 이진 트리
-   루트를 1번으로 하여 **(2^(h+1) -1)까지** 정해진 위치에 대한 노드 번호를 가짐

![](https://blog.kakaocdn.net/dn/I38uN/btrLZyRQS2p/D6yydR9wKQHxMkcWQuO4P0/img.png)

**2. 완전 이진트리(Complete Binary Tree)**

-   높이가 h이고 노드 수가 n개일 때 (단, h+1 <= n < 2^(h+1)-1), 포화 이진트리의 **노드 번호 1번부터 n번까지 빈자리가 없는 이진트리**

![](https://blog.kakaocdn.net/dn/pL2JB/btrLZQSmi3m/nV23LQTTyI5nlbQS9KKP00/img.png)

노드가 10개인 완전 이진 트리

**3. 편향 이진트리(Skewed Binary Tree)**

-   높이 h에 대한 최소 개수의 노드를 가지면서 한쪽 방향의 자식 노드만을 가진 이진 트리

![](https://blog.kakaocdn.net/dn/vNWFL/btrL43WYln9/82o63QKXhKKOD3YKx0hYf1/img.png)

왼쪽 편향과 오른쪽 편향

**4. 수식 트리**

-   수식을 표현하는 이진 트리
-   **수식 이진트리(Expression Binary Tree)**라고 부르기도 한다.
-   **연산자**는 **루트 노드**이거나 **가지 노드**
-   **피연산자**는 모드 **리프 노드**

![](https://blog.kakaocdn.net/dn/JEhF5/btrL4avw1oN/PJMas5HCBUTmPHrwEK3hK0/img.png)

---

### **3. 순회(traversal)**

-   트리의 각 노드를 **중복되지 않게 전부 방문(visit)**하는 것을 말하는데 트리는 **비 선형 구조**이기 때문에 선형구조에서와 같이 **선후 연결 관계**를 알 수 없다.
-   즉, 트리의 노드들을 **체계적으로 방문**하는 것
-   3가지의 기본적인 순회 방법
    1.  **전위 순회(preorder traversal) : VLR**
        -   부모 노드 방문 후, 자식 노드를 좌, 우 순서로 방문
    2.  **중위 순회(inorder traversal) : LVR**
        -   왼쪽 자식 노드, 부모노드, 오른쪽 자식노드 순으로 방문
    3.  **후위 순회(postorder traversal) : LRV**
        -   자식 노드를 좌우 순서로 방문한 후, 부모 노드로 방문

![](https://blog.kakaocdn.net/dn/dtGiJ9/btrL43WYzkl/ljxYCuFGYLziVoan3DK0RK/img.png)

> **전위 순회(preorder traversal)**

1.  현재 노드 n을 방문하여 처리 -> V
2.  현재 노드 n의 왼쪽 서브 트리 이동 -> L
3.  현재 노드 n의 오른쪽 서브 트리로 이동 -> R

![](https://blog.kakaocdn.net/dn/bSyDjh/btrL2m4xwWk/iZPBixvErkLDj5s6khqzv1/img.png)

![](https://blog.kakaocdn.net/dn/bpsgQf/btrL1z31nIx/nsPcKNA458ie9uUI31M0w0/img.png)

    순서 1 : T0 - T1 - T2

    순서 2 : A - B D (T3) - C F G

    총 순서 : A B D E H I C F G

> **중위 순회(inorder traversal)**

1.  현재 노드 n의 왼쪽 서브 트리로 이동 ->  L
2.  현재 노드 n을 방문하여 처리 -> V
3.  현재 노드 n의 오른쪽 서브트리로 이동 -> R

![](https://blog.kakaocdn.net/dn/1nsjx/btrL22LDe3J/vmHIkAvtnI2bUsFXiVEYUk/img.png)

![](https://blog.kakaocdn.net/dn/EHtZa/btrL5RhHCxN/u7bGGarWKScN5eGMgSMk60/img.png)

    순서 1 : T1 - T0 - T2

    순서 2 : D B (T3) - A - F C G

    총 순서 : D B H E I A F C G

> **후위 순회(postorder traversal**

1.  현재 노드 n의 왼쪽 서브 트리로 이동 -> L
2.  현재 노드 n의 오른쪽 서브트리로 이동 -> R
3.  현재 노드 n을 방문하여 처리 -> V

![](https://blog.kakaocdn.net/dn/cnWumA/btrL34Wwfak/MNh6q5BkUidK9xbaS4yrj1/img.png)

![](https://blog.kakaocdn.net/dn/dEzjns/btrL1zCYIMU/rEzaW6sRKn9XRmTaAzK7P0/img.png)

    순서 1 : T1 - T2 - T0

    순서 2 : D (T3) B - F G C - A

    총 순서 : D H I E B F G C A

```
import sys
sys.stdin = open('input.txt')

def preorder(node):
    # 해당 노드가 있으면
    if node:
        print(f'{node}', end=' ')
        # 해당 노드의 왼쪽 조사
        preorder(tree[node][0])
        # 해당 노드의 오른쪽 조사
        preorder(tree[node][1])

def in_order(node):
    # 해당 노드가 있으면
    if node:
        # 해당 노드의 왼쪽 조사
        in_order(tree[node][0])
        print(f'{node}', end=' ')
        # 해당 노드의 오른쪽 조스
        in_order(tree[node][1])

def post_order(node):
    # 해당 노드가 있으면
    if node:
        # 해당 노드의 왼쪽 조사
        post_order(tree[node][0])
        # 해당 노드의 오른쪽 조스
        post_order(tree[node][1])
        print(f'{node}', end=' ')

# 각 노드의 수
V = int(input())
# 간선의 수
E = V-1

# 간선 정보
arr = list(map(int, input().split()))
print(arr)
'''
1번 노드
- 왼쪽 : 2번
- 오른쪽 : 3번
- 부모 : 없음

2번 노드
- 왼쪽 : 4번
- 오른쪽 : 없음
- 부모 : 1번

3번 노드
- 왼쪽 : 5번
- 오른쪽 : 6번
- 부모 : 1번
'''
tree = [[0,0,0] for _ in range(V+1)]
print(tree)
# 간선의 개수 만큼 반복해서
for i in range(E):
    parent, child = arr[i*2], arr[i*2+1]
    # print(parent, child)
    # parent가 부모일때 왼쪽, 오른쪽 자식
    # 아직 왼쪽 자식이 없다면
    if tree[parent][0] == 0:
        tree[parent][0] = child
    else:
        tree[parent][1] = child
    # 자식 노드에 부모 값 추가
    tree[child][2] = parent
```

#### **# 수식 트리의 순회**

![](https://blog.kakaocdn.net/dn/CBfks/btrL4bnJqow/KcaD4GrB529E2QlwwvmFJ0/img.png)

    중위 순회 : A / B * C + D + E (수식의 중위 표기법)

    후위 순회 : A B / C * D * E + (수식의 후위 표기법)

    전위 순회 : + * * / A B C D E (수식의 전위 표기법)

---

### **4. 표현 및 저장**

> **표현**

이진트리의 표현 같은 경우는 파이썬에서는 **배열**을 이용하여 할 수 있다.

-   이진 트리에 각 노드 번호를 다음과 같이 부여
-   루트의 번호를 1로 함
-   레벨 n에 있는 노드에 대하여 왼쪽부터 오른쪽으로 **2^n부터** **2^(n+1)-1**까지 번호를 차례대로 부여
-   즉 노드의 번호를 인덱스로 사용하는 것이다.

![](https://blog.kakaocdn.net/dn/4b4bc/btrL34WwsFf/KXVDHeJe8Sd68iqjnObKPk/img.png)

> ****노드 번호의 성질****
> 
> ![](https://blog.kakaocdn.net/dn/0ARlf/btrL4A8zSKT/PJ8PgkmByTV8F8HVzXLiuK/img.png)

-   노드 번호가 i인 노드의 부모 노드의 번호는?   
    -   i // 2
-   노드 번호가 i인 노드의 왼쪽 자식 노드 번호?
    -   2 * i
-   노드 번호가 i인 노드의 오른쪽 자식 노드 번호?
    -   2 * i + 1
-   레벨 n의 노드 번호 시작 번호는?
    -   2^n

![](https://blog.kakaocdn.net/dn/dTUYuQ/btrL4b817nB/o0CMGeLFXSXzOnSoklJKhk/img.png)

-   높이가 h인 이진트리를 위한 배열의 크기
    -   레벨 i의 최대 노드 수는 **2 ^ i**
    -   따라서 1 + 2 + 4 +.. + 2^i  = 2 ^ (h+1) -1  -> 포화 이진트리의 노드 수와 동일하게 만들어 주면 된다.

![](https://blog.kakaocdn.net/dn/evQr3j/btrLYj8tE9O/Us3leHxXXxBdlCelBqE1N0/img.png)

![](https://blog.kakaocdn.net/dn/dTNpuD/btrL4abddeY/KREzy7gp2LkBuvrRsQ8EW0/img.png)

위와 같이 완전 이진 트리의 경우에도 사용하지 않는 메모리가 발생하는데 아래와 같은 편향 이중 트리의 경우 낭비가 더 심해진다.

![](https://blog.kakaocdn.net/dn/sczme/btrL3EcFBn8/UsYHO45PB3WjeZJq2TD2Zk/img.png)

> **저장**

앞서 살펴봤던 순회의 코드를 입력하며 미리 **이진 트리의 저장**에 대해서 볼 수 있었다.

1.  부모 번호를 인덱스로 자식 번호를 저장
2.  자식 번호를 인덱스로 부모 번호를 저장

![](https://blog.kakaocdn.net/dn/d6YaI2/btrL1yD0eSB/IicymneKQw3cUcKV9Hau51/img.png)

1번

![](https://blog.kakaocdn.net/dn/bZyC6M/btrL5SVdZoQ/qRuDEhnA2AfzkRphUIBIUK/img.png)

2번

따로 이루어지는 것이 아닌 [ 0,0,0 ]의 배열에서 **왼쪽 자식 노드 번호, 오른쪽 자식 노드 번호, 부모의 번호**가 되는 것!!!

루트 또는 조상을 찾기 위해서는 **자식의 인덱스에서 부모 번호를 추출, 새로운 리스트에 저장한 후 꼬리 물기로 이어나가면 된다.** dfs에서 경로를 찾는 것과 비슷한 원리이다.

다만, 배열을 이용하여 이진트리를 표현한다면

1.  편향 이진트리의 경우 사용하지 않는 배열 원소에 대한 메모리 공간 낭비 발생
2.  트리의 중간에 새로운 노드를 삽입하거나 기존의 노드를 삭제할 경우 배열의 크기 변경이 어려워 비효율적

2가지의 단점이 존재한다.

이런 단점을 보완하기 위하여 **연결 리스트(Linked List)를** **이용**하지만 파이썬에서는 따로 구현해주어야 하기 때문에 사용하지 않는 것 같기 때문에 살짝만 보고 넘어가자.

---

### **5. 연결 리스트를 이용한 트리의 표현**

-   이진트리의 모든 노드는 최대 2개의 자식 노드를 가지므로 일정한 구조의 **단순 연결 리스트 노드를 사용**하여 구현

![](https://blog.kakaocdn.net/dn/tu2AO/btrLZQrqskr/rOWl8zfUknNzECLrhDbqKk/img.png)

![](https://blog.kakaocdn.net/dn/djiXVo/btrL1yxhvI4/skyMlknqzF49B5663iffiK/img.png)