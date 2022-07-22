## 01_pjt

#### 프로젝트01 목표

- 파일 입출력에 대한 이해

- 데이터 구조에 대한 분석과 이해

- 데이터를 가공하고 JSON 형태로 구성하기

#### Problem

A. 제공하는 영화데이터의 주요내용 수집 

- 접근 방법
  
  - movie.json 데이터의 형태는  리스트 안에 딕셔너리로 하나의 영화 데이터가 담겨져 있는 것을 확인하였다.
  
  - 빈 딕셔너리를 생성하고 리스트 안에 들어있는 딕셔너리에서 문제에서 주어진 key값들과 value값들의 정보를 추출해서 새로운 딕셔너리로 반환하였다.

- 새로 배운 것
  - pprint 함수로 인해 딕셔너리의 key 순서가 정렬되어서 출력되는 것을 알게되었다.

- 코드
  
  ```python
  import json
  from pprint import pprint
  
  def movie_info(movie):
      new_dict = {}
      new_dict['id'] = movie_dict['id']
      new_dict['title'] = movie_dict['title']
      new_dict['poster_path'] = movie_dict['poster_path']
      new_dict['vote_average'] = movie_dict['vote_average']
      new_dict['overview'] = movie_dict['overview']
      new_dict['genre_ids'] = movie_dict['genre_ids']
      return new_dict
  
  if __name__ == '__main__':
      movie_json = open('data/movie.json', encoding='utf-8')
      movie_dict = json.load(movie_json)
  
      pprint(movie_info(movie_dict))
  ```

B. 제공하는 영화데이터의 주요내용 수집

- 접근 방법
  
  - movie.json 데이터의 형태는 리스트 안에 딕셔너리로 하나의 영화 데이터가 담겨져 있고 genres.json 데이터의 형태는 리스트 안에 딕셔너리로 영화의 id와 name의 정보가 담겨져 있다는 것을 확인하였다.
  
  - A에서 반환한 새로운 딕셔너리에서 'genre_ids'의 key값은 두개의 id값이 숫자로 들어있는 리스트 형태이다.
  
  - 새로운 빈 리스트를 생성하고 for문을 사용하여 movie.json의 'genre_ids'의 key인 리스트안에 두개의 id값을 반복하며 genres.json의 id의 value값과 같다면 name의 key값을 리스트에 추가하였다.
  
  - 새로운 리스트를 value로 갖는 'genre_names'의 키로 바꿔 반환하였다.

- 어려웠던 부분
  
  - 딕셔너리의 value이 리스트의 형태였기 때문에 리스트의 요소를 하나씩 반복문으로 꺼내서 조건에 맞게 다시 리스트의 형태로 생성하는 부분을 생각해내는데 시간이 걸렸다. 

- 코드
  
  ```python
  import json
  from pprint import pprint
  
  def movie_info(movie, genres):
      new_dict = {}
      new_dict['id'] = movie['id']
      new_dict['title'] = movie['title']
      new_dict['poster_path'] = movie['poster_path']
      new_dict['vote_average'] = movie['vote_average']
      new_dict['overview'] = movie['overview']
  
      lst = []
      for i in movie['genre_ids']:
          for j in genres :
              if i == j['id']:
                  lst.append(j['name'])
  
      new_dict['genre_names'] = lst
      return new_dict
  
  if __name__ == '__main__':
      movie_json = open('data/movie.json', encoding='utf-8')
      movie = json.load(movie_json)
  
      genres_json = open('data/genres.json', encoding='utf-8')
      genres_list = json.load(genres_json)
  
      pprint(movie_info(movie, genres_list))
  ```

C. 다중 데이터 분석 및 수정

- 접근 방법
  
  - movie.json 데이터의 형태는 리스트 안에 딕셔너리로 하나의 영화 데이터가 담겨져 있고 movies.json 데이터의 형태는 리스트안에 딕셔너리로 평점이 높은 20개의 영화 데이터가 담겨져 있다는 것을 확인하였다.
  
  - 새로운 딕셔너리 20개가 리스트에 담겨 반환될 수 있도록 빈 리스트를 생성하였다.
  
  - for문을 사용하여 movies.json에서 리스트안에 딕셔너리를 하나씩 추출해서 그 딕셔너리에서 문제에서 주어진 key값들에 해당하는 정보를 담는 새로운 딕셔너리를 생성하였다. 
  
  - 새로운 딕셔너리 20개를 처음에 만든 빈 리스트에 추가하여 반환하였다. 

- 어려웠던 부분
  
  - movies.json에서 딕셔너리를 한개씩 읽어 A, B를 적용하고 새로운 딕셔너리들을 다시 리스트에 넣어 반환할 수 있는 방법에 대해서 생각하는 점에서 고민을 많이 했다. 

- 코드
  
  ```python
  import json
  from pprint import pprint
  
  def movie_info(movies, genres):
      a = []
      for i in movies:
          new_dict = {}
          new_dict['id'] = i['id']
          new_dict['title'] = i['title']
          new_dict['poster_path'] = i['poster_path']
          new_dict['vote_average'] = i['vote_average']
          new_dict['overview'] = i['overview']
  
          lst = []
          for k in i['genre_ids']:
              for l in genres :
                  if k == l['id']:
                      lst.append(l['name'])
  
          new_dict['genre_names'] = lst
  
          a.append(new_dict)
      return a
          
  if __name__ == '__main__':
      movies_json = open('data/movies.json', encoding='utf-8')
      movies_list = json.load(movies_json)
  
      genres_json = open('data/genres.json', encoding='utf-8')
      genres_list = json.load(genres_json)
  
      pprint(movie_info(movies_list, genres_list))
  ```

