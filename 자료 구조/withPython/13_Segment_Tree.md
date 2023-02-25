
#### **목차**

1.  Segment Tree?
2.  구현
3.  업데이트

---

### **1. Segment Tree?**

어떤 데이터가 존재할 때, **특정 구간의 결과값을 구하는데 사용하는 자료구조**이다.

아래와 같은 배열이 존재할 때, 구간합을 구해보자.

![](https://blog.kakaocdn.net/dn/c4mUtA/btrStQykkqq/rqwam2yugD3eOBEpnKJtt0/img.png)

배열을 돌면서 원하는 구간의 합을 더해주면 된다!

**배열의 크기가 커진다면, 시간이 더 많이 걸릴 것이다.**

**따라서, 구간별 합을 구해 저장해둔다면 빠르게 찾을 수 있을 것이다!!**

-   세그먼트 트리는 **Binary Tree(이진 트리) 구조**를 가지고 있다.
-   선형 탐색보다 좀 더 효율적인 탐색이 가능하다.
-   특히, **누적합**의 경우 특정 데이터 변경 시 **O(N)으로 업데이트**
-   **세그먼트 트리**는 **O(logN)**으로 반영
-   **단점**으로는 기본 완전 탐색 사용에 비해 **더 많은 메모리가 필요**하게 된다.

![](https://blog.kakaocdn.net/dn/b4b7Nn/btrSsZ98zWP/5BgLZbZkupfutJecgXkVx1/img.png)

![](https://blog.kakaocdn.net/dn/dATCct/btrSsnwCpyS/Y9kCTTGaaxhjFHDKy3UXEk/img.png)

-   0번 인덱스 값은 1번과 2번 인덱스를 더한 값
-   1번은 3번과 4번 인덱스를 더한 값
-   편의를 위해 **배열의 크기를 +1** 해준다면 구하기 쉬울 것이다!

![](https://blog.kakaocdn.net/dn/SwsVA/btrSwCMLuPY/3ouBMFWkBVrcSaIk1hJc2k/img.png)

-   1번의 경우 2번과 3번
-   2번의 경우 4번과 5번
-   즉, **왼쪽 노드는 x2 / 오른쪽 노드는 x2 + 1 로 접근** 가능!!
-   **배열의 크기**
    -   **Full Binary Tree** 일 경우 
    -   2^(H+1) - 1 개

---

### **2. 구현**

-   세그먼트 트리의 경우 재귀 구조를 이용하여 구현한다.

```
# <세그먼트 트리를 배열의 각 구간 합으로 채워주기>
# start : 배열의 시작 인덱스, end : 배열의 마지막 인덱스
# index : 세그먼트 트리의 인덱스 (무조건 1부터 시작)
def init(start, end, index):
    # 가장 끝에 도달했으면 arr 삽입
    if start == end:
        tree[index] = arr[start]
        return tree[index]
    mid = (start + end) // 2
    # 좌측 노드와 우측 노드를 채워주면서 부모 노드의 값도 채워준다.
    tree[index] = init(start, mid, index * 2) + init(mid + 1, end, index * 2 + 1)
    return tree[index]
```

![](https://blog.kakaocdn.net/dn/nukDw/btrSwRQr712/poo4rpy9EUqwqu6PP5HBaK/img.png)

![](https://blog.kakaocdn.net/dn/btFngi/btrSsSpMPHH/4K0TDSmbUcbPgIPTBiDR4K/img.png)

![](https://blog.kakaocdn.net/dn/tloEe/btrSs0Beoue/wK3N4AM2c0gOga0bFMrLuK/img.png)

![](https://blog.kakaocdn.net/dn/p8TVK/btrSwMuXDxW/803VgLnh7ixJ2KTfEzjOY0/img.png)

![](https://blog.kakaocdn.net/dn/df6yty/btrSsSiZFRq/lfcjHnVqntJyBNtguzEfmk/img.png)

![](https://blog.kakaocdn.net/dn/MGM6y/btrSwpNGFUY/nIbXeyzhAPGaTFXrnxIEHk/img.png)

![](https://blog.kakaocdn.net/dn/w0Dl4/btrSwjUlRzm/ynsUPbarT01W6KsNE5AMo1/img.png)

> **세그먼트 트리 쿼리**

-   각 구간에 대해 쿼리를 하여 구간합을 **합리적인 시간에 리턴**해주어야 한다.
    1.  구간이 노드의 구간에 완전히 벗어난 경우 -> 0 리턴
    2.  요청 구간이 노드의 구간을 완전히 포함한 경우 -> 트리 좌표의 값 리턴
    3.  노드의 구간이 요청 구간을 완전히 포함한 경우 -> 요청 구간 외의 잉여 구간 배제해야 하므로 **절반씩 나눠 재귀 탐색**
    4.  요청 구간이 노드의 구간에 걸쳐진 경우 -> 3번과 같이 더 깊이 탐색해서 요청 외 잉여 구간 배제
-   위 1, 2번에 대해 조건 분기를 해준 코드를 작성해보자.

```
# <구간 합을 구하는 함수>
# start : 시작 인덱스, end : 마지막 인덱스
# left, right : 구간 합을 구하고자 하는 범위
def interval_sum(start, end, index, left, right):
    # 범위 밖에 있는 경우
    if left > end or right < start:
        return 0
    # 범위 안에 있는 경우
    if left <= start and right >= end:
        return tree[index]
    # 그렇지 않다면 두 부분으로 나누어 합을 구하기
    mid = (start + end) // 2
    # start와 end가 변하면서 구간 합인 부분을 더해준다고 생각하면 된다.
    return interval_sum(start, mid, index * 2, left, right) + interval_sum(mid + 1, end, index * 2 + 1, left, right)
```

---

### **3. Segment Tree 업데이트**

-   기존 배열의 i번째 원소를 바꾸고 싶은 상황이 발생했을 때, 매번 새로 트리를 만들기는 효율이 떨어진다. 
-   따라서 원소가 포함된 구간만 변경을 가하면 된다.
-   우선 바꾸고자 하는 인덱스가 포함되지 않은 경우는 의미없는 탐색이므로 그대로 종료하고 구간에 포함될 경우 기존 값과 바뀔 값의 차이를 넘겨 트리의 값에 반영
-   만약 리프 노드까지 도달하지 못했다면 좌/우로 분할하여 반영

```
def update(tree, i, start, end, idx, diff):
    if start > idx or idx > end:
        return
    tree[i] += diff
    if start != end:
        mid = left + (right - left) // 2
        update(tree, i * 2, start, mid, idx, diff)
        update(tree, i * 2 + 1, mid + 1, end, idx, diff)
```

**Update index = 4**

![](https://blog.kakaocdn.net/dn/cpawmO/btrSyhueLYm/8YycOCSDW2CaAplmPbMPZ0/img.png)

![](https://blog.kakaocdn.net/dn/bNTWhV/btrSxDRQeUD/yHIVZ4gAKNELGZk0fpaFa0/img.png)

![](https://blog.kakaocdn.net/dn/byFWkq/btrSsmq0Y6G/vYPpSpfKkbzol4KzO6FNBK/img.png)

![](https://blog.kakaocdn.net/dn/ong8p/btrSvzDbFF9/yyzx3qv3ZdQTo3sl0A2JyK/img.png)

![](https://blog.kakaocdn.net/dn/brgEZX/btrSwSu7FQw/vm8uWHKepK1e3t1F4wvM0K/img.png)

![](https://blog.kakaocdn.net/dn/WqrTM/btrSs1tublQ/9SF4uaS43R00oj5kAsek2K/img.png)

![](https://blog.kakaocdn.net/dn/Hb5nf/btrSwjfLePV/0kPkYMY4ule2QrDTZRiJaK/img.png)

![](https://blog.kakaocdn.net/dn/qbmgI/btrSwK42HUk/R20hXKKEwm13foXgQqTN40/img.png)

![](https://blog.kakaocdn.net/dn/baaEhl/btrSwtvFWav/q4nypmkPY4pTDSqJfkECx0/img.png)

![](https://blog.kakaocdn.net/dn/ckMjrW/btrSsZWE8Bs/Mhs6BKLdWpjeSXW7PUEOs0/img.png)

![](https://blog.kakaocdn.net/dn/bNs7uX/btrSwSWcn1Z/0NkZ4jmO0htzlZXaZgwSw0/img.png)

![](https://blog.kakaocdn.net/dn/ebMPeZ/btrSs02ioPb/6ZTDLkitPCFqj4BYm7K3nk/img.png)

![](https://blog.kakaocdn.net/dn/bzfZ0B/btrSw5gKRmu/EdCfeKBTvkOO1GT6TgBxL1/img.png)

> **전체 코드**

```python

from math import ceil, log
 
 
def init(arr, tree, i, left, right):
    if left == right:
        tree[i] = arr[left]
        return tree[i]
    mid = left + (right - left) // 2
    tree[i] = init(arr, tree, i * 2, left, mid) + \
        init(arr, tree, i * 2 + 1, mid + 1, right)
    return tree[i]
 
 
def search(tree, i, start, end, left, right):
    if end < left or right < start:
        return 0
    if left <= start and end <= right:
        return tree[i]
    mid = start + (end - start) // 2
    return search(tree, i * 2, start, mid, left, right) + search(tree, i * 2 + 1, mid + 1, end, left, right)
 
 
def update(tree, i, start, end, idx, diff):
    if start > idx or idx > end:
        return
    tree[i] += diff
    if start != end:
        mid = start + (end - start) // 2
        update(tree, i * 2, start, mid, idx, diff)
        update(tree, i * 2 + 1, mid + 1, end, idx, diff)
 
 
nums = [1, 3, 5, 2, 6, 4]
segment_tree = [0] * pow(2, ceil(log(len(nums), 2) + 1))
 
init(nums, segment_tree, 1, 0, len(nums) - 1)
 
print(f'idx 0 to 3 : {nums[0:4]}')
print(f'sum 0 to 3 : {search(segment_tree, 1, 0, len(nums) - 1, 0, 3)}')
 
print(segment_tree)
update(segment_tree, 1, 0, len(nums) - 1, 3, 4 - nums[3])
nums[3] = 4
print(segment_tree)
```