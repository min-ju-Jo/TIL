## 1. 무엇이 중복일까

- 문자열을 전달 받아 해당 문자열에서 중복해서 나타난 문자들을 담은 list를 반환하는
  duplicated_letters 함수를 작성하시오.
  
  ```python
  def duplicated_letters(a):
      lst = []
      for i in a:
          if a.count(i) >= 2:
              if i not in lst:
                  lst.append(i)
      return lst
  print(duplicated_letters('apple')) #['p']
  print(duplicated_letters('banana')) #['a', 'n']
  ```

## 2. 소대소대

- 문자열을 전달 받아 해당 문자열을 소문자와 대문자가 번갈아 나타나도록 변환하여
  반환하는 low_and_up 함수를 작성하시오.
  이때, 전달 받는 문자열은 알파벳으로만 구성된다.
  
  ```python
  def low_and_up(a):
      f = ''
      for i in range(len(a)):
          if i % 2 :
              f += a[i].upper()
          else :
              f += a[i]
      return f
  print(low_and_up('apple')) #aPpLe
  print(low_and_up('banana')) #bAnAnA
  ```

## 3. 솔로 천국 만들기

- 정수 0부터 9까지로 이루어진 list를 전달 받아, 연속적으로 나타나는 숫자는 하나만 남
  기고 제거한 list를 반환하는 lonely 함수를 작성하시오.
  이때, 제거된 후 남은 수들이 담긴 list의 요소들은 기존의 순서를 유지해야 한다.
  
  ```python
  def lonely(lst):
      new_lst= []
      new_lst.append(lst[0])
      for i in range(1, len(lst)):
          if new_lst[len(new_lst)-1] != lst[i]:   
              new_lst.append(lst[i])
      return new_lst
  print(lonely([1, 1, 3, 3, 0, 1, 1])) #[1, 3, 0, 1]
  print(lonely([4, 4, 4, 3, 3])) #[4, 3]
  ```
  
  


