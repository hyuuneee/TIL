## 목차

1. [HTML, CSS 기본 개념](#HTML,-CSS-기본-개념)

   1. [이클립스에서 사용하기](#이클립스에서-사용하기)
2. [HTML 기본](#HTML-기본)
   1. [기본 구조](#기본-구조)
   2. [태그 (TAG)](#태그-(TAG))
   
3. [CSS 기본](#CSS-기본)
   1. [스타일시트](#스타일시트)
   2. [CSS 기본 선택자](#CSS-기본-선택자)
   2. [CSS 속성](#CSS-속성)


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
* `<ol>, <li>` : 순서가 있는 목록 
* `<ul>, <li>` : 순서가 없는 목록 (disk, circle, square)
* `<dl>, <dt>, <dd>` : 설명 목록
* `<table>` : 표 만들기
  * `<caption>` : 표 제목
  * `<tr>` : 행
  * `<td>` : 셀
  * `<th>` : 제목 셀
  * `<colspan>` : 열 합치기
    * `<td colspan="합칠 셀의 개수">셀의내용</td>`

  * `<rowspan>` : 행 합치기
  * `border` : 경계선
  * `<colgroup>, <col>` : column을 그룹으로 만드는 태그
* `<iframe>` : 웹페이지 내에 웹페이지 표시
  * `src` : 파일명
  * `<width>, <height>` : 폭, 높이
  * `<frameborder>` : 구분선
  * `<scrolling>` : 스크롤바 (yes[기본값], no)
* `<meta>` : 페이지에 대한 설명을 기술
  * `name` 속성 
    * `description` : 페이지에 대한 설명
    * `keywords` : 검색엔진에 검색되는 단어들
    * `author` : 작성자

  * `http-equiv` 속성
    * `refresh` : 새로고침(초단위)
    * `Refresh` : 일정시간이 지나면 자동으로 페이지 이동
* `<audio>`, `<video>` : 음성파일, 영상파일 재생하기
  * `src` : 재생할 사운드,영상 파일
  * `controls` : 컨트롤바
  * `autoplay` : 자동재생
  * `loop` : 반복재생
  * `preload` : 전송완료 후 재생
  * `width, height` : 플레이어의 너비와 높이
  * `poster="파일이름"` : video태그에서 사용, 비디오 재생 전까지 화면에 표시될 이미지 지정
* `<form>` : 폼을 만드는 기본 태그
  * `method` : 데이터 전송방식 (get-공개[기본값], post-숨김)
  * `action` : 서버페이지 파일명
  * `<input>` 태그의 `type` 속성들
    * text, passwords, search, url, email, tel, checkbox, radio, number, color, range, date, month, week, time, datetime, datetime-local, **submit**(submit이 발생하면 action이 실행됨), reset, **image**(submit버튼과 같은 기능), button, file, **hidden**(사용자에게는 보이지 않지만 서버로 넘겨주는 값이 있는 필드를 만들때)
  * placeholder : 입력란에 표시하는 힌트, 필드를 입력하면 사라짐
  * required : 필수 입력 필드
  * autofocus : 페이지를 불러오자마자 원하는 폼 요소에 마우스 커서 표시
  * readonly : 입력 금지
  * textarea : 여러줄의 텍스트 
    * cols, rows : 칸, 줄 지정
  * `<select>, <outgroup>, <option>` : 여러 옵션 중 선택, 드롭다운 목록
    * size : 드롭다운 항목의 개수 (select 태그 속성) 
    * multiple : 목록에서 둘 이상의 항목을 선택할 때 사용 (select 태그 속성)
    * label : 그룹 이름 (outgroup 태그 속성)
* oncontextmenu : 마우스 오른쪽버튼 메뉴 제어
* onselectstart, ondragstart  : 드래그 시작 불가능
* ondragend  : 드래그 종료 불가능




## CSS 기본

* 기본 형식 : 선택자 {속성1: 속성값1; 속성2:속성값2 }
* 주석 : /* ~ */

#### 스타일 시트

* 인라인(inline) 스타일 : 스타일 시트를 사용하지 않고 스타일을 적용할 대상에 직접 표시, 스타일을 적용하고 싶은 태그에 style 속성을 사용해 style="속성:속성값;" 형태로 스타일 적용
* 내부(internal) 스타일 시트 : 웹 문서 안에서 사용할 스타일을 문서 안에 정리한 것, 모든 스타일 정보는 `<head>~</head>` 태그 안에서 정의,  `<style>~</style>`태그 사이에 작성
* 외부(external) 스타일 시트 : 여러 웹 문서에서 사용할 스타일을 별도 파일로 저장해 놓고 필요할 때마다 파일에서 가져와 사용, style태그 없이 link태그만 사용해 미리 만들어 놓은 외부 스타일시트 파일 연결

#### CSS 기본 선택자

* 태그 선택자 : 문서에서 특정 태그를 사용한 모든 요소에 스타일이 적용됨, 여러 태그에 같은 스타일 적용 가능

  * ```
    span, b, strong{ 
     	color:#0000ff; 
     	font-weight:bold; 
     	font-size:30px;
     }
    ```

* id 선택자 : 요소의 특정 부분에만 스타일 적용, #다음에 id이름 지정, 문서 안에서 한번만 사용한다면 id 선택자로 정의

  * ```
    #txt{
     	background:#ddd; 
     }
    ```

* 클래스 선택자 : 요소의 특정 부분에만 스타일 적용, 마침표(.) 다음에 클래스 이름 지정, 문서 안에서 여러번 반복할 스타일이라면 클래스 선택자로 정의, 같은 클래스를 여러곳에 중복 선언 가능

  * ```
    .a{
     	background:#8a3;color:#fff;font-size:50px; 
    }
    ```




#### CSS 속성

* **배경과 관련된 속성**

  * background-color : 배경색
  * background-image:url() : 배경이미지
  * background-repeat : 반복처리 (no-repeat, repeat-x, repeat-y)
  * background-position : left, center, right, top, middle, bottom, 백분율
  * background-attachment : 배경 고정 (fixed, scroll)
  * background-size : px, %
  * opacity : 투명도 (0~1)
  * background 로 묶어서 한번에 지정 가능

* **그림자, 그라데이션**

  * text-shadow:왼/오른px  위/아래px  그림자색상; : 글자에 그림자 설정
  * box-shadow:위와 동일 : 박스에 그림자 설정
  * 그라데이션 : http://colorzilla.com/gradient-editor 를 사용

* **텍스트 관련 스타일**

  * font-size : 글자 크키 (px[기본16 px], pt, cm, mm, in, em[현재글자크기 기준으로 정함])
  * font-family : 글꼴 (여러개 지정가능)
  * color : 글자 색상
  * font-weight : 글자 굵기 (normal, bold, bolder, lighter...)
  * text-decoration : linethrough(취소선), underline(밑줄), overline(윗줄), none(선없음)
  * text-align : 텍스트 정렬 (start,end,left,right,center..)
  * line-height : 문단의 줄 높이 (height의 값과 똑같이 지정하면 세로 정렬 가능)

* **테두리 (border)**

  * 4개 방향 값 지정 순서 : top->right->bottom->left
  * border-style : 테두리 스타일
    * solid(실선), dotted(점선), dashed(--), double(이중선), none(테두리 없음), groove(홈), inset(볼록), hidden(숨기기)
  * border-width : 테두리 두께 (px)
  * border-color : rgb코드, 컬러명
  * border-radius : 테두리 둥글게
  * border로 묶어서 한번에 지정 가능

* **여백 (margin, padding)**

  * margin : 테두리 밖의 여백
    * 가운데 정렬하기 : margin-left와 margin-right의 속성값을 auto로 지정
    * 요소 중첩 : 요소를 세로로 배치할 때, 마진과 마진이 만날 때 마진이 큰 쪽으로 겹쳐지는 것
  * padding : 테두리와 콘텐츠 사이의 여백

* **레이아웃 만들기**

  * display : 요소의 배치 방법 , 선택된 객체를 보여주거나 숨길 수 있음, 숨김 상태에서 공간 반납
    * block, inline, inline-block, none(숨김)
  * visibility : 선택된 객체를 보여주거나 숨길 수 있음, 숨겨져도 원래 공간 유지
    * visible, hidden
  * float : 정렬 (left, right, none)

* **위치 지정하기**

  * position : 요소들을 배치하기
    * static : 기본값, 좌표x
    * absolute : 페이지 시작점 기준 이동, 원래 공간 없어짐, 감싸고 있는 태그의 포지션에 따라 기준이 달라짐
    * relative : 원래 자리에서 이동, 공간 유지
    * fixed : 지정한 위치에 고정
  * left, top, right, bottom 사용하여 위치 지정

* **목록 스타일**

  * life-style-type : list 헤더 설정
    * none(기호 없음), disc, circle, square, decimal....

* **속성선택자**

  * 지정한 속성을 가진 요소를 찾아 스타일 적용
  * =
  * $= : 특정값으로 끝나는 태그를 선택
  * ^= : 특정값으로 시작하는 태그를 선택
  * *= : 특정값의 일부가 일치하는 태그를 선택

* **가상 클래스 선택자** 

  * 사용자 동작에 반응
    * link : 방문하지 않은 링크에 스타일 적용
    * visited : 방문한 링크에 스타일 적용
    * hover : 웹요소에 마우스 커서를 올려놓았을 때 스타일 적용
    * active : 마우스를 클릭했을 때 스타일 적용
    * focus : 웹 요소에 초점이 맞춰졌을 때 스타일 적용
  * 요소 상태에 따른 선택자 (상태선택자)
    * target : 앵커로 연결된 부분에 스타일 적용
    * enabled, disabled : 요소의 사용 여부에 따라 스타일 적용(활성화, 비활성화)
    * checked : 라디오 버튼이나 체크 박스에 체크했을 때 스타일 적용

* **가상 요소**

  * ::first-line : 첫번째 줄에 스타일 적용
  * ::first-letter : 첫번째 문자에 스타일 적용
  * ::selection : 선택 영역에 스타일 적용

* **구조선택자**

  * nth-child(2n) : 짝수번째
  * nth-child(2n+1) : 홀수번째
  * nth-child(3n) : 3의배수번째
  * first-child : 첫번째 객체
  * last-child : 마지막 객체

* **연결선택자**

  * 자식 선택자 : 자식 요소에 스타일 적용 (두요소 사이 부등호(>)표시)

  * 후손 선택자 : 부모 요소에 포함된 모든 하위 요소에 적용, 자식 요소뿐 아니라 손자, 손자의 손자요소 등 모든 하위요소까지 적용 (상위요소 하위요소)

  * 동위 선택자 

    * 선택자A+선택자B : 선택자A의 바로 다음에 있는 선택자B를 선택
    * 선택자A~선택자B : 선택자A 다음의 모든 선택자B를 선택 (다른 태그가 나올때까지)

    
