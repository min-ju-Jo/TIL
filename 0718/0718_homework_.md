## 1. Python 예약어

```
import keyword
print(keyword.kwlist)


```

- ['False', 'None', 'True', '__peg_parser__', 'and', 'as', 'assert', 'async', 'await', 'break', 'class', 'continue', 'def', 'del', 'elif', 'else', 'except', 'finally', 'for', 'from', 'global', 'if', 'import', 'in', 'is', 'lambda', 'nonlocal', 'not', 'or', 'pass', 'raise', 'return', 'try', 'while', 'with', 'yield']

## 2. 실수 비교

```
# 1. 임의의 작은 수 활용
print((num1-num2) < 0.00000000001)

# 2. 
import math
print(math.isclose(num1, num2)
```

## 3. 이스케이프 시퀀스

### (1) 줄 바꿈 \n

### (2) 탭 \t

### (3) 백슬래시 \\\

## 4. String Interpolation

```
name = '철수'
#1
print('안녕, %s' % name)
#2
print(f'안녕, {name})
```

## 5. 형 변환

```
# ValueError
int('3.5')
```

## 6. 네모 출력

```
n, m = 5, 9
#1
print(('*'*n + '\n')*m)
#2
print(('*'*n + '\n')*(m-1)+'*'*n)
```



## 7. 이스케이프 시퀀스 응용

```
print('\"파일은 c:\\Windows\\Users\\내문서\\Python에 저장이 되었습니다.\"\n나는 생각했다. \'cd를 써서 git bash로 들어가 봐야지.\'')
```

## 8. 근의 공식

```
#1
-b +- (b**2 - 4 * a *c)**(1/2) / 2

#2
import math
-b +- math.sqrt(b**2 - 4 * a *c) / 2
```


