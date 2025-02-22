# 음반 검색 사이트 : 띵반 모음집


목차

## 팀원 및 역할

오기쁨(팀장) : 메인페이지 및 디자인 전반, 게시글 작성 페이지 크롤링 모듈 개발(python/js [POST]method) <br>
유도원 : 회원가입 및 로그인 <br>
안다민 : 게시판 상세보기 및 작성 <br>

## 프로젝트 소개

<p align="justify">
지니뮤직의 앨범 상세페이지의 파라미터값을 활용하여 유저들 간의 앨범 추천, 리뷰를 남길 수 있는 커뮤니티 게시판<br>
  <li> 게시글 작성 시 지니뮤직 앨범 상세페이지의 파라미터값을 작성하면 인풋값을 받아 크롤링 데이터를 가공하여 js에서는 response 값을 프론트 페이지에 노출</li>
  <li> 게시글 DB 저장 시 크롤링 데이터와 사용자 입력 데이터를 1개의 아이템으로 [POST]</li>
</p>

## <a href="https://www.notion.so/joyfive/C-7-SA-d39031182ebb4444aca55339cf89f7f4">SA</a>

## <a href="https://youtu.be/MFXuNat4a0I">Youtube 시연 링크<a>

<br>

## 기술 스택

HTML / CSS / JavaScript / Python / Flask / mongoDB

<br>

## 구현 기능

### 기능 1 : 회원가입 및 로그인
- jwt 이용한 회원가입 및 로그인 기능 구현
- 토글 버튼을 이용한 상황에 맞는 회원가입, 로그인 요소  
- 해시 함수를 이용한 패스워드 암호화
- 로그인 시 토큰에 저장된 정보로 인증하여 페이지  
- 로그아웃 시 토큰 삭제

### 기능 2 : 메인페이지
#### 1) 리스팅 기능 [GET]method
- DB에 저장된 게시글 데이터 리스트 형태로 find 및 역순으로 sort (최신 게시글 노출)
- json 활용하여 프론트로 데이터 전달
- js for 문으로 개별 아이템별 딕셔너리 value 호출 
- temp_html로 가공된 데이터 사용자 노출

#### 2) 상세페이지 이동링크
- 게시글 저장 시 jinja 방식으로 구현한 상세url 활용* 
- temp_html 내 링크 연결 시 데이터의 'num' 필드 값을 활용한 상세페이지 url 이동

### 기능 3 : 게시글 입력 및 확인
#### 1) 크롤링 모듈 동작 : 
- JS) 사용자 input 값을 파라미터로 치환하여 POST 요청 
- Python) bs4 크롤링 및 데이터 가공 후 프론트로 response 전달 
- JS) 가공데이터로 temp_html 사용자 노출

#### 2) write.html 
- Jinja2 템플릿 엔진을 이용한 서버사이드 렌더링으로 게시판 기능 구현 
- 사용자가 지니뮤직의 파라미터값 입력 시 크롤링 모듈 동작
- 가공데이터로 전달받은 response 값은 사용자 노출 및 게시글 데이터 저장 시 같이 저장 
- 글제목+내용+별점 입력 후 함께 mongoDB에 데이터 저장 
- 게시글 작성 
- 메인페이지 정상 리스팅 확인

#### 3) view.html 
- 매개변수 keyworld [jinja] 상세 페이지 url 분기 [GET]:jinja를 활용한 서버사이드렌더링 방식
- write에서 POST한 크롤링데이터 및 사용자 데이터 find
- json으로 프론트에서 상세

<br>

## 배운 점 & 아쉬운 점

(기쁨)
<b> 배운 점</b>
<크롤링 데이터 가공>
- 지니뮤직 기존 예제 외 앨범 상세페이지 / 곡 상세페이지 크롤링 성공
- 라우트 내에서 파라미터값 변수로 치환하여 크롤링 성공
- 사용자 인풋 박스 값 POST로 Python에서 크롤링 후 DB 저장없이 프론트로 response 전달 성공
- 테스트 프론트 페이지에서 데이터 정상 노출여부 확인 후 모듈 전달(js / python)

<메인페이지 리스팅>
- GET method (Python API/ js ajax) 및 function 내 데이터 변수 지정, temp_html  복습
- 변수형 상세페이지 url 이동 링크 활용
- 리스트 역순 노출 (sort)

<협업>
- Jinja를 활용한 매개변수 상세페이지 코드 디버깅 작업 협업
- 게시글 작성 페이지 랜딩 링크 변수 활용 (temp_html > href 내 js변수삽입)
- 팀원 작업파일의 전체적인 html/css 수정을 통한 UI 통일 

<b>아쉬운 점</b>
- 초기 아이디어 중 좋아요, 로그인 시 유저 닉네임 노출 등 몇가지 기능을 축소하면서 진행하게 되어서 아쉬움
- 메인페이지+크롤링기능 / 게시판 모듈(백/프론트)/ 회원 모듈(백/프론트)로 나누어 진행해서, 웹개발 플러스 강의의 메인 기능들을 많이 못 써본 것이 아쉽지만, 팀원들의 코드를 함께보며 디버깅 하면서 개념을 잡을 수 있었음

(도원)
배운점 <br>
- 토큰을 활용한 회원가입, 로그인, 로그아웃 방법
- 해시 함수 활용법
- 토큰을 활용한 페이지 접근 방법
- 상황에 맞는 요소를 토글 버튼으로 활용

아쉬운점 <br>
-로그인 회원가입 토글 사용법
-프로필 변경과 회원탈퇴

(다민)
배운 점 <br>
- post한 곳이 아닌 다른 페이지에서 get해올 수 있게 하는 게시판 방법 터득
- 크롤링 자료와 작성 자료 동시 데이터 저장 방법 터득
- 데이터 정렬 역순화
- github conflict 해결

아쉬운 점 <br>
- 좋아요 기능 구현
- 게시물 삭제 및 수정


<p align="justify">

</p>

<br>

## 라이센스

Copyright 2022. hang-hae99 9th W1 team C7. all rights reserved.
