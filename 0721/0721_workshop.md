## 1. 간단한 N의 약수 (SWEA #1933)

- 입력으로 1 개의 정수 N 이 주어진다 . 정수 N 의 약수를 오름차순으로 출력하는
  프로그램을 작성하시오.

```python
"""
[제약 사항]
N은 1 이상 1,000 이하의 정수이다 . (1 ≤ N ≤ 1000)
[입력]
입력으로 정수 N 이 주어진다
[출력]
정수 N 의 모든 약수를 오름차순으로 출력한다
[입력 예시]
10
[출력 예시]
1 2 5 10 """

numb = int(input())
for i in range(1, numb+1):
    if numb % i == 0:
        print(i, end=' ') 
```

## 2. List의 합 구하기

- 정수로만 이루어진 list 를 전달 받아 해당 list 의 모든 요소들의 합을 반환하는
  list_sum 함수를 built in 함수인 ``sum()`` 함수를 사용하지 않고 작성하시오.

```python
lst = [1, 2, 3, 4, 5]
def list_sum():
    result = 0
    for i in lst:
        result = result + i
        print(result)
list_sum()
#
def list_sum(lst):
    result = 0
    for i in lst:
        result = result + i
    return result
print(list_sum([1, 2, 3, 4, 5]))
```

## 3. Dictionary로 이루어진 List의 합 구하기

- Dictionary로 이루어진 list 를 전달 받아 모든 dictionary 의 'age' key 에 해당하는 value
  들의 합을 반환하는 dict_list_sum 함수를 built in 함수인 ``sum()`` 함수를 사용하지 않고
  작성하시오.

```python
#
lst = [{'name':'kim', 'age':12}, {'name':'lee', 'age':4}]
def dict_list_sum():
    a = 0
    for i in lst:
        a = a + i['age']
    print(a)
dict_list_sum()
#
def dict_list_sum(lst):
    a = 0
    for i in lst:
        a = a + i['age']
    return a
print(dict_list_sum([{'name':'kim', 'age':12}, {'name':'lee', 'age':4}]))
```

## 4. 2차원 List의 전체 합 구하기

- 정수로만 이루어진 2 차원 list 를 전달 받아 해당 list 의 모든 요소들의 합을 반환하는
  all_list_sum 함수를 built in 함수인 ``sum()`` 함수를 사용하지 않고 작성하시오

```python
#
lst = [[1],[2, 3], [4, 5, 6], [7, 8, 9, 10]]
def all_list_sum():
    a = 0
    for i in lst:
        for j in i :
            a = a + j
    print(a)
all_list_sum()

#
def all_list_sum(lst):
    a = 0
    for i in lst:
        for j in i :
            a = a + j
    return a
print(all_list_sum([[1],[2, 3], [4, 5, 6], [7, 8, 9, 10]]))
```

## 5. 숫자의 의미

- 정수로 이루어진 list 를 전달 받아 , 각 정수에 대응되는 아스키 문자를 이어붙인
  문자열을 반환하는 get_secret_word 함수를 작성하시오 .
  단, list 는 65 이상 90 이하 그리고 97 이상 122 이하의 정수로만 구성되어 있다.

```python
#
lst = [83, 115, 65, 102, 89]
def get_secret_word():
    for i in lst :
        print(chr(i), end='')
get_secret_word()

#
def get_secret_word(lst):
    a = ''
    for i in lst :
        a += chr(i)
    return a
print(get_secret_word([83, 115, 65, 102, 89]))
```

## 6. 내 이름은 몇일까?

- 문자열을 전달 받아 해당 문자열의 각 문자에 대응되는 아스키 숫자들의 합을 반환하는
  get_secret_number 함수를 작성하시오 . 단 , 문자열은 A~Z, a~z 로만 구성되어 있다.

```python
#
a = 'happy'
def get_secret_number():
    s = 0
    for i in range(len(a)):
        s += ord(a[i])
    print(s)
get_secret_number()

#
def get_secret_number(a):
    s = 0
    for i in range(len(a)):
        s += ord(a[i])
    return s
print(get_secret_number('happy')) 
```

## 7. 강한 이름

- 문자열 2 개를 전달 받아 두 문자열의 각 문자에 대응되는 아스키 숫자들의 합을
  비교하여 더 큰 합을 가진 문자열을 반환하는 get_strong_word 함수를 작성하시오
  단, 두 문자열의 아스키 숫자의 합이 같은 경우 , 둘 다 반환하세요.

```python

```