D. 알고리즘을 사용한 데이터 출력

- 접근 방법
  
  - movie.json 데이터의 형태는 리스트 안에 딕셔너리로 하나의 영화 데이터가 담겨져 있고 movies 폴더 내부의 데이터들은 딕셔너리로 각 영화의 세부정보를 담고 있다는 것을 확인했다.
  - 빈 리스트를 만들고 for문을 사용하여 movie.json의 리스트안에 딕셔너리를 하나씩 읽어서 그 딕셔너리에서 id에 해당하는 value값을 문자열로 변환하여 빈 리스트에 추가하여 문자열 형태로 영화들의 id값이 담겨져 있는 새로운 리스트를 생성하였다.
  - for 문을 사용하여 새로운 리스트의 id값들에 해당하는 movies폴더 내부의 파일안의 딕셔너리를 하나씩 읽어서 revenue에 해당하는 value값이 내가 max값을 정한 변수보다 크게 되면 max값을 그 value값을 바꾸고 그 때의 id값을 새로운 변수에 정의하였다.
  - revenue값이 가장 큰 영화의 id값을 가진 파일을 읽어 그 딕셔너리 안의 title의 value 값을 반환하였다.

- 어려웠던 부분
  
  - 폴더내부의 파일들을 불러온다는 것이 막막했다. 폴더내부의 파일들의 이름이 id.json이였으므로 이를 이용해서 불러올 수 있었지만 만약 파일들의 이름이 다르다면 어떻게 불러와야 할지는 잘 모르겠다.
  
  - 내가 max로 정한 변수를 처음에 정의하는 것을 for문안에서 하다가 계속 마지막 영화의 제목이 반환되었다. 문제점을 처음에 찾지 못하다가 0으로 정의한 max변수의 위치가 잘못 되었다는 것을 알게 되었다.  max로 정한 변수가 for문 안에 위치하게 된다면 for문 안에서의 if문으로 조건이 맞을 때 그 변수를 바꾸는 조건문을 실행 되어도 다시  for문이 반복될 때 max로 정한 변수가 0이라는 줄도 같이 반복되면 0으로 리셋되어 실행되었던 것이다.  for문 밖으로 꺼내니 해결되었다. 

- 코드
  
  ```python
  import json
  
  def max_revenue(movies):
      lst = []
      for t in movies :
          lst.append(str(t['id']))
  
      a = 0
      for i in lst :
          movies_json = open('data/movies/'+ i +'.json' , encoding='utf-8')
          movies_list = json.load(movies_json)
          
          if movies_list['revenue'] > a:
              a = movies_list['revenue']
              b = i
  
      movies_json = open('data/movies/'+ b +'.json' , encoding='utf-8')
      movies_list = json.load(movies_json)
      return movies_list['title']
  
  if __name__ == '__main__':
      movies_json = open('data/movies.json', encoding='utf-8')
      movies_list = json.load(movies_json)
      
      print(max_revenue(movies_list))
  
  ```

E. 알고리즘을 사용한 데이터 출력

- 접근 방법
  
  - movie.json 데이터의 형태는 리스트 안에 딕셔너리로 하나의 영화 데이터가 담겨져 있고 movies 폴더 내부의 데이터들은 딕셔너리로 각 영화의 세부정보를 담고 있다는 것을 확인했다.
  
  - 빈 리스트를 만들고 for문을 사용하여 movie.json의 리스트안에 딕셔너리를 하나씩 읽어서 그 딕셔너리에서 id에 해당하는 value값을 문자열로 변환하여 빈 리스트에 추가하여 문자열 형태로 영화들의 id값이 담겨져 있는 새로운 리스트를 생성하였다.
  
  - 두번째의 빈리스트 만들고 for문을 사용하여 첫번째로 만든 리스트 안에서의 id에 해당하는 파일들을 하나씩 불러와서 딕셔너리의 release_data에 해당하는 value값에서 월이 12인 영화의 title에 해당하는 value값을 두번째 리스트에 추가하였다.
  
  - 개봉일이 12월인 영화들의 제목이 담겨져 있는 리스트를 반환하였다.

- 어려웠던 부분
  
  - 영화들의 id값을 문자열로 변화하여야 하는 부분과 개봉일이 12월인 부분에서 12를 문자열로 입력하야한다는 부분에서 오류가 났다. 정수가 아니라 문자열로 받는 부분을 주의해야할 것 같다.

- 코드
  
  ```python
  import json
  
  def dec_movies(movies):
      lst = []
      for t in movies :
          lst.append(str(t['id']))
          
      new_lst =[]
      for j in lst:
          movies_json = open('data/movies/'+ j +'.json' , encoding='utf-8')
          movies_list = json.load(movies_json)
          if movies_list['release_date'][5:7] == '12':
              new_lst.append(movies_list['title'])
      return new_lst
  
  if __name__ == '__main__':
      movies_json = open('data/movies.json', encoding='utf-8')
      movies_list = json.load(movies_json)
      
      print(dec_movies(movies_list))
  ```
  
  
