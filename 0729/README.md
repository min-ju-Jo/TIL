## 02_pjt

#### 프로젝트02 목표

- 데이터 구조에 대한 분석과 이해

- 요청과 응답에 대한 이해

- API의 활용과 API 문서 숙지

#### 준비사항

- API
  
  - TMDB API 영화 정보 및 API 서비스
  
  - My API 생성 :  72abd96085f1b006d69e19aa2de25d95

- 필수 라이브러리 Requests
  
  - pip list -> 라이브러리 종류 확인
  
  - pip install requests -> 라이브러리 requests 설치

#### Problem

A. 

- 접근방법
  
  - requests 라이브러리를 사용하여 TMDB 에서 현재 인기있는 영화 목록
    (Get Popular) 데이터를 요청해서 response에 응답받는다 . 
  
  - URL 
    
    - required : api key -> My API
  
  - 응답 받은 데이터 형태 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 인기있는 영화 데이터를 담고 있다.
  
  - 응닫 받은 데이터의 영화 개수 반환하기 위해 빈 리스트 생성하고 results의 values의 리스트안에서 반복문을 사용하여 딕셔너리를 한 줄씩 읽으며 id의 values를 리스트에 추가하였다.
  
  - 영화의 id 값들이 들어있는 리스트 길이를 사용하여 영화의 개수를 반환하였다. 

- 새로 알게 된 것
  
  - 가장 먼저 응답받은 데이터의 형태를 확인하는 과정이 중요하다는 것을 알게 되었다. 

- 코드
  
  ```python
      base_URL = 'https://api.themoviedb.org/3/'
      path = 'movie/popular'
      params = { 
          'api_key' : '72abd96085f1b006d69e19aa2de25d95',
          'language' : 'en-US',
          'page' : 1
      }
      response = requests.get(base_URL + path, params = params).json()
  ```
  
  ```python
  import requests
  from pprint import pprint
  
  def popular_count():
      URL = 'https://api.themoviedb.org/3/movie/popular?api_key=72abd96085f1b006d69e19aa2de25d95&language=en-US&page=1' 
      response = requests.get(URL).json()
  
      lst = []
      for i in response['results']:
          lst.append(i['ㅑ'])
      return len(lst)
  
  # 아래의 코드는 수정하지 않습니다.
  if __name__ == '__main__':
      print(popular_count())
  ```

B. 

- 접근방법
  
  - TMDB에서 현재 인기있는 영화 목록(Get Popular) 데이터를 요청해서 response에 응답받는다.
  - URL
    - required : api key -> My API
  - 응답 받은 데이터 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 인기있는 영화 데이터를 담고 있다.
  - 응답 받은 데이터 중 평점 vote_average 이 8 점 이상인 영화 목록을 반환하기 위하여 빈 리스트 생성하고 results의 values의 리스트안에서 반복문을 사용하여 딕셔너리를 한 줄씩 읽으며 vote_average의 value가 8이상인 영화 목록을 리스트에 추가하였다.
  - vote_average 이 8 점 이상인 영화 목록이 들어있는 리스트를 반환하였다.

- 코드
  
  ```python
  import requests
  from pprint import pprint
  
  def vote_average_movies():
      URL = 'https://api.themoviedb.org/3/movie/popular?api_key=72abd96085f1b006d69e19aa2de25d95&language=en-US&page=1' 
      response = requests.get(URL).json()
      lst = []
      for i in response['results']:
          if i['vote_average'] >= 8:
              lst.append(i)
      return lst
  
  # 아래의 코드는 수정하지 않습니다.
  if __name__ == '__main__':
      pprint(vote_average_movies())
  ```

C. 

- 접근방법
  
  - TMDB에서 현재 인기있는 영화 목록(Get Popular) 데이터를 요청해서 response에 응답받는다.
  
  - URL
    
    - required : api key -> My API
  
  - 응답 받은 데이터 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 인기있는 영화 데이터를 담고 있다.
  
  - 응답 받은 데이터 중 평점 vote_average 을 기준으로 평점이 높은 영화 5개 정보를 리스트로 반환 받기 위해 먼저, 20개의 영화목록의 vote_average 의 value를 리스트형태로 lst1을 생성하였다.
  
  - 20개의 영화목록의 vote_average 값들이 들어있는 리스트를 ``sort``메서드를 사용하여 가장 높은 순으로 정렬하였다. 
  
  - 평점이 가장 높은 순으로 정렬 된 리스트에서 높은 순으로 5개의 정보를 가져오기 위해 for i in range(5) 를 사용하여 lst1에서 인덱스 0,1,2,3,4의 값을 갖는 영화 목록을 다시 새로운 리스트에 생성하였다.

