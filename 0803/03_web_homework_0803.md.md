## 03_web_homework_0803.md

#### Bootstrap

#### 1. Button 만들기

```python
<button type="submit" class="(a) (b)">Submit</button>
```

`(a)` : btn

`(b)` : btn-primary

#### 2. Navbar 만들기

```python
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <!-- CSS only -->
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-0evHe/X+R7YkIZDRvuzKMRqM+OrBnVFBL6DOitfPri4tjfHxaWutUpFmBp4vmVor" crossorigin="anonymous">
  <!-- JavaScript Bundle with Popper -->
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.2.0-beta1/dist/js/bootstrap.bundle.min.js" integrity="sha384-pprn3073KE6tl6bjs2QrFaJGz5/SUsLqktiwsUTF55Jfv3qYSDhgCecCxMW52nD2" crossorigin="anonymous"></script>
  <title>Document</title>
</head>
<body>
    <nav class="navbar navbar-expand-lg navbar-(a) bg-(a)">
        <div class="container-fluid">
            <a class="navbar-brand" href="#">
          <img src="my.png" alt="my" width="70" height="30" class="d-inline-block align-top">
        </a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDarkDropdown" 
                aria-controls="navbarNavDarkDropdown" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
         </button>
            <div class="collapse navbar-collapse" id="navbarNavDropdown">
                <ul class="(b)">
            <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="(c)" role="button" data-bs-toggle="dropdown" 
                            aria-expanded="false">아침
                        </a>
                        <ul class="dropdown-menu dropdown-menu-light" aria-labelledby="navbarBreakfast">
                            <li><a class="dropdown-item" href="#">오믈렛</a></li>
                            <li><a class="dropdown-item" href="#">샌드위치</a></li>
                            <li><a class="dropdown-item" href="#">팬케이크</a></li>
                            <li><a class="dropdown-item" href="#">김밥</a></li>
                            <li><a class="dropdown-item" href="#">주먹밥</a></li>
                        </ul>
                    </li>
                    <li class="nav-item dropdown">
                        <a class="nav-link dropdown-toggle" href="#" id="navbarLunch" role="button" data-bs-toggle="dropdown" 
                            aria-expanded="false">점심 
                        </a>
                        <ul class="dropdown-menu dropdown-menu-light" aria-labelledby="navbarLunch">
                            <li><a class="dropdown-item" href="#">샐러드</a></li>
                            <li><a class="dropdown-item" href="#">떡볶이</a></li>
                                <li><a class="dropdown-item" href="#">햄버거</a></li>
                        </ul>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link active" href="#">저녁</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link disable" href="#">야식</a>
                    </li>
                </ul>
            </div>
        </div>
    </nav>
</body>
</html>
```

`(a)` : light

`(b)` : navbar-nav

`(c)` : navbarBreakfast

#### 3. Pagination 만들기

```python
<nav aria-label="...">
      <ul class="(a)">
          <li class="page-item (b)">
              <a class="page-link" href="#" tabindex="-1" aria-disabled="true">Prev</a>
          </li>
          <li class="page-item (c)" aria-current="page">
              <a class="page-link" href="#">1</a>
          </li>
          <li class="page-item"><a class="page-link" href="#">2</a></li>
          <li class="page-item"><a class="page-link" href="#">3</a></li>
          <li class="page-item">
              <a class="page-link" href="#">Next</a>
          </li>
      </ul>
  </nav>
```

`(a)` : pagination

`(b)` : disabled

`(c)` : active
