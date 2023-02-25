이전에 배웠던 스택과 마찬가지로 **삽입**과 **삭제**의 위치가 제한적인 자료구조이다.

동적 자료형인 리스트 자료형을 사용한다

-   **선입선출 구조(FIFO** **: First In First Out)**  
    -   큐의 뒤에서는 삽입만 하고, 큐의 앞에서는 삭제만 한다.
    -   즉, 삽입한 순서대로 원소가 저장되어, 가장 먼저 삽입된 원소가 가장 먼저 삭제된다.

![](https://blog.kakaocdn.net/dn/bLbTot/btrKqP0Dcec/7kKXQntdBaZOpoaKp0K7ZK/img.png)

-   기본 연산
    -   삽입 : enQueue(item) - 큐의 뒤쪽(rear 다음)에 원소를 삽입하는 연산
    -   삭제 : deQueue() - 큐의 앞쪽(front)에서 원소를 삭제하고 반환하는 연산
    -   createQueue() - 공백 상태의 큐를 생성하는 연산
    -   isEmpty() - 큐가 공백상태인지를 확인하는 연산
    -   isFull() - 큐가 포화상태인지를 확인하는 연산
    -   Qpeek() - 큐의 앞쪽(front)에서 원소를 삭제 없이 반환하는 연산

![](https://blog.kakaocdn.net/dn/Anrfs/btrKtAokw6w/MLUHsWLXYmWtY5SoUCjfU0/img.png)

공백 큐 생성과 삽입

![](https://blog.kakaocdn.net/dn/VBv2s/btrKpz5OrX4/zJQweKYQ8SECq7VBeOUkR1/img.png)

원소 삭제와 삽입

위에서 1차원 배열로 이루어진 큐의 동작을 그림과 함께 알아보았다. 코드와 함께 1차원 배열 큐의 특성을 알아보자.

### # **선형 큐**

-   1차원 배열을 이용한 큐
    -   큐의 크기 = 배열의 크기
    -   front: 저장된 첫 번째 원소의 인덱스
    -   rear: 저장된 마지막 원소의 인덱스
-   상태 표현
    -   초기 상태: front = rear = -1
    -   공백 상태: front == rear
    -   포화 상태: rear == n-1 (n:배열의 크기, n-1: 배열의 마지막 인덱스)

1. **초기 공백 큐 생성**

-   크기 n인 1차원 배열 생성
-   front와 rear를 -1로 초기화

2. **삽입: enQueue(item)**

-   마지막 원소 뒤에 새로운 원소를 삽입하기 위해
-   1) rear 값을 하나 증가시켜 새로운 원소를 삽입할 자리를 마련
-   2) 그 인덱스에 해당하는 배열 원소 Q[rear]에 item을 저장

3. **삭제 : deQueue()**

-   가장 앞에 있는 원소를 삭제
-   1) front 값을 하나 증가시켜 큐에 남아있게 될 첫 번째 원소 이동
-   2) 새로운 첫 번째 원소를 리턴 함으로써 삭제와 동일한 기능

```
class Queue:

    def __init__(self, size):
        self.size = size
        self.items = [None]*size
        self.rear = -1
        self.front = -1

    def enQueue(self, item):
        self.rear += 1
        self.items[self.rear] = item

    def deQueue(self):
        self.front += 1
        return self.items[self.front]
```

4. **공백상태 및 포화상태 검사: isEmpty(), isFull()**

-   공백상태: front == rear
-   포화상태: rear == n-1 (n: 배열의 크기, n-1: 배열의 마지막 인덱스)

```
def isEmpty():
	return front == rear
    
def Full():
	return rear == len(Q) -1
```

**5. 검색: Qpeek()**

-   가장 앞에 있는 원소를 검색하여 반환하는 연산
-   현재 front의 한자리 뒤(front+1)에 있는 원소, 즉 큐의 첫 번째에 있는 원소를 반환

```
def Qpeek():
	if isEmpty() : print("Queue_Empty")
    else: return Q[front+1]
```

방금과 같이 선형 큐를 이용한다면 문제점이 있다. 무엇일까!?

> **성능  
> **

-   list 자료형을 사용하는데 **list 자료형의 경우 무작위 접근에 최적화**
-   **pop(0)와 insert(0,** **x)**는 **O(n)**의 시간 복잡도 

> **잘못된 포화상태 인식**

-   선형 큐를 이용하여 원소의 삽입과 삭제를 계속할 경우, 배열의 앞부분에 활용할 수 있는 공간이 있음에도 불구하고, rear=n-1인 상태 즉, 포화상태로 인식하여 더 이상의 삽입을 수행하지 않는다.

