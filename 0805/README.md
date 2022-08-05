## 03_pjt

#### 프로젝트03 목표

- HTML을 통한 웹 페이지 마크업 이해

- CSS라이브러리의 이해와 활용

- Bootstrap컴포넌트 및 Grid system 을 활용한 반응형 레이아웃 구성

#### 준비사항

- #### Problem 01_nav_footer.html
  
  - Navigation Bar
  
  ```python
  <nav class="navbar navbar-expand-md navbar-dark bg-dark sticky-top">
      <div class="container-fluid">
        <a class="navbar-brand" href="02_home.html">
          <img src="images/logo.png" alt="#" width="90" height="40" class="d-inline-block align-text-top">
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNavDropdown">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link active" aria-current="page" href="02_home.html">Home</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="03_community.html">Community</a>
            </li>
            <li class="nav-item">
              <a class="nav-link"href="#loginModal" data-bs-toggle="modal">Login</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>
  ```
  
  - Modal  
  
  ```python
  <div class="modal fade" id="loginModal" tabindex="-1" aria-labelledby="loginModalLabel" aria-hidden="true">
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h5 class="modal-title fw-bold" id="loginModalLabel">Modal title</h5>
              <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
          </div>
          <!-- Modal Body -->
          <div class="modal-body">
            <form class="row g-3 d-flex flex-column">
              <div>
                <label for="inputUserName" class="form-label">Email address</label>
                  <input type="email" class="form-control" id="inputUserName">
              </div>
              <div class="mb-2">
                <label for="inputPassword" class="form-label">Password</label>
                  <input type="password" class="form-control" id="inputPassword">
              </div>
              <div>
                <div class="form-check">
                  <input class="form-check-input" type="checkbox" id="gridCheck">
                    <label class="form-check-label" for="gridCheck">
                      Check me out
                    </label>
                </div>
              </div>
            </form>
          </div>
          <!-- Modal Footer -->
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
            <button type="button" class="btn btn-primary">Submit</button>
          </div>
        </div>
      </div>
    </div>
  ```
  
  - footer
  
  ```python
  <footer class="d-flex flex-column justify-content-center align-items-center py-3 bg-light fixed-bottom">
      <sapn>Web-bootstrap PJT by____</sapn>
    </footer>
  ```

- #### Problem 02_home.html
  
  - header
    
    - 이미지, 제목 , 설명을 포함합니다
    
    - 이미지는 제공된 영화 포스터 이미지를 사용합니다
  
  ```python
  <header>
      <div id="carouselExampleInterval" class="carousel slide" data-bs-ride="carousel">
        <div class="carousel-inner">
          <div class="carousel-item active" data-bs-interval="1000">
            <img src="images/header1.jpg" class="d-block w-100" alt="...">
          </div>
          <div class="carousel-item" data-bs-interval="2000">
            <img src="images/header2.jpg" class="d-block w-100" alt="...">
          </div>
          <div class="carousel-item">
            <img src="images/header3.jpg" class="d-block w-100" alt="...">
          </div>
        </div>
        <button class="carousel-control-prev" type="button" data-bs-target="#carouselExampleInterval" data-bs-slide="prev">
          <span class="carousel-control-prev-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Previous</span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#carouselExampleInterval" data-bs-slide="next">
          <span class="carousel-control-next-icon" aria-hidden="true"></span>
          <span class="visually-hidden">Next</span>
        </button>
      </div>
    </header>
  ```
  
  - section
    
    - 개별요소들은 좌우 일정한 간격을 가집니다 . 
    
    - Viewport의 가로 크기가 576px 미만일 경우 한 행에 1 개씩 표시됩니다.
    
    - Viewport의 가로 크기가 576px 이상일 경우 한 행에 2 개 이상 표시됩니다.
    
    ```python
    <div class="container">
        <section class="text-center">
          <h3 class="fw-bold my-4">Boxoffice</h3>
        </section>
    
        <article class="text-start">
          <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3">
            <div class="col">
              <div class="card">
                <img src="images/movie1.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>
            <div class="col">
              <div class="card">
                <img src="images/movie2.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>
    
            <div class="col">
              <div class="card">
                <img src="images/movie3.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>
    
            <div class="col">
              <div class="card">
                <img src="images/movie4.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>
    
            <div class="col">
              <div class="card">
                <img src="images/movie5.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>
    
            <div class="col">
              <div class="card">
                <img src="images/movie6.jpg" class="card-img-top" alt="...">
                  <div class="card-body">
                    <h5 class="card-title">Card title</h5>
                    <p class="card-text">This is a longer card with supporting text below as a natural lead-in to additional content. This content is a little bit longer.</p>
                  </div>
              </div>
            </div>  
          </div>
        </article>
      </div>
    ```

#### 03_community.html

- Community 페이지는 크게 게시판 목록 과 게시판 으로 이루어져 있습니다.

