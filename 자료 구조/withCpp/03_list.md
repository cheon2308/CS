

> **list**

-   연결리스트
-   요소가 **인접한 메모리 위치에 저장 xxx**인 **선형 데이터 구조**
-   요소들은 **next, prev**라는 **포인터로 연결**되어 이루어지고
-   **중복을 허용**

![](https://blog.kakaocdn.net/dn/bj9h00/btr0yimFOog/XzjzwZjnwS50USAZi7xXQk/img.png)

> **시간복잡도**

-   데이터를 감싼 **노드**를 **포인터****로 연결**해서 **공간적인 효율성을 극대화**시킨 자료구조
-   삽입과 삭제 **O(1)**
-   k번째 요소를 참조한다 했을 때 **O(k)**

> **노드**

-   노드는 아래와 같이 이루어져 있다.
    -   (싱글연결리스트 기준) **data**
    -   노드와 노드를 잇게 만드는 **next라는 포인터** 

```cpp
class Node {
public:
	int data;
    Node* next;
    Node(){
        data = 0;
        next = NULL;
    }
    Node(int data){
        this->data = data;
        this->next = NULL;
    }


};
```

> **분류**

크게 3가지로 나뉜다.

-   **싱글 연결 리스트(Singly Linked List)** 
    -   **next 포인터** 밖에 존재하지 않으며 **한 방향**으로만 **데이터가 연결**된다.

![](https://blog.kakaocdn.net/dn/N8h0d/btr0uwTCpG5/Zth7xDI9fHAAKBvryOcMEK/img.png)

-   **이중 연결 리스트(Doubly Linked List)**  
    -   **prev, next** 두개의 포인터로 **양방향**으로 **데이터가 연결**된다.

![](https://blog.kakaocdn.net/dn/T62Si/btr0yIrUqTW/rATBH1Kq5ipRt9Op1Yk5WK/img.png)

-   **원형연결리스트(Circular Linked List)**  
    -   마지막 노드와 첫번재 노드가 연결되어 원을 형성
    -   싱글연결리스트 또는 이중연결리스트로 이루어진 2가지 타입의 원형연결리스트 

![](https://blog.kakaocdn.net/dn/bl5Eok/btr0xPyx4My/w6WKbH5hx82xWThx5fB4e0/img.png)

![](https://blog.kakaocdn.net/dn/DLy5x/btr0AOrOzJl/JMg7mqH22fVgNjRDkyvNK1/img.png)

> **예시코드**

```cpp
#include <bits/stdc++.h>
using namespace std;
list<int> a;
void print(list <int> a){
    for(auto it : a) cout << it << " ";
    cout << '\n';
}
int main(){
    for(int i = 1; i <=3; i++)a.push_back(i);
    for(int i = 1; i <=3; i++)a.push_front(i);
    
    auto it = a.begin(); it++;
    a.insert(it, 1000);
    print(a);
    
    it = a.begin(); it++;
    a.erase(it);
    print(a);
    
    a.pop_front();
    a.pop_back();
    print(a);
    
    cout << a.front() << " : " << a.back() << '\n';
    a.clear();
    return 0;
}

/*
3 1000 2 1 1 2 3
3 2 1 1 2 3
2 1 1 2
2 : 2
*/
```

> **method**

-   **push_front(value)**
    -   리스트의 앞에서 부터 value를 넣는다.
-   **push_back(value)**
    -   뒤에서부터 value를 넣는다.
-   **insert(idx, value)**
    -   요소를 idx번째에 삽입

```cpp
iterator insert (const_iterator position, const value_type& val);
```

-   **erase(idx)**
    -   리스트의 idx번째 요소를 지운다.

```cpp
iterator erase (const_iterator position);
```

-   **pop_front()**
    -   첫번째 요소를 지운다
-   **pop_back()**
    -   맨 끝 요소를 지운다.
-   **front()**
    -   맨 앞 요소를 참조한다.
-   **back()**
    -   맨 뒤 요소를 참조한다.
-   **clear()**
    -   모든 요소를 지운다.

> **랜덤 접근과 순차적 접근**

-   직접 접근이라고 하는 **랜덤 접근(random access)**
    -   동일한 시간에 배열과 같은 순차적인 데이터가 있을 때 **임의의 인덱스에 해당하는 데이터에 접근**할 수 있는 기능
-   데이터를 저장된 **순서대로 검색**하는 **순차적 접근(sequential access)** 

![](https://blog.kakaocdn.net/dn/bDpe1Q/btr0GJ4nHpC/fccCY65K0reMqH4NI8s8w1/img.png)

-   **vector, Array**와 같은 배열은 **랜덤접근이 가능**해서 k번째 요소에 접근시 **O(1)**
-   **연결리스트, 스택,** 큐는 **순차적 접근**만 가능해서 k번째 요소에 접근할 때 **O(k)** 

> **배열과 연결리스트 비교**

![](https://blog.kakaocdn.net/dn/bqchrj/btr0xLiG65z/nLklkkqCFUkdJkpkmaYVNk/img.png)

-   **배열**  
    -   연속된 메모리 공간에 데이터를 저장
    -   삽입과 삭제 -> **O(n)**
    -   참조 -> **O(1)**
-   **연결리스트**
    -   연속되지 않은 메모리 공간에 데이터를 저장
        -   삽입과 삭제 -> **O(1)**
        -   참조 -> **O(n)**

따라서, **데이터 추가 및 삭제를 많이하면 -> 연결리스트**

             **참조를 많이 하는 것은 -> 배열**