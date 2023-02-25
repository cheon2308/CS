

#### **목차**

1.  팬윅 트리?
2.  구현
3.  업데이트

---

### **1. Fenwick Tree ?**

-   Segment Tree 처럼 구간에 대한 연산을 저장하는 트리
-   Segment Tree 보다 **적은 메모리**로 사용 가능하다!!
    -   절반 정도의 메모리만으로 사용 가능
    -   시간 복잡도 **O(logN)**
-   **비트**를 이용한 구간 연산을 진행한다.

![](https://blog.kakaocdn.net/dn/BeGjk/btrSyqrdHxg/o3mGIXiOm1zD4E0IrKqdq0/img.png)

![](https://blog.kakaocdn.net/dn/bEG1gG/btrSyhVqckm/8rsJvk1tkymk5fxh0KyXek/img.png)

![](https://blog.kakaocdn.net/dn/b8Rhpp/btrSsRki8rb/nfTZ6L1w4IV3lqPUkJX0C1/img.png)

![](https://blog.kakaocdn.net/dn/blGp3n/btrStQeda0v/k8tr3AP6MukOPgPfR8pKO1/img.png)

**Q. 3~5번째 인덱스 구간 합을 구하기**

**A. 두 구간의 차를 구하면 된다.**

![](https://blog.kakaocdn.net/dn/bDnajc/btrSwrEKL9x/Kf3thku6kyQamqKPRqY3R0/img.png)

![](https://blog.kakaocdn.net/dn/dOyLgR/btrSw4I5vJO/QkEjD6gCcd1DAbiMziVk61/img.png)

**5번 인덱스**까지의 값을 구하려면 **2진수 101 인덱스 값**과 **100 인덱스 값**을 더하면 된다.

101 인덱스에서 **마지막 1의 값을 제거**해주면 100이 된다.

**Q. 마지막 2진수 1의 값을 제거하는 방법은?**

![](https://blog.kakaocdn.net/dn/Tryw3/btrSs0VIn7v/P9khODVlmUdntDklhANHsK/img.png)

![](https://blog.kakaocdn.net/dn/dTtNdN/btrSwLXgOOT/v3vWmi14U0swmy7RGnxdJk/img.png)

**Answer.**

-   N = N - (N & -N)
-   5 - ( 5 & -5 ) = 4
-   4 - ( 4 & -4 ) = 0

---

### **2. 구현**

![](https://blog.kakaocdn.net/dn/bBUH3P/btrSwDkQDpb/2OgVcZRaKZJRQmDilqtqjk/img.png)

-   Val = 1
-   index = 1 -> 1 += (1 & -1) = 2

![](https://blog.kakaocdn.net/dn/bIuT2W/btrStRRMzGX/TrivLg8Fv2KlpRa34VGvi1/img.png)

-   Val = 1
-   index = 2 -> 2 += (2 & -2) = 4

![](https://blog.kakaocdn.net/dn/cxkN6i/btrStQyBdnx/gtNAKTVdoyKGT1yoKP18z1/img.png)

-   Val = 1
-   index = 4 -> 4 += (4 & -4) = 8

![](https://blog.kakaocdn.net/dn/cmUKK4/btrSvz4msG0/SmW4q44lgxoh2HHFkPIh3k/img.png)

-   Val = 1
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지** 

![](https://blog.kakaocdn.net/dn/ewAB1G/btrSs0OYbNk/al0KtL9guJwsXhVXTW6CWk/img.png)

![](https://blog.kakaocdn.net/dn/Y9ZjZ/btrSvdHdCtR/f7V9fYNVERRvuoeqEQCjJ0/img.png)

-   Val = 2
-   index = 2 -> 2 += (2 & -2) = 4

![](https://blog.kakaocdn.net/dn/3iOW5/btrSwRQGUW5/9NHQlKZhB64CAZRmkc2ksK/img.png)

-   Val = 2
-   index = 4 -> 4 += (4 & -4) = 8

![](https://blog.kakaocdn.net/dn/dhKsUN/btrSxDLeRz1/bmMuxmoKzjsWqXBspYg0K0/img.png)

-   Val = 2
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지** 

![](https://blog.kakaocdn.net/dn/bDn05d/btrSwLbXuuy/kAMfmsjsLaKTz60f7XNRt1/img.png)

![](https://blog.kakaocdn.net/dn/dnV41C/btrSwMhBxBS/iDvJ5nSMg2CPOpqM4l14c1/img.png)

-   Val = 3
-   index = 3 -> 3 += (3 & -3) = 4

![](https://blog.kakaocdn.net/dn/b4FZK8/btrSvzDmWrJ/kjTLndH0IcrPZ1l9WVvcJk/img.png)

-   Val = 3
-   index = 4 -> 4 += (4 & -4) = 8

![](https://blog.kakaocdn.net/dn/JgcNz/btrSxFI5xTB/9bF6faiF3SW9PWkkk1IK4K/img.png)

-   Val = 3
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/byS7rn/btrSsRxNS4J/GkSKwQyaV2Rr4hY0lwmHKK/img.png)

![](https://blog.kakaocdn.net/dn/cVjkr5/btrSxEi6a0f/z892e9Ww1gnbJGHFvckpM0/img.png)

-   Val = 4
-   index = 4 -> 4 += (4 & -4) = 8

![](https://blog.kakaocdn.net/dn/xpTVK/btrSsRxNUpS/yHb05ibveQczEPfQxfkDsk/img.png)

-   Val = 4
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/esxRb0/btrSwS9VenY/pEeYNwLnrfOK419ovUbR91/img.png)

-   Val = 5
-   index = 5 -> 5 += (5 & -5) = 6

![](https://blog.kakaocdn.net/dn/C9B7b/btrSvAPNEi1/yYJICR2qJBJ6ekvHeM00MK/img.png)

-   Val = 5
-   index = 6 -> 6 += (6 & -6) = 8

![](https://blog.kakaocdn.net/dn/cHOXu5/btrSypFUStd/V8SOzUJpPXSko0ZypThg8K/img.png)

-   Val = 5
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/RmzXu/btrSwtbx76D/A41R8Hb7XSTO4hvbMlA0j1/img.png)

-   Val = 6
-   index = 6 -> 6 += (6 & -6) = 8

![](https://blog.kakaocdn.net/dn/MDC83/btrSxlxeCX9/J1u8Siz79vc3Hk6cmpiK7k/img.png)

-   Val = 6
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/ucMOK/btrSs0uGFaY/svPZDUqlUReE7gCt38Lms0/img.png)

-   Val = 7
-   index = 7 -> 7 += (7 & -7) = 8

![](https://blog.kakaocdn.net/dn/cNhFE4/btrSwC7jmpE/P0VKHmfDqTCdlzgWxXYYRk/img.png)

-   Val = 7
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/boIcyE/btrSxkrCj1C/bKMz9LH0JgVwdIdLKhb9Zk/img.png)

-   Val = 8
-   index = 8 -> 8 += (8 & -8) = 16
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/dljSz8/btrSsZvNVtU/kGJTZs7hRwQQPLSZKGdq0K/img.png)

-   Val = 9
-   index = 9 -> 9 += (9 & -9) = 10

![](https://blog.kakaocdn.net/dn/blPONL/btrSw587oTt/fmlBtIXRFtnsRwnzKwJIk0/img.png)

-   Val = 9
-   index = 10 -> 10 += (10 & -10) = 12
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/lewqL/btrSwi2qRiI/EyzsSZUH5sm2JYYDSHDINK/img.png)

-   Val = 10
-   index = 10 -> 10 += (10 & -10) = 12
-   **트리의 길이보다 index 값이 크기 때문에 중지**

![](https://blog.kakaocdn.net/dn/KZ8gV/btrSsZCw7KE/ThrJWM0ZDN9opRQpOgK5RK/img.png)

![](https://blog.kakaocdn.net/dn/pFM8v/btrSxEckuvF/LbgwSYT0vxuI2d4pTIEyfK/img.png)

---

### **3. 업데이트**

특정 값을 변경해주고 싶다면, **0이 아닌 마지막 비트만큼 더하면서 구간들의 값을** **변경**

![](https://blog.kakaocdn.net/dn/cG0KAy/btrSwjmITIG/OSZuTSYtcfZdCjktj3sNm0/img.png)

![](https://blog.kakaocdn.net/dn/bh4Yvg/btrSyrDJxqd/fTkCi9v6pMaTOhKimikIo0/img.png)

![](https://blog.kakaocdn.net/dn/lbAYf/btrSyrqcw5e/WBCPOOV81WfJbG06cxkre1/img.png)

> **전체 코드**

```python
import sys
input = sys.stdin.readline()

# 데이터의 개수(n), 변경 횟수(m), 구간 합 계산 횟수(k)
n,m,k = map(int,input().split())

# 전체 데이터의 개수는 최대 1,000,000개
arr = [0] * (n+1)
tree = [0] * (n+1)

# i번째 수까지의 누적 합을 계산하는 함수
def prefix_sum(i):
    result = 0
    while i > 0:
        result += tree[i]
        # 0이 아닌 마지막 비트만큼 빼가면서 이동
        i -= (i & -i)
    return result

# i번째 수를 dif만큼 더하는 함수
def update(i,dif):
    while i <= n:
        tree[i] += dif
        i += (i & -i)

# start부터 end까지의 구간 합을 계산하는 함수
def interval_sum(start,end):
    return prefix_sum(end) - prefix_sum(start-1)

for i in range(m+k):
    a,b,c = map(int,input().split())
    # 업데이트(update) 연산인 경우
    if a == 1:
        update(b,c - arr[b])
        arr[b] = c
    # 구간 합(interval) 연산인 경우
    else:
        print(interval_sum(b,c))
```