- 게시판
  
  ```python
  <div class="container">
      <div class="text-start">
        <h1>Community</h1>
      </div>
  ```

- Aside (게시판 목록)
  
  ```python
  <div class="row">
        <aside class="card col-12 col-lg-2">
          <ul class="list-group list-group-flush">
            <li class="list-group-item list-group-item-action text-primary">BoxOffice</li>
            <li class="list-group-item list-group-item-action text-primary">Movies</li>
            <li class="list-group-item list-group-item-action text-primary">Genres</li>
            <li class="list-group-item list-group-item-action text-primary">Actors</li>
          </ul>
        </aside>
  ```

- Section (게시판) -table
  
  ```python
  <section class="col-12 col-lg-10">
          <div class="d-none d-lg-block">
            <table class="table table-striped"> 
              <thead>
                <tr class="table-dark">
                  <th scope="row">영화 제목</th>
                  <td>글 제목</td>
                  <td>작성자</td>
                  <td>작성 시간</td>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <th scope="row">Great Movie title</th>
                  <td>Best Movie Ever</td>
                  <td>user</td>
                  <td>1 minute ago</td>
                </tr>
                <tr>
                  <th scope="row">Great Movie title</th>
                  <td>Best Movie Ever</td>
                  <td>user</td>
                  <td>1 minute ago</td>
                </tr>
                <tr>
                  <th scope="row">Great Movie title</th>
                  <td>Best Movie Ever</td>
                  <td>user</td>
                  <td>1 minute ago</td>
                </tr>
                <tr>
                  <th scope="row">Great Movie title</th>
                  <td>Best Movie Ever</td>
                  <td>user</td>
                  <td>1 minute ago</td>
                </tr>
              </tbody>
            </table>
          </div>
        </section>
  ```

- Section (게시판) - list
  
  ```python
  <article class="col-12">
          <div class="d-block d-lg-none">
            <hr class="m-20">
            <a href="#" class="list-group-item list-group-item-action">
              <div class="d-flex w-100 justify-content-start">
                <h2 class="mb-1">Best Movie Ever</h2>
              </div>
              <div class="d-flex w-100 justify-content-between">
                <h5 class="mb-1">Great Movie title</h5>
              </div>
              <p class="text-muted">user</p>
              <small class="text-muted">1 minute ago</small>
            </a>
            <hr class="m-20">
            <a href="#" class="list-group-item list-group-item-action">
              <div class="d-flex w-100 justify-content-between">
                <h2 class="mb-1">Best Movie Ever</h2>
              </div>
              <div class="d-flex w-100 justify-content-between">
                <h5 class="mb-1">Great Movie title</h5>
              </div>
              <p class="text-muted">user</p>
              <small class="text-muted">1 minute ago</small>
            </a>
            <hr class="m-20">
            <a href="#" class="list-group-item list-group-item-action">
              <div class="d-flex w-100 justify-content-between">
                <h2 class="mb-1">Best Movie Ever</h2>
              </div>
              <div class="d-flex w-100 justify-content-between">
                <h5 class="mb-1">Great Movie title</h5>
              </div>
              <p class="text-muted">user</p>
              <small class="text-muted">1 minute ago</small>
            </a>
            <hr class="m-20">
            <a href="#" class="list-group-item list-group-item-action">
              <div class="d-flex w-100 justify-content-between">
                <h2 class="mb-1">Best Movie Ever</h2>
              </div>
              <div class="d-flex w-100 justify-content-between">
                <h5 class="mb-1">Great Movie title</h5>
              </div>
              <p class="text-muted">user</p>
              <small class="text-muted">1 minute ago</small>
            </a>
          </div>
        </article>
  ```

- 페이지네이션
  
  ```python
  <nav aria-label="Page navigation example ">
          <ul class="pagination justify-content-center mb-5 pb-3">
            <li class="page-item"><a class="page-link" href="#">Previous</a></li>
            <li class="page-item"><a class="page-link" href="#">1</a></li>
            <li class="page-item"><a class="page-link" href="#">2</a></li>
            <li class="page-item"><a class="page-link" href="#">3</a></li>
            <li class="page-item">
              <a class="page-link" href="#">Next</a>
            </li>
          </ul>
        </nav>
  
      </div>
    </div>
  ```

#### 어려웠던 점

- 메뉴바를 화면 상단에 고정시킬 때 아래 콘텐츠가 가려졌다. 
  
  - fixed-top -> sticky-top 
  
  - fixed는 normal flow를 벗어난다. sticky는 normal flow를 따르고 스크롤링에 따라서 fixed로 전환되기 때문에 stick-top를 써야한다.

- 페이지네이션이 footer 에 의해 가려졌다.
  
  - mb-5 pb-3 클래스를 주면서 margin bottom과 padding bottom을 확보해주었다.
