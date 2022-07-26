## 1. Built-in 함수와 메서드

- ``sorted()``와 ``.sort()``의 차이점을 코드의 실행 결과를 활용하여 설명하시오.
  
  ``.sort()`` : 메서드
  
  ```python
  a = [42, 36, 6, 45, 12, 17]
  result = a.sort()
  print(a, result) #[6, 12, 17, 36, 42, 45] None
  ```
  
  ``sorted()`` : 함수
  
  ```python
  b = [31, 23, 44, 18, 33, 10]
  result = sorted(b)
  print(b, result) #[31, 23, 44, 18, 33, 10] [10, 18, 23, 31, 33, 44]
  ```

## 2. .extend()와 .append()

- ``.extend()``와 ``.append()``의 차이점을 코드의 실행 결과를 활용하여 설명하시오.
  
  ``append()`` : 메서드, a[len(a) : ] = [x] 와 동일합니다.
  
  ```python
  cafe = ['starbucks', 'tomntoms', 'hollys']
  cafe.append('banapresso') 
  #['starbucks', 'tomntoms', 'hollys', 'banapresso']
  ```
  
  ``.extend()`` : 메서드, a[len(a) : ] = iterable 와 동일합니다.
  
  ```python
  cafe = ['starbucks', 'tomntoms', 'hollys']
  cafe.extend(['wcafe', '뺵다방'])
  #['starbucks', 'tomntoms', 'hollys', 'wcafe', '뺵다방']
  ```

- append vs extend
  
  ```python
  cafe = ['starbucks', 'tomntoms', 'hollys']
  cafe.append(['banapresso'])
  #['starbucks', 'tomntoms', 'hollys', 'banapresso']
  ```
  
  ```python
  cafe = ['starbucks', 'tomntoms', 'hollys']
  cafe.append('banapresso')
  #['starbucks', 'tomntoms', 'hollys', 'b', 'a', 'n', 'a', 'p', 'r', 'e', 's', 's', 'o' ]
  ```

## 3. 복사가 잘 된 건가?

- 아래의 코드를 실행 하였을 때, 변수 a와 b에 담긴 list의 요소가 같은지 혹은 다른지
  여부를 판단하고 그 이유를 작성하시오

```python
a = [1, 2, 3, 4, 5]
b = a 
a[2] = 5 
print(a) #[1, 2, 3, 4, 5]
print(b) #[1, 2, 3, 4, 5]
```
