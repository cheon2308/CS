OTT, 유튜브 등을 시청할 때 '버퍼링' 때문에 짜증났던 기억이 있을 것이다. 왜 일어나는 것일까? 배웠던 Queue 구조를 활용하여 **버퍼**에 대해 알아보자.

또한 queue를 파이썬에서 더 간편하고 빠르게 사용하게 해주는 deque에 대해서도 알아보자.

#### **목차**

1. 버퍼

2. deque 모듈

---

### **1. 버퍼**

-   데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리 영역
-   **버퍼링:** 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작

> **자료 구조**

-   버퍼는 일반적으로 입출력 및 네트워크와 관련된 기능에서 이용
-   순서대로 입/출력/전달되어야 하므로 **FIFO 방식의 자료구조인 큐가 활용**

**그림**을 통해 키보드 버퍼의 수행 과정을 보자.

![](https://blog.kakaocdn.net/dn/bDcX9s/btrKrLYduPY/y3hyWbTDeifl9q7MyHxkYK/img.png)

Queue와 버퍼에 대해 '마이쮸 나눠주기'를 구현해보며 이해해보자!!

> 마이쮸 나눠주기

![](https://blog.kakaocdn.net/dn/bjxEdm/btrKn7ol4aY/btEzfR3tWRBoUeRA6x6aBk/img.png)

![](https://blog.kakaocdn.net/dn/cBVBjR/btrKrJ7c46P/YIkuRudasbY16l7k0mK2WK/img.png)

![](https://blog.kakaocdn.net/dn/tJgrO/btrKpylv0Lu/xQ40aJPcJYoXf9lF7ww5Bk/img.png)

```
p = 1 # 처음 줄 설 사람 번호

q = []
N = 20 # 초기 마이쮸 개수
m = 0  # 나눠준 개수

while m<N:
    input()
    q.append((p,1,0)) # 처음 줄 서는 사람
    print(q)
    #  c = 줄선 횟 수
    # v = 받아가는 사람 번호
    v, c, my = q.pop(0)
    print(f'큐에 있는 사람 수 {len(q)+1}, 받아갈 사람 수 {c}, 나눠준 사탕 수{m}')
    m += c
    q.append((v, c+1, my+c)) # 마이쮸를 받고 다시 서는 사람
    p += 1 # 처음 줄서는 사람 번호

print(f'마지막 받은 사람: {v}')
```

엔터키를 칠 때마다 버퍼와 같이 현재 정보가 출력된다!

---

### **2. deque**

-   double-ended queue의 약자로 **데이터를 양방향에서 추가 및 제거할수 있는 자료구조**
-   스택과 큐의 **특징들을 모두 가진다.**
-   **appendleft(), popleft()**를 이용하여 맨 앞에 데이터를 삽입, 삭제 할 수 있고 **O(1)**이라는 훌륭한 시간 복잡도를 가진다.
-   한쪽 끝에서의 출력 또는 입력 작업에 제한을 둔 **출력제한 덱, 입력제한 덱**도 존재한다.
-   다만, 무작위 접근의 시간 복잡도가 **O(N)**이고, 내부적으로 **linked list를 사용**하여 N번째 데이터에 접근하려면 N번 순회가 필요하다.

```
from collections import deque
>>> queue = deque([1, 2, 3])
>>> type(queue)
<class 'collections.deque'>
>>> queue.append(4)
>>> queue
deque[1, 2, 3, 4]
>>> queue.popleft()
1
>>> queue.popleft()
2
>>> queue
deque[3, 4]

# rotate
>>> queue.append(1)
>>> queue
deque[3, 4, 1]
>>> queue.rotate(1)
>>> queue
deque[1, 3, 4]
```

![](https://blog.kakaocdn.net/dn/lX3AK/btrL4bHFgdG/PIk51wRFkeET1lksUvOZ4K/img.png)

또는 queue 모듈의 Queue 클래스를 사용할 수 있다.

-   queue 모듈의 Queue 클래스는 **클래스 형태**기 때문에 객체 변수를 할당받아 사용
-   위의 deque와 달리 방향성이 없어 데이터 추가와 삭제가 한 메소드로 처리된다.
    -   데이터 추가 **put(x)**
    -   데이터 삭제 **get()**
-   주로 **멀티 쓰레딩 환경에서 사용**하며 내부적으로 **라킹**을 지원해 여러 쓰레드가 동시에 데이터를 추가하거나 삭제할 수 있음
-   성능은 deque와 동일하다.

```
from queue import Queue
>>> que = Queue()
>>> que.put(1)
>>> que.put(2)
>>> que.put(3)
>>> que.get()
1
>>> que.get()
2
```

또한 queue 모듈에 정의된 클래스 정보

![](https://blog.kakaocdn.net/dn/egT86B/btrL3AVyCHP/enKd9UEGcowKInjrL2jyW0/img.png)

각 클래스는 아래의 메소드를 동일하게 사용한다.

-   **qsize() :** 아이템 갯수 반환
-   **put(n) :** 아이템 등록
-   **put_nowait :** 블로킹 없이 큐 객체에 아이템 등록
-   **get :** 아이템 1개 반환
-   **get_nowiat()** : 블로킹 없이 큐 객체에 들어있는 아이템 반환