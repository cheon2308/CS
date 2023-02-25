
> **Array**

-   **정적배열**
-   **선언 시** 보통 **크기를 설정해서 연산** 진행
-   **연속된 메모리** **공간**에 위치한 **같은 타입의 요소들**의 모음이며 **숫자인덱스를 기반**으로 랜덤접근이 가능하며 **중복을 허용**

![](https://blog.kakaocdn.net/dn/dfo1m5/btr0yhuvBLb/c7rena1yqZHioMIvJgvbs0/img.png)

> **선언 타입**

-   c 스타일과 std 스타일이 존재
-   **c 스타일**
    -   int a[10] 과 같이 선언
-   **std 스타일**  
    -   array<int, 10> a; 이렇게 선언

> **특징**

-   vector와는 달리 메서드가 xxxxx
-   배열의 크기를 정해서 선언할 수도 있음
    -   int a[3]
-   크기를 정하지 않고 선언하되 **배열을 중괄호로 요소들을 할당**할 수도 있음
    -   int a2[] = {1, 2, 3, 4}
-   위 코드처럼 하게 되면 자동적으로 rvalue의 크기로 할당되어 int a2[] 는 int a2[4] 와 같은 의미를 가진다.

> **예시 코드**

```cpp
#include <bits/stdc++.h>
using namespace std;
int a[3] = {1,2,3};
int a2[] = {1,2,3,4};
int a3[10];
int main(){
    for(int i = 0; i < 3; i++) cout << a[i] << " ";
    cout << '\n';
    for(int i : a) cout << i << " ";
    
    for(int i = 0; i < 4; i ++) cout << a2[i] << " ";
    cout << '\n';
    for(int i : a2) cout << i << " ";
    
    for(int i = 0; i < 10; i++) a3[i] = i;
    cout << '\n';
    for(int i : a2) cout << i << " ";
    return 0;
}

/*
1 2 3
1 2 3 1 2 3 4
1 2 3 4
1 2 3 4
*/
```

-   Arrya, vector와 같은 배열은
    -   **같은 타입**의 변수들로 이루어져 있고
    -   **크기**가 정해져 있으며
    -   **인접한 메모리위치**에 있는 데이터들을 모아놓은 집합

> **2차원 배열과 탐색을 빠르게 하는 팁**

-   단순하게 차원을 늘려서 만들면 된다.

```cpp
#include <bits/stdc++.h>
using namespace std;
const int mxy = 3;
const int mxx = 4;

int a[mxy][mxx];
int main(){
    for(int i = 0; i < mxy; i++){
        for(int j = 0; j < mxx; j++){
            a[i][j] = (i + j);
        }
    }
    // good
    for(int i = 0; i < mxy; i++){
        for(int j = 0; j < mxx; j++){
            cout << a[i][j] << ' ';
        }
        cout << '\n';
    }
    
    //bad
    for(int i = 0; i < mxx; i++){
        for(int j = 0; j < mxy; j++){
        cout << a[j][i] << ' ';
        }
        cout << '\n';
	}
    return 0;
}

/*
0 1 2 3
1 2 3 4
2 3 4 5
0 1 2
1 2 3
2 3 4
3 4 5
*/
```

-   2차원 배열을 만들고 출력해보았다.
-   이 때, **첫 번째 차원 >> 2번째 차원 순으로 탐색하는게 성능이 좋다!!!** 
    -   C++에서 **캐시를 첫번째 차원**(여기서는 y) 를 기준으로 하기 때문에 **캐시관련 효율성 때문에 탐색을** **하더라도 순서**를 지켜주자.