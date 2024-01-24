---
layout: single
title: "[Python] 리스트의 크기"

categories:
  - python

date: 2024-01-24
last_modified_at: 2024-01-24

---

# 0. 파이썬의 리스트

> 파이썬에서 리스트를 사용하게 되면 c혹은 c++과 다르게 자료형과 상관없이 만들 수 있기 때문에 편리하게 사용이 가능하다. 이 작동 방식을 확인해보자.
> 

---

# 1. 기본 SIZE 확인

> 우선 리스트의 크기를 확인해보기 위해서 **sys**모듈 내부의 **getsizeof()**함수를 사용한다. 해당 함수는 입력되는 자료의 크기를 byte단위로 리턴 해주는 함수이다. 우선 기본적인 자료 형들의 크기를 확인해보자.(vscode기준으로 측정하였다.)
> 

```python
import sys

integer_ = 1
boolean_ = True
char_ = ""
string_ = "gubam"
float_ = 1.25

print(sys.getsizeof(integer_))
print(sys.getsizeof(boolean_))
print(sys.getsizeof(char_))
print(sys.getsizeof(string_))
print(sys.getsizeof(float_))
```

![size 확인](%5BPython%5D%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%84%80%E1%85%B5%209bb71ba1eb094e40923bd6b4ed02ad5a/Untitled.png)

size 확인

![type 확인](%5BPython%5D%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%84%80%E1%85%B5%209bb71ba1eb094e40923bd6b4ed02ad5a/Untitled%201.png)

type 확인

- 위의 사진 같은 결과 같이 나왔고 이를 통해 integer 28, boolean 28, char 50, string 54, float 24 바이트로 나왔다. 이는 기존의 C혹은 C++에서 생각하고 있던 자료형의 사이즈와 많은 차이를 보인다. 이에 대해서 찾아보니 여러 글이 있어서 이는 다음에 찾아보겠다.

- 문자열의 경우 사실 파이썬에서는  char의 자료형이 없고 string 형태이기 때문에 따로 측정할 필요는 없었다. string의 경우 기본적인 크기는 49byte이고 한 글자에 1byte가 추가되는 것을 확인 할 수 있다.

---

# 2. 리스트의 크기 확인

> 리스트의 크기를 확인하기 위해서 우선 아래와 같이 정수 형으로 리스트를 만들어서 비교해 보았다.
> 

```python
import sys

list_ = []
list_int1 = [1]
list_int2 = [1,2]
list_int3 = [1,2,3]

print(sys.getsizeof(list_))
print(sys.getsizeof(list_int1))
print(sys.getsizeof(list_int2))
print(sys.getsizeof(list_int3))
```

```python
import sys

list_ = []#텅빈 리스트
list_str1 = [""]
list_str2 = ["","a"]
list_str3 = ["","a","ab"]
list_bool = [True]
list_float = [1.25]

print(sys.getsizeof(list_))
print(sys.getsizeof(list_str1))
print(sys.getsizeof(list_str2))
print(sys.getsizeof(list_str3))
print(sys.getsizeof(list_bool))
print(sys.getsizeof(list_float))
```

![Untitled](%5BPython%5D%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%84%80%E1%85%B5%209bb71ba1eb094e40923bd6b4ed02ad5a/Untitled%202.png)

![Untitled](%5BPython%5D%E1%84%85%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B3%20%E1%84%8F%E1%85%B3%E1%84%80%E1%85%B5%209bb71ba1eb094e40923bd6b4ed02ad5a/Untitled%203.png)

- 우선 왼쪽의 코드로 아무것도 들어 있지 않은 기본 리스트는 56바이트가 나왔고 자료 한 개에 8바이트가 추가되는 것을 볼 수 있다. 다른 자료형의 경우에도 확인을 해보기 위해서 오른쪽의 코드를 입력해 보았다.

- 우측의 코드를 통해서 리스트의 경우에는 내부에 어떠한 자료형인지 상관없이 데이터 당 8byte인 것을 확인 할 수 있다. 혹시나 싶어서 string 자료형의 길이를 아주 길게 늘려서 측정을 해보았는데 사이즈의 변화는 없었다.

---

# 3. 결론

> 우선 리스트의 크기를 확인해보기 위해서 각 자료형의 크기를 측정해 보았고 그 결과는 아래의 표와 같이 출력이 되었다. 그리고 리스트의 경우에도 아래의 표와 같고 내부에 **어떠한 자료형이 들어가든 자료 한 개가 8 byte**를 차지한다는 것을 확인 할 수 있다.
> 

---

| 종류 | 크기(byte) |
| --- | --- |
| int | 28 |
| float | 24 |
| string | 49 |

| 종류 | 크기(byte) |
| --- | --- |
| [ ] | 56 |
| [1] | 64 |
| [1 , 2] | 72 |
