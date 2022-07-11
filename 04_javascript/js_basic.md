## 목차

1. [Javascript](#Javascript)
   1. [기본 용어](#기본-용어)
   2. [변수](#변수)
   3. [함수](#함수)
2. [JS 사용하기](#JS-사용하기)
   1. [배열](#배열)
   2. [날짜와 시간](#날짜와 시간)
   3. [window](#window)
   4. [setInterval](#setInterval)


## Javascript

#### 기본 용어

* 주석 : // , /**/

* 자바스크립트 출력 : **alert**
  * alert("메시지") : 웹브라우저에 경고창(대화상자) 출력
* 조건문과 반복문의 사용법은 JAVA와 같다.

#### 변수

* 변수 : var, let, const
  * 변수타입을 따로 선언할 필요 없다. 초기값에 의해서 데이터형이 정해진다. 초기값을 설정하지 않은 경우에는 undefined
  * var : 선언한 변수가 필요하면 다시 선언할 수 있음
  * let : 같은 블럭내에서 한번만 선언 가능
  * const : 상수화된 변수로 한번만 선언 가능

#### 함수

* 문자열 처리 함수
  * length, indexOf(위치 찾아서 인덱스 반환), search(위치 인덱스 반환), slice(부분 문자열 반환), substring(부분 문자열 반환), substr(시작문자부터 n개의 문자 반환),replace(문자열 대체), toUpperCase(대문자), toLowerCase(소문자), concat(문자열 연결), charAt(해당 위치 문자 반환), charCodeAt(해당 위치 아스키코드 반환), split(문자열 나눠서 배열로 반환)
* Math 함수
  * PI, pow(거듭제곱), round(반올림), ceil(올림), floor(버림), max, min, random....
* 함수 생성하기 : 함수는 **호출**해야 실행됨
  * 방법 1 : function 함수명([매개변수1, 매개변수2...]){실행문}
  * 방법 2 : var 변수명 = function([매개변수1,매개변수2..]){실행문}
  * 방법 3 : var 변수명 = (매개변수1, 매개변수2)=>{실행문}
    * 참고: console.log() : 콘솔 화면에 결과 확인하고 싶을때
    * isNaN (is not a number) : 숫자가 아닐때 true, 숫자일때 false

## JS 사용하기

* document는 body를 가리킨다 . document.write()를 통해 출력 가능.

* 자바스크립트에서 CSS 사용하기

  * document.getElementById("id").style.속성="속성값";

  * css에서 -으로 연결되었던 속성은 -을 없애고 다음 문자를 대문자로 작성

  * 변수에 담아서 사용 가능

    * var dom = document.getElementById("id");

  * 태그 속성 제어 가능

    * document.getElementById("id").value="속성값"

  * 타입 속성 변경

    * document.getElementById("id").type="checkbox"

  * 태그 삽입하기

    * ```html
      var tag = "<h1>javascript에서 태그 삽입</h1>";
      tag += "<ol><li>코스모스</li><li>해바라기</li></ol>";
      ```


#### 배열

* **배열의 선언** : 배열의 크기를 따로 지정하지 않아도 된다. 데이터형이 다른 데이터를 하나의 배열에 보관 할 수 있다.
  * `var arr = new Array();`
  * `var arr2 = new Array(1111,2222,3333,'aaaa','bbbb');`
  * `var arr3 = [23, 45, '가나다', '라마바'];`
* **push** : 배열에 데이터 추가하기
* **join** : 배열의 데이터 연결하기
  * `var txt = arr2.join("/");`
* **pop** : 마지막 데이터 삭제하기
* **배열의 이동**
  * shift : 오른쪽 데이터를 왼쪽으로 이동하고 0번째 index의 값은 지워진다.
  * unshift :  왼쪽 데이터를 오른쪽으로 이동하고 0번째 index값을 작성해야 한다.
* **Json(javascript object notation) 데이터 처리하기**
  * key와 value값을 가진다.
  * `var jData = {username:"홍길동", tel:"010-8934-2253"}`
* **배열 정렬하기**
  * 오름차순 정렬
    * 문자 : 배열명.sort();
    * 숫자 : 배열명:sort(function(x,y){return x-y});
  * 내림차순 정렬
    * 문자 : 배열명.reverse();   --오름차순으로 정렬 후 역순으로 변경한다.
    * 숫자 : 배열명.sort(function(a,b){return b-a});

#### 날짜와 시간

* **Date** : 현재 시스템(사용자 컴퓨터)의 날짜와 시간정보 얻어오기
  * `var now = new Date();`
* **날짜 변경하기** : `var now1 = new Date("2022.10.23");`
* getFullYear():년 / getMonth():월 / getDate():일 / getHours():시 / getMinutes():분 / getSeconds():초 / getDay():요일 (일요일-0,월요일-1...)

#### window

* **팝업창 만들기**

  * window.open("새창에 띄울 파일명", "창이름", "옵션:width, height, left, top...")
  * `win = window.open("popup.html","w","width=400px, height=600px, left=200px, top=200px");`
  * 창이름이 없으면 새창에 팝업창이 반복적으로 만들어진다.

* **팝업창 이동하기**

  * 절대좌표 사용
    * `변수명.moveTo(500,300);`
  * 상대좌표 사용
    * `변수명.moveBy(-10,-10);`

* 화면의 가운데에 팝업창이 뜨게 하기

  * ```
    var x = screen.width/2 - win.outerWidth/2;
    var y = screen.height/2 - win.outerHeight/2;
    		
    win.moveTo(x, y);
    ```

* **팝업창 크기 변경**

  * 절대크기
    * `변수명.resizeTo(800,400);`
  * 상대크기
    * `변수명.resizeBy(10,10);` 

* **window의 좌표 구하기**

  * x좌표 : window.screenX , y좌표 : window.screenY
  * 테두리와 제목을 포함한 폭과 높이 : window.outerWidth, window.outerHeight
  * 테두리와 제목을 제외한 폭과 높이(컨텐츠 영역) : window.innerWidth, window.innerHeight
  * screen의 폭과 높이 : screen.width, screen.height

#### setInterval

* 설정한 시간 간격으로 함수가 호출된다. (함수 반복 시행) 
* **setInterval("호출할 함수명", 밀리초);**
* **clearInterval(변수이름)** : interval 중지
  * 참고: 이벤트 --> onmouseover : 마우스 커서가 올라갔을때 , onmouseout : 커서가 나갔을때