## 01_web_workshop_0801

#### nth-child()와 nth-of-type()

(1) nth-child

- nth-child 는 모든 요소를 포함해서 카운팅한다. 

- #m > p:nth-child(2) -> 모든 요소 중 두번째 꺼 -> 첫번째 단락이 red로.

```python
<div id="m">
  <h2>어떻게 선택 될까?</h2>
  <p>첫번째 단락</p>
  <p>두번째 단락</p>
  <p>세번째 단락</p>
  <p>네번째 단락</p>
</div>
<style>
  #ssafy > p:nth-child(2) {
    color: red;
  }
</style>
```

(2) nth-of-type

- nth-of-type 는 특정 요소만을 순서로 카운팅한다.

- #m > p:nth-of-type(2) -> p요소 중 두번째꺼 -> 두번째 단락이 red로.

```python
<div id="m">
  <h2>어떻게 선택 될까?</h2>
  <p>첫번째 단락</p>
  <p>두번째 단락</p>
  <p>세번째 단락</p>
  <p>네번째 단락</p>
</div>
<style>
  #ssafy > p:nth-of-type(2) {
    color: red;
  }
</style>
```

(3) nth-child()와 nth-of-type() 의 차이점

| nth-child(n)         | nth-of-type(n)       |
| -------------------- | -------------------- |
| 부모 안에 모든 요소 중 n번째 요소 | 부모 안에 특정 요소 중 n번째 요소 |
