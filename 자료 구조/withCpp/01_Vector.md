
> **Vector**

-   **동적인 요소를 할당**할 수 있는 **동적배열**
-   만약 컴파일 시점에 사용해야 할 요소들의 개수를 모른다면 **vector를 사용**해야 한다.

> **특징**

-   **연속된 메모리 공간**에 위치한 **같은 타입의 요소**들의 모음
-   **숫자인덱스**를 기반으로 **랜덤접근**이 가능
-   **중복**을 허용

![](https://blog.kakaocdn.net/dn/cV2rQS/btr0w1lq5aD/2P0Uy2KaY65ZdNJ4crYqtk/img.png)

> **시간 복잡도**

-   **탐색과 맨 뒤의 요소를 삭제하거나 삽입하는데 O(1)**
-   **맨 뒤나 맨 앞이 아닌 요소를 삭제하고 삽입하는데 O(n)** 

> **선언** 

```cpp
vector<타입> 변수명;
```

-   위와 같이 선언한다
-   예를 들어 **int형 vector**를 정의하고 싶다면 **vector<int>**로ㅓ 정의
-   이는 다른 자료구조도 동일

> **예시 코드**

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> v;
int main(){
    for(int i = 1; i <= 10; i++)v.push_back(i);
    for(int a: v) cout << a << " ";
    cout << "\n";
    v.pop_back();
    
    for(int a : v) cout << a << " ";
    cout << "\n";
    
    v.erase(v.begin(), v.begin() + 3);
    
    for(int a : v) cout << a << " ";
    cout << "\n";
    
    auto a = find(v.begin(), v.end(), 100);
    if(a == v.end()) cout << "not found" << "\n";
    
    fill(v.begin(), v.end(), 10);
    for(int a : v) cout << a << " ";
    cout << "\n";
    v.clear();
    cout << "아무것도 없을까?\n";
    for(int a : v) cout << a << " ";
    cout << "\n";
    return 0;    
}
/*
1 2 3 4 5 6 7 8 9 10
1 2 3 4 5 6 7 8 9
4 5 6 7 8 9
not found
10 10 10 10 10 10
아무것도 없을까?
*/
```

> **method**

-   **push_back()**
    -   vector의 뒤에서부터 요소를 더한다. 
    -   **emplace_back()과 동일 -** 더 빠르지만 시간차이 많이 안난다.
-   **pop_back()**
    -   vector 맨 뒤의 요소를 지운다.
-   **erase()** 
    -   한 요소만을 지운다면 **erase(위치)**로 쓰이지만
    -   (from, to]로 지우고 싶다면 
    -   **erase(from, to)**를 통해 지운다.

```cpp
iterator erase (const_iterator position);


iterator erase (const_iterator first, const_iterator last);
```

**※ 참고 - ( 와 ) 는 해당요소를 포함하지 않는 구간, [ 와 ] 는 해당 요소를 포함한다는 수학적 기호**

![](https://blog.kakaocdn.net/dn/ctRbnt/btr0BBesuOK/1mL5BTX71AjKFjvkRGJ5Dk/img.png)

-   **find(from, to, value)**
    -   vector의 메서드가 아닌 **STL** 함수
    -   [from, to) 에서 value를 찾는다.
    -   vector내의 요소들을 찾고 싶을 때 이를 통해 찾는다.
    -   **O(n)의 시간복잡도**
-   **clear()**
    -   vector의 모든 요소를 지운다.
-   **fill(from, to, value)**
    -   vector 내의 value로 값을 할당하고 싶다면 fill을 써서 채운다.
    -   보통 이를 ~~한 값으로 초기화라고 부른다.
    -   [from, to) 구간에 value를 초기화 한다.
-   **범위기반 for 루프**
    -   앞에서 한 번 다뤘었는데 다시 보자
    -   아래 두 코드는 동일한 의미이다.
    -   vector 등 **컨테이너의 요소들을 간편하게 탐색**할 때 사용
    -   **Array, 연결리스트, 맵, 셋을 탐색할 때도 사용**
    -   pair를 담고 있다면 **pair<int, int>** a 로 들어가야됨

```cpp
for(int a : v)
for(int i = 0; i < v.size(); i++)

vector<pair<int, int>> v2;
for(pair<int, int> a : v2) cout << a.first << " ";
```

> **정적할당**

-   vector라고 해서 무조건 크기가 0인 빈 vector를 만들어 동적할당으로 요소를 추가하는 것은 아니다.
-   애초에 크기를 정해놓거나 해당 크기에 대해 어떠한 값으로 **초기화** 해놓고 시작 가능

```cpp
#include <bits/stdc++.h>
using namespace std;
vector<int> v(5,100);
int main() {
    for(int a : v) cout << a << " ";
    cout << "\n";
    return 0;
}

/*
100 100 100 100 100
*/
```

> **2차원 배열**

-   vector를 이용한 2차원 배열을 만드는 방법은 **3가지 존재**  
    -   **vector를 중첩**해서 만든 v
    -   **vector를 중첩해서 만들고 0이란 값으로 초기화 ->** 2차원 배열은 v와 10*10 크기, 0으로 초기화된 v2를 볼 수 있다.
    -   **반복문을 통해 vector 중첩** 시키기

```cpp
#include<bits/stdc++.h>
using namespace std;
vector<vector<int>> v;
vector<vector<int>> v2(10, vector<int>(10,0));
vector<int> v3[10];
int main(){
    for(vector<int> v : v2){
        for(int i : v) cout << i << ' ';
        cout << '\n';
    }
    for(int i = 0; i < 10; i++){
        vector<int> vv;
        v.push_back(vv);
    }
    return 0;
}
```