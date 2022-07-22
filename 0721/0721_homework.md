## 1. 위치 인자와 키워드 인자

- 다음과 같이 함수가 선언되어 있을 때 , 보기 (1)~(4) 중에서 실행 시
  오류가 발생하는 코드를 고르시오.

```python
def ssafy(name, location = '서울') :
    print(f'{name}의 지역은 {location}입니다.') 

# (1)
ssafy('가흔') # 가흔의 지역은 서울입니다.
# (2)
ssafy(location = '부울경', name = '승현') # 승현의 지역은 부울경입니다.
# (3)
ssafy('지우', location = '서울') # 지우의 지역은 서울입니다.
# (4)
ssafy(name = '승호', '광주') # SyntaxError: positional argument follows keyword argument
```

## 2. 가변 인자 리스트

- 가변
  인자 리스트를 사용하여 , 개수가 정해지지 않은 여러 정수들을 전달 받아
  해당 정수들의 평균 값을 반환하는 my_avg 함수를 작성하시오.

```python
def my_avg(*numbers) :
    result = 0
    for number in numbers :
        result += number
    print(result/len(numbers))
my_avg(77, 83, 95, 80, 70)
```

## 3. 반환값

- 다음과
  같이 함수를 선언하고 호출하였을 때 , 변수 result 에 저장된 값과
  그 값이 나온 이유를 작성하시오.

```python
def my_func(a, b) : 
    c = a + b
    print(c)

result = my_func(3, 7) 
print(result) # None 

# return 
def my_func(a, b) : 
    return a + b

result = my_func(3, 7) 
print(result) # 10
```

## 4. 이름 공간(Namespace)

- Python에서 변수를 찾을 때 접근하는 이름 공간을 순서대로 작성하시오.
  
  - 파이썬에서 사용되는 이름(식별자)들은 이름공간(namespace)에 저장되어 있음.
  
  - 아래와 같은 순서로 이름을 찾아나가며, LEGB Rule이라고 부름.
    
    - Local scope : 지역 범위 ( 현재 작업 중인 범위 )
    
    - Enclosed scope : 지역 범위 한 단계 위 범위
    
    - Global scope : 최상단에 위치한 범위
    
    - Built-in scope : 모든 것을 담고 있는 범위 ( 정의하지 않고 사용할 수 있는 모든 것)

## 5. 매개변수와 인자 , 그리고 반환

- 아래의 보기 (1) ~ (4) 중에서 , 옳지 않은 것을 고르시오
  
  - (1) 함수는 오직 하나의 객체만 반환할 수 있으므로 'return a, b' 와 같이 쓸 수 없다.
    
    - 튜플을 활용하여 두 개 이상의 값 반환 할 수 있다.
  
  - (2) 함수에서 return 을 작성하지 않으면 None 값을 반환한다.
  
  - (3) 함수의 매개변수 (parameter)는 함수를 선언할 때 설정한 값이며  전달 인자        (argument)는 함수를 호출할 때 넘겨주는 값이다.
  
  - (4) 가변 인자를 설정할 때는 함수 선언 시 매개변수 앞에 * 을 붙이고 , 이 때는 함수내에서 tuple로 처리 된다 .
