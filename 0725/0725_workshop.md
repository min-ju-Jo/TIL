## 1. 평균 점수 구하기

- key 값으로 과목명 , value 값으로 점수를 가지는 dictionary 를 전달 받아 , 전체 과목의
  평균 점수를 반환하는 함수 get_dict_avg 함수를 작성하시오.
  
  ```python
  def get_dict_avg(my_dict):
      sum_score = 0
      for i in my_dict.values():
          sum_score += i
      return sum_score / len(my_dict) #85.5
  
  print(get_dict_avg({'python' : 80, 'web' : 83, 'algorithm' : 90, 'django' : 89}))
  ```

## 2. 혈액형 분류하기

- 여러 사람의 혈액형 (A, B, AB, 에 대한 정보가 담긴 list 를 전달 받아 , key 는 혈액형의
  종류 , value 는 사람 수인 dictionary 를 반환하는 count_blood 함수를 작성하시오.
  
  ```python
  def count_blood(my_lst):
      my_dict = {}
      for i in my_lst:
          my_dict.update({i:my_lst.count(i)})
      return my_dict #{'A': 3, 'B': 3, 'O': 3, 'AB': 3}
  print(count_blood(['A', 'B', 'A', 'O', 'AB', 'AB', 'O', 'A', 'B', 'O', 'B', 'AB']))
  ```

- 답
  
  #처음에 초기값 설정해주어야한다. 
  
  #위 코드는 만약 A가 10명이라면 B가 몇 명인지 알 수 없다.
  
  ```python
  def count_blood(my_lst):
      my_dict = {}
      dic = {"A" : 0, "B" : 0, "O" : 0, "AB" : 0}
      for i in my_lst:
          if i == "A":
              dic["A"] += 1
          elif i == "B":
              dic["B"] += 1
          elif i == "O":
              dic["O"] += 1
          else :
              dic["AB"] += 1
          my_dict.update(dic)
      return my_dict
  print(count_blood(['A', 'B', 'A', 'O', 'AB', 'AB', 'O', 'A', 'B', 'O', 'B', 'AB']))
  ```
  
  
