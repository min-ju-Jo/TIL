## 01_web_homework_0801

#### 1. HTML 정의

- Hyper Text Markup Language

#### 2. HTML 개념

- 웹 표준을 만드는 곳은 Mozilla 재단이다.(F)
  
  - 웹 표준을 만드는 곳은 `W3C`, `WHATWG` 이다.
    - [W3C 링크](https://www.w3.org/Consortium/) (World Wide Web Consortium)
    - [WHATWG 링크](https://whatwg.org/) (Web Hypertext Application Technology Working Group)

- 표(table) 을 만들 때에는 반드시 <th> 태그를 사용해야 한다.(F)
  
  - 반드시 `th`를 사용해야할 필요는 없다.
  
  ```HTML
  <table>
    <tr>
      <td>Month</td>
      <td>Savings</td>
    </tr>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
  </table>
  ```
  
  - `<td>` 만으로도 가능하다.
  - [HTML Tag 설명 링크](https://www.w3schools.com/tags/tag_table.asp)

- 제목(Heading) 태그는 제목 이외에는 사용하지 않는 것이 좋다.(T)
  
  - 시맨틱 태그들은 그 의미에 맞도록 사용하는 것이 권장된다.
    - `<header>` `<nav>` `<aside>` `<footer>` , etc...

- 리스트를 나열하기 위해서는 <ul> 태그만 사용 할 수 있다.(F)
  
  - 리스트 태그는 `ul`, `ol` 을 사용 할 수 있으며 각각의 리스트 아이템은 `li`를 사용한다.
    
    - 리스트 태그는 `ul`, `ol` 을 사용 할 수 있으며 각각의 리스트 아이템은 `li`를 사용한다.
      
      - `ul` 은 unlisted로 순서 無
      - `ol` 은 ordered로 순서 有
    
    - 중첩 리스트 사용
      
      - ```
        <ul>
            <li>List item one</li>
            <li>List item two with subitems:
                <ul>
                    <li>Subitem 1</li>
                    <li>Subitem 2</li>
                </ul>
            </li>
            <li>Final list item</li>
        </ul>
        ```

- HTML의 태그는 반드시 별도의 닫는 태그가 필요하다.(F)
  
  - 여는 태그와 닫는 태그가 한 쌍인 태그와 별도의 닫는 태그가 필요하지 않은 태그가 존재한다.
    - `<br>` `<hr>` `<img>` , etc ...

#### 3. CSS 정의

- Cascading Style Sheets

#### 4. CSS개념

- HTML 과 CSS 는 각자 문법을 갖는 별개의 언어이다.(T)
  
  - HTML과 CSS는 같은 파일 안에 작성될 수는 있지만, 별개의 언어입니다.

- 웹 브라우저는 내장 기본 스타일이 있어 CSS 가 없어도 작동한다.(T)
  
  - 웹 브라우저 별로 내장 기본 스타일(user agent stylesheets)이 있습니다.
  - 그래서 Bootstrap 같은 CSS Framework는 모든 브라우저가 똑같은 출발선에서 CSS가 작성될 수 있도록 하는 reset.css 같은 초기화 css를 포함하고 있습니다.
    - [reset.css 설명 링크](https://meyerweb.com/eric/tools/css/reset/)

- 자식 요소 프로퍼티는 부모의 프로퍼티를 모두 상속 받는다.(F)
  
  - 모두 상속받지 않습니다.
  - 대표적으로 width, height, background-color 와 같은 속성들은 상속되지 않습니다.

- 디바이스마다 화면의 크기가 다른 것을 고려하여 상대 단위인 를 사용한다.(F)
  
  - 디바이스에 따른 상대 단위는 `vw`, `vh` 를 사용 합니다.
  - 백분율 값은 요소의 부모의 크기를 참조하므로 각각의 사용 용도가 다릅니다.

- id 값은 유일해야 하므로 중복되어서는 안된다.(T)
  
  - id 값은 반드시 고유 값이어야 합니다.

#### 5. CSS 우선순위

- `!important` 
- `Inline style`
- `id 선택자`
- `class 선택자`
- `요소 선택자`
- `소스 순서`
