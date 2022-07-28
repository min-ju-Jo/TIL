## 1. Circle 인스턴스 만들기

- 아래와 같은 Circle 클래스가 있을 때 , 반지름이 3 이고 x, y 좌표가 (2, 인
  Circle 인스턴스를 만들어 넓이와 둘레를 출력하시오.
  
  ```python
  class Circle:
      pi = 3.14
  
      def __init__(self, r, x, y):
          self.r = r
          self.x = x
          self.y = y
  
      def area(self):
          return Circle.pi*self.r*self.r
  
      def circumference(self):
          return 2*Circle.pi*self.r
  
      def center(self):
          return (
  ```
  
  -----------------
  
  ```python
  circle1 = Circle(3, 2, 4)
  print(circle1.circumference()) #18.84 
  print(circle1.area()) #28.259999999999998
  ```

## 2. Dog와 Bird는 Animal이다.

- 다음과 같이 Animal 클래스가 주어질 때 , 해당 클래스를 상속 받아 아래의 보기와 같이
  동작하는 Dog 클래스와 Bird 클래스를 작성하시오.
  
  ```python
  class Animal:
      def __init__(self, name):
          self.name = name
  
      def walk(self):
          print(f'{self.name}! 걷는다!')
  
      def eat(self):
          print(f'{self.name}! 먹는다!')
  ```
  
  ```python
  dog = Dog('꼽이')
  dog.run() #꼽이! 달린다!
  dog.bark() #꼽이! 짖는다!
  
  bird = Bird('구구')
  bird.walk() #구구! 걷는다!
  bird.eat() #구구! 먹는다!
  bird.fly() #구구! 푸드덕!
  ```
  
  --------- 
  
  ```python
  class Animal:
      def __init__(self, name):
          self.name = name
  
      def walk(self):
          print(f'{self.name}! 걷는다!')
  
      def eat(self):
          print(f'{self.name}! 먹는다!')
  
  class Dog(Animal):
      def run(self):
          print(f'{self.name}! 달린다!')
      def bark(self):
          print(f'{self.name}! 짖는다!')
  
  class Bird(Animal):
      def fly(self):
          print(f'{self.name}! 푸드덕!')
  
  dog = Dog('꼽이')
  dog.run() #꼽이! 달린다!
  dog.bark() #꼽이! 짖는다!
  
  bird = Bird('구구')
  bird.walk() #구구! 걷는다!
  bird.eat() #구구! 먹는다!
  bird.fly() #구구! 푸드덕!
  ```

## 3. Module Import

```python
#fibo.py

def fibo_recursion(n):
    if n < 2:
        return n
    else:
        return fibo_recursion(n-1) + fibo_recursion(n-2)
```

위와 같은 코드가 같은 폴더 안의 fibo.py 파일에 작성되어 있을 때 , 아래와 같은 형태로
함수를 실행 할 수 있도록 하는 import 문을 빈칸 (a), (b), (c)를 채워 넣어 완성하시오.

```python
from __(a)__ import __(b)__ as __(c)__
# (a) : fibo # 파일이름
# (b) : fibo_recursion #함수이름
# (c) : recursion # 받을 이름
```
