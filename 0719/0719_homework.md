## 1. Mutable & Immutable

- mutble : List, Set, Dictionary

- lmmutable : String, Tuple, Range
  
  

## 2. Dictionary 만들기

```
dictionary = {'이한빈' : 30 , '오지원' : 26}
```




## 3. 평균 구하기

```
#1
average = sum(scores) / len(scores)
#2
print((scores[0] + scores[1] + scores[2] + scores[3]) / 4 )
#3
tmp_sum = 0
cnt = 0
for value in scores :
    tmp_sum += value
    cnt += 1
print(tmp_sum/cnt)
```
