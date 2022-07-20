## 1. Built-in 함수

- map

- filter

- range

- int

- sum

## 2. 홀수만 담기

- range와 slicing을 활용하여 1부터 50까지의 숫자 중,
  홀수로만 이루어진 리스트를 만드시오.

```python
lst = []
for i in range(1, 51) :
    lst.append(i)
print(lst[slice(0, 49, 2)])

# print(lst[:50:2])
```

## 3. 반복문으로 네모 출력

- 두 개의 정수 n과 m이 주어졌을 때, 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 별(*) 문자를 이용하여 출력하시오. 단, 반복문을 사용하여 작성하시오.

```python
for i in range(9):            # 9번 반복. 세로 방향
    for j in range(5):        # 5번 반복. 가로 방향
        print('*', end='')    # 별 출력. end에 ''를 지정하여 줄바꿈을 하지 않음
    print() 
```

## 4. 조건 표현식

- 주어진 코드의 조건문을 조건 표현식으로 바꾸어 작성하시오.

```python
# 주어진 코드
temp = 36.5
if temp >= 37.5 :
    print('입실 불가')
else :
    print('입실 가능')
```

```python
# 조건 표현식
temp = 35.5
result = '입실 불가' if temp >= 37.5 else '입실 가능'
print(result)
```

## 5. 정중앙 문자

- 문자열을 전달 받아 해당 문자열의 정중앙 문자를 반환하는 get_middle_char 함수를
  작성하시오. 단, 문자열의 길이가 짝수일 경우에는 정중앙 문자 2개를 반환한다.

```python
a = input()
def get_middle_char(a) :
    return a[(len(a)-1)//2 : len(a)//2 + 1]
print(get_middle_char(a))
```


