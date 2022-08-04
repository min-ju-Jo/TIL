## 04_web_homework_0804.md

#### 1. CSS flex-direction

- Flex box의 주축을 변경하는 flex-direction의 4가지 값과 각각의 특징을 작성하시오.
  
  ###### Main axis 기준 방향 설정
  
  - row : Main axis 가로
  
  - row-reverse : Main axis 가로, 순서 오른쪽에서 왼쪽
  
  - column : Main axis 세로
  
  - column-reverse : Main axis 세로, 순서 아래에서 위

#### 2. Bootstrap flex-direction

- flex-direction의 4가지 요소와 대응하는 bootstrap 클래스를 작성하시오.
  
  - row : flex-row
  
  - row-reverse : flex-row-reverse
  
  - column : flex-column
  
  - column-reverse : flex-column-reverse

#### 3. align-items

- align-items 속성의 4가지 값과 각각의 특징을 작성하시오.
  
  ###### Cross axis 중심으로
  
  - stretch : 컨테이너를 가득 채움
  
  - flex-start : 위
  
  - flex-end : 아래
  
  - center : 가운데
  
  - baseline : 텍스트 baseline에 기준선을 맞춤

#### 4. flex-flow

- flex-flow 속성은 두가지 속성의 축약형이다. 올바르게 짝지어진 것을 고르시오.
  
  ```python
  (1) flex-direction, flex-wrap
  (2) flex-direction, align-items
  (3) justify-content, flex-wrap
  (4) justify-content, align-items
  ```
  
  - (1) flex-direction, flex-wrap

#### 5. Bootstrap Grid System

```python
<div class="(a)">
  <div class="(b)">
    <div class="col-(c)-(d)"></div>
  </div>
</div>
```

- Bootstrap Grid System을 적용시키고자한다. 

- (a), (b) 각각에 입력해야 할 클래스 이름을 작성하시오.

``(a)`` : container

``(b)`` : row

#### 6. Breakpoint prefix

- Bootstrap Grid System에서 요소의 크기를 지정하기 위해서는 상단 코드와 같은 형태로
  클래스 이름을 지정해야 한다. 
  
  1) (c) 에 들어갈 수 있는 값들과 그 값들이 가지는 의미를 작성하시오. 
  2) (d) 에 들어갈 수 있는 값들과 그 값들이 가지는 의미를 작성하시오.

``(c)`` : sm, md, lg, xl, xxl : 디바이스 또는 화면의 크기에 따라 응답을 조정하며 반응형 디자인을 구현 할 수 있도록 함

``(d)`` : 12이하의 정수 : 12개로 나누어진 공간에서 몇 칸을 차지하는지 표시한다.
