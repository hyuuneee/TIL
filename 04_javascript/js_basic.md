## 목차

1. [Javascript](#Javascript)
   1. [기본 용어](#기본-용어)
   2. [변수](#변수)
   3. [함수](#함수)
   4. [JS 사용하기](#JS-사용하기)

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

#### JS 사용하기

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

  