- 어려웠던 부분
  
  - 20개의 평점들을 높은 순으로 정렬된 리스트에서 높은 순으로 5개의 값들을 확인해보았을 때 -> 8.3, 8.1, 8, 7.7, 7.7  
  
  - 처음에는 이중 반복문을 사용하여 20개의 영화목록들을 한 줄씩 읽으면서 인덱스 0,1,2,3,4의 값들과 평점이 같은 영화목록을 가져왔을 때 평점 7.7을 갖는 영화가 두개이므로 리스트에 중복되어 추가되었다.
  
  - 위 문제를 해결하기 위해 if 조건을 한번 더 사용하여 두번씩 추가 되는 것을 해결하긴 하였지만 이게 맞는건가 의문이 들긴 하다. 

- 새로 알게 된 것
  
  - 리스트.sort() -> 내림차순 정렬
  
  - 리스트.sort(reverse = True) -> 오름차순 정렬

- 코드
  
  ```python
  import requests
  from pprint import pprint
  
  def ranking():
      URL = 'https://api.themoviedb.org/3/movie/popular?api_key=72abd96085f1b006d69e19aa2de25d95&language=en-US&page=1' 
      response = requests.get(URL).json()
  
      lst1 = []
      for i in response['results']:
          lst1.append(i['vote_average'])
          lst1.sort(reverse=True)
  
      lst2 = []
      for i in range(5):
          for j in response['results']:
              if j['vote_average'] == lst1[i]:
                  if j not in lst2 :
                      lst2.append(j) 
      return lst2
  
  # 아래의 코드는 수정하지 않습니다.
  if __name__ == '__main__':
      pprint(ranking())
  ```

D. 

- 접근방법
  
  - 제공된 영화 제목으로 TMDB에서 영화를 검색(Search Movies)하여 response에 응답 받는다.
  
  - URL
    
    - required : api_key -> My API, query -> 영화제목을 받는다.
    
    - optional : language -> ko-KR
  
  - query='기생충'으로 응답 받은 데이터 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 '기생충'과 관련된 영화 목록을 담고 있다.
  
  - Search Movies하여 응답 받은 결과에서 첫번째 영화의 id 값을 찾는다. 이때, 검색한
    영화 정보가 없다면 None 을 반환하기 위하여 if문을 사용하여 빈 리스트라면 None을 반환해주었다.
  
  - 가져온 첫번째 영화의 id 값을  movie_id 에 받고, 해당하는 영화에 대한 추천 영화 목록(Get Recommendations)을 데이터를 요청해서 response에 응답받는다.
  
  - URL
    
    - required : api_key -> My API, movie_id -> Search Movies하여 응답 받은 결과에서 첫번째 영화의 id 값
    
    - optional : language -> ko-KR
  
  - '기생충' 관련 영화에서 첫 번재 id를 movie_id=496243으로 응답받은 데이터 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 추천 영화 목록을 담고 있다.
  
  - 추천 영화 목록의 title을 출력하는 리스트를 반환하였다.

- 어려웠던 부분
  
  - 데이터를 두번 요청하는 부분이 처음에 접근하기 어려웠다. 처음 Search Movies 에서 required에 해당하는 query에 영화 title을 받아오고, 여기서 또 아이디를 저장해서 두번째 Get Recommendations 에서 required 에 해당하는 movie_id를 받아오는 것에서 시간이 걸렸다. 데이터만 잘 요청해서 응답받는다면 그 다음은 해결하기 괜찮았던 것 같다.
  
  - 검색한 영화 정보가 없다면 None 을 반환하는 부분에서 접근하기 어려웠다. 검색한 영화정보가 있는 경우와 없는 경우를 비교하는 부분에서 print로 과정을 출력해보고 두 경우가 어떤 점에서 차이가 있는지 확인하는 과정을 거쳐 반복문을 사용하여 해결하였다.
  
  - 과정을 계속해서 출력해가면서 확인하는 과정이 중요하다는 것을 알게 되었다.