![](https://blog.kakaocdn.net/dn/4LwMw/btrKrLw7VKo/McZaRUku1Zpi6KHLZAckvK/img.png)

**# 해결방법**

1. 매연산이 이루어질 때마다 저장된 원소들을 배열의 앞부분으로 모두 이동시킴

    원소이동에 많은 시간이 소요되어 **큐의 효율성이 급격히 떨어짐**

![](https://blog.kakaocdn.net/dn/ImG0k/btrKpzreZHa/KEVyXJxjtrA43YUW3i6GR1/img.png)

2. 1차원 배열을 사용하되, 논리적으로는 배열의 처음과 끝이 연결되어 원형 형태의 큐를 이룬다고 가정하고 사용

![](https://blog.kakaocdn.net/dn/cCzZZb/btrKpTibMeU/y8fmpWAJqUJFakGEfVgsE1/img.png)

원형 큐의 논리적 구조

---

### **# 원형 큐**

-   초기 공백 상태
    -   front = rear = 0
-   Index의 순환
    -   front와 rear의 위치가 배열의 마지막 인덱스인 n-1을 가리킨 후, 그다음에는 논리적 순환을 이루어 배열의 처음 인덱스인 0으로 이동해야 함
    -   이를 위해 나머지 연산자 mod를 사용함
-   **front 변수**
    -   공백 상태와 포화 상태 구분을 쉽게 하기 위해 front가 있는 자리는 사용하지 않고 항상 빈자리로 둠
-   **삽입 위치 및 삭제 위치**

![](https://blog.kakaocdn.net/dn/BYAsS/btrKrLKF1QS/JUyg7npSodMWmT24rXKVU0/img.png)

> **연산과정**

**1. create Queue**

![](https://blog.kakaocdn.net/dn/uT3VV/btrKq5vQR3Z/fVlPnGzJT90XTKqBrsWwNk/img.png)

**2. enQueue(A);**

![](https://blog.kakaocdn.net/dn/vt43d/btrKqa42eN1/g31WuiLXKg3ZCN8YHNK3nk/img.png)

**3. enQueue 및 deQueue**

![](https://blog.kakaocdn.net/dn/cKtylN/btrKn7okoj7/dYBNin3VnXkvcAYMp88Qlk/img.png)

![](https://blog.kakaocdn.net/dn/c2J4AI/btrKsN2ka0r/WiRa3OrPoZBofOWkg6wZCk/img.png)

사실상 덮어써버리는 경우가 아니면 많이 사용하지 않는다. 코드와 함께 구현해보자.

**1. 초기 공백 큐 생성**

-   크기 n인 1차원 배열 생성
-   front와 rear를 0으로 초기화

**2. 공백상태 및 포화상태 검사 : isEmpty(), isFull()**

-   공백상태: front == rear
-   포화상태: 삽입할 rear의 다음 위치 == 현재 front
-   -(rear +1) mod n == front

**3. 삽입: enQueue(item)**

-   마지막 원소 뒤에 새로운 원소를 삽입하기 위해
-   1) rear 값을 조정하여 새로운 원소를 삽입할 자리를 마련함;   rear <- (rear +1) mod n;
-   2) 그 인덱스에 해당하는 배열 원소 cQ [rear]에 item을 저장

**4. 삭제: deQueue(), delete()**

-   가장 앞에 있는 원소를 삭제하기 위해
-   1) front 값을 조정하여 삭제할 자리를 준비함
-   2) 새로운 front 원소를 리턴 함으로써 삭제와 동일한 기능

```
class Queue:
    def __init__(self, size):
        self.size = size
        self.items = [None] * size
        self.rear = self.size
        self.front = 0

    def enQueue(self, item):
        if self.isFull():
            print('is Full')
        else:
            self.rear = (self.rear + 1) % self.size
            self.items[self.rear] = item

    def deQueue(self):
        self.front = (self.front + 1) % self.size
        return self.items[self.front]

    def isFull(self):
        return self.front == (self.rear + 1) % self.size
```

---

### **# 우선순위 큐(Priority Queue)**

앞서 살펴봤던 큐들과는 조금은 다른, 또 사용분야가 많은 **우선순위 큐**에 대해 알아보자.

> **특성  
> **

-   우선순위를 가진 항목들을 저장하는 큐
-   FIFO 순서가 아니라 우선순위가 높은 순서대로 먼저 나가게 된다.

> **적용 분야**

1. 시뮬레이션 시스템

2. 네트워크 트레픽 제어

3. 운영체제의 테스크 스케줄링

> **구현**

1. 배열을 이용한 우선순위 큐

-   배열을 이용하여 자료를 저장하며 원소를 삽입하는 과정에서 우선순위를 비교하여 적절한 위치에 삽입하는 구조
-   가장 앞에 최고 우선순위의 원소가 위치하게 됨
-   **문제점** : 배열을 사용하므로, 삽입이나 삭제 연산이 일어날 때 원소의 재배치가 발생, 이에 소요되는 시간이나 메모리 낭비가 크다.

2. 리스트를 이용한 우선순위 큐

> **기본 연산**

-   삽입 : enQueue
-   삭제 : deQueue

![](https://blog.kakaocdn.net/dn/b1TYUL/btrKmLZvzwt/1rMErWWTGhATDGPXIoJYe1/img.png)

이론으로만 간단히 알아보았다. 나중에 트리구조, 그래프 구조에 대해 배워보며 실습과 함께 구현을 직접 해보겠지만 유튜브 등 자료 더 찾아보고 직접 구현해보자!!