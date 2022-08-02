## 02_web_homework_0802

#### 1. Semantic Tag

- HTML 태그가 특정 목적, 역할 및 의미적 가치를 가지는 것.

- HTML5에서 새롭게 추가된 시맨틱(semantic) 태그
  
  - header, section, footer

#### 2. input Tag

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  <label for="name">USERNAME:</label>
  <input type="text" id="name" placeholder="아이디를 입력 해 주세요."><br>
  <label for="password">PWD:</label>
  <input type="text" id="password" >
  <input type="submit" value="로그인">
</body>
</html>
```

#### 3. 크기 단위

- em
  
  - (바로 위, 부모 요소에 대한) 상속의 영향을 받음.
  
  - 배수 단위, 요소에 지정된 사이즈에 상대적인 사이즈를 가짐.

- rem
  
  - (바로 위, 부모 요소에 대한) 상속의 영향을 받지 않음.
  
  - 최상위 요소(html)의 사이즈를 기준으로 배수 단위를 가짐.

#### 4. 선택자

- 자손 결합자
  
  - <div> 태그 밑에 소속된 모든 <p> 태그를 선택자로 지정.
  
  ```python
  div p{
      color: crimson;
  }
  ```

- 자식 결합자
  
  - <div> 태그의 자식 관계인  <p> 태그를 선택자로 지정.
  
  ```python
  div > p{
      color: crimson;
  }
  ```