- 코드
  
  ```python
      base_URL = 'https://api.themoviedb.org/3/'
      path = 'search/movie'
      params = { 
          'api_key' : '72abd96085f1b006d69e19aa2de25d95',
          'language' : 'ko-KR',
          'page' : 1,
          'query' : title
      }
      response = requests.get(base_URL + path, params = params).json()
  ```
  
  ```python
      base_URL = 'https://api.themoviedb.org/3/'
      path = f'movie/{movie_id}/recommendations'
      params = { 
          'api_key' : '72abd96085f1b006d69e19aa2de25d95',
          'language' : 'ko-KR',
          'page' : 1
      }
      response = requests.get(base_URL + path, params = params).json()
  ```
  
  ```python
  import re
  from unittest import result
  import requests
  from pprint import pprint
  
  def recommendation(title):
      query = title
      URL = f'https://api.themoviedb.org/3/search/movie?api_key=72abd96085f1b006d69e19aa2de25d95&language=ko-KR&page=1&include_adult=false&query={query}'
      response = requests.get(URL).json()
  
      if len(response['results']) == 0:
          return None
      else:
          movie_id = response['results'][0]['id']
  
      URL = f'https://api.themoviedb.org/3/movie/{movie_id}/recommendations?api_key=72abd96085f1b006d69e19aa2de25d95&language=ko-KR&page=1'
      response = requests.get(URL).json()
  
      lst=[]
      for i in response['results']:
          lst.append(i['title'])
      return lst
  
  # 아래의 코드는 수정하지 않습니다.
  if __name__ == '__main__':
      pprint(recommendation('기생충'))
      pprint(recommendation('그래비티'))
      pprint(recommendation('검색할 수 없는 영화'))
  ```

E.

- 접근방법
  
  - 제공된 영화 제목으로 TMDB에서 영화를 검색(Search Movies)하여 response에 응답 받는다.
  
  - URL
    
    - required : api_key -> My API, query -> 영화제목을 받는다.
    
    - optional : language -> ko-KR
  
  - query='기생충'으로 응답 받은 데이터 확인 -> page와 results를 key로 갖고 있는 딕셔너리 형태, results의 values은 리스트 안에 딕셔너리들로 '기생충'과 관련된 영화 목록을 담고 있다.
  
  - Search Movies하여 응답 받은 결과에서 첫번째 영화의 id 값을 찾는다. 이때, 검색한
    영화 정보가 없다면 None 을 반환하기 위하여 if문을 사용하여 빈 리스트라면 None을 반환해주었다.
  
  - 가져온 첫번째 영화의 id 값을 movie_id 에 받고, 해당하는 영화에 대한 출연진과 스태프목록(Get Credits)을 데이터를 요청해서 response에 응답받는다.
  
  - URL
    
    - required : api_key -> My API, movie_id -> Search Movies하여 응답 받은 결과에서 첫번째 영화의 id 값
    
    - optional : language -> ko-KR
  
  - '기생충' 관련 영화에서 첫 번재 id를 movie_id=496243으로 응답받은 데이터 확인 -> id, cast, crew를 key로 갖고 있는 딕셔너리 형태, cast의 values은 리스트 안에 딕셔너리들로 출연진 목록을 담고 있고, crew의 values은 리스트 안에 딕셔너리들로 d연출진 목록을 담고 있다.
  
  - 출연진은 cast_id 값이 10 미만인 출연진만 추출하고 연출진은 스태프 부서가 Directing 인 데이터만 추출 받아 각각 리스트로 생성하였다.
  
  - 각각 생성한 리스트를 딕셔너리의 value로 새로운 딕셔너리로 반환하였다.

- 어려웠던 부분
  
  - D에서 데이터를 요청하고 응답하는 부분이 같았기에 D를 하고 하니 E가 수월하긴 하였다.

- 코드
  
  ```python
  import requests
  from pprint import pprint
  
  def credits(title):
      query = title
      URL = f'https://api.themoviedb.org/3/search/movie?api_key=72abd96085f1b006d69e19aa2de25d95&language=ko-KR&page=1&include_adult=false&query={query}'
      response = requests.get(URL).json() 
  
      if response['results'] == []:
          return None
      else:
          movie_id = response['results'][0]['id']
  
      URL = f'https://api.themoviedb.org/3/movie/{movie_id}/credits?api_key=72abd96085f1b006d69e19aa2de25d95&language=ko-KR'
      response = requests.get(URL).json()
  
      cast_list = []
      directing_list = []
  
      for i in response['cast']:
          if i['cast_id'] < 10:
              cast_list.append(i['name'])
  
      for i in response['crew']:
          if i['department'] == 'Directing':
              directing_list.append(i['name'])
  
      my_dict = {'cast': cast_list, 'directing' : directing_list}
      return my_dict
  
  if __name__ == '__main__': 
      pprint(credits('기생충'))
      pprint(credits('검색할 수 없는 영화'))
  ```
