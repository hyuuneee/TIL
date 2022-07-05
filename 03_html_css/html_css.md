## 목차

1. [HTML, CSS 기본 개념](#HTML,-CSS-기본-개념)

   1. [이클립스에서 사용하기](#이클립스에서-사용하기)

2. [HTML 기본](#HTML-기본)

   1. [기본 구조](#기본-구조)
   2. [태그 (TAG)](#태그-(TAG))

   

## HTML, CSS 기본 개념

* HTML은 뼈대, CSS는 꾸미기!
* HTML은 크게 head와 body로 구성되며, head안에는 페이지의 속성 정보를, body안에는 페이지의 내용을 담는다. 
* CSS는 <head>~</head> 안에 <style>~</style> 로 공간을 만들어 작성한다.

#### 이클립스에서 사용하기

* TOMCAT 서버와 같은 WAS(Web Apllication Server)가 필요하다.
* 기존 실행 중인 서버는 실행을 중지하고 이클립스에서 이를 복제한 가상 서버를 사용한다. 

## HTML 기본 

#### 기본 구조

* `<!doctype html>`은 현재 문서가 HTML5 언어로 작성한 웹 문서라는 뜻이다.
* `<html>~</html>` 은 웹 문서의 시작과 끝을 나타내는 태그이다. 웹 브라우저가 <html> 태그를 만나면 </html>까지 소스를 읽어 화면에 표시한다.
* `<head>~</head>`은 웹 브라우저가 웹 문서를 해석하는 데 필요한 정보를 입력하는 부분이다.
* `<meta>`는 문자 세트 등 문서 정보를 나타낸다.
* `<title>~</title>`은 문서의 제목을 나타낸다.
* `<body>~</body>`은 실제로 웹 브라우저 화면에 나타나는 내용이다. 

#### 태그 (TAG)

* `<!-- ~ -->` : 주석 
* `<h1>제목</h1>` : 제목을 표시할 때 사용하는 태그. 크기에 따라 h1~h6까지 사용 가능하다.
* `<p>~</p>` : 입력한 내용 앞뒤로 빈 줄이 생기면서 텍스트 단락이 만들어진다.
* `<br>` : 줄 바꾸기
* `<strong>`, `<b>` : 굵게 표시
* `<em>`, `<i>` : 기울임꼴
* `<s>`, `<del>`, `<strike>` : 취소선
* `&nbsp` : 공백
* `&lt;`, `&gt;` : <, >
* `<a>` : 링크, 파일 다운로드
  * `href` : 주소
  * `target` : _blank(새창으로 열기), _self(현재창으로 열기(생략))
  * 텍스트에 링크 걸기 : `<a href="https://www.naver.com/" target="_blank" title="네이버로 이동하기!">네이버</a>` 
  * 이미지에 링크 걸기 : `<a href="tag02_img.html"><img src="../img/05.jfif"/></a>`
    * `<img/>` : 웹페이지에 이미지 포시하기
    * `src`  : 사용할 이미지 파일명
    * `width` : 폭(px, %)
    * `height` : 높이(px)
    * `alt` : 이미지가 없을 때 표시
    * 예시 : `<img src="../img/03.jfif" width="100%" height="300px"/>`
  * 파일 다운로드 : `<a href="../downFile/mysql_demo.sql">demo.sql 다운로드하기</a>`
  * 이미지 다운로드 : `<a href="../img/03.jpg" download>이미지 다운로드</a>`
  * 1개의 이미지를 여러 곳으로 나눠 링크 걸기 : `<map>~</map>`,  `<area/>`
    * `shape` : 링크 모양(rect, circle, poly)
    * `coords` : 좌표
    * `href` : 이동할 페이지
    * 예시 : `<area shape="poly" coords="70,210,160,240,100,270,10,265" href="../index.html" target="_blank" title="제주국제공항"/>`

