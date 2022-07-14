## 목차

1. [JQuery란?](#JQuery란?)
2. [JQuery 사용하기](#JQuery-사용하기)
   1. [선택자](#선택자)

## JQuery란?

* 제이쿼리는 웹사이트에 자바스크립트를 쉽게 활용할 수 있도록 도와주는 오픈소스, 이벤트 기반의 자바스크립트 라이브러리이다.
* JQuery의 특징
  * 웹페이지 상에서 엘리먼트(Element)를 쉽게 찾고 조작할 수 있다.
  * 거의 모든 웹브라우저에 대응할 정도로 호환성이 매우 뛰어나다.
  *  네트워크, 애니메이션 등 다양한 기능을 제공한다.
  *  메소드 체이닝(Method chaining) 등 짧고 유지관리가 용이한 코드 작성을 지원한다.
  *  관련 플러그인들이 웹상에 공개되어 있으며 플러그인을 직접 구현하거나 확장할 수 있다.
  *  공식 웹사이트(www.jquery.com)와 수많은 레퍼런스를 통해 쉽게 접근 가능하다.

## JQuery 사용하기

* JQuery는 라이브러리를 다운로드하여 외부 자바스크립트 파일로 추가하거나 cdn방식으로 링크를 걸어서 사용할 수 있다.

* cdn방식으로 사용하기 : www.jquery.com -> 다운로드 클릭 -> cdn링크로 이동 -> 첫번째 링크 복사하여 사용

* ```
  <script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.6.0/jquery.min.js"></script> //jquery링크를 추가한 코드
  ```

* **Jquery 실행하기**

  * ```
    $(document).ready(function(){
    	실행문;
    })
    ```

  * ```
    JQuery(document).ready(function(){
    	실행문;
    })
    ```

  * ```
    $(function(){
    	실행문;
    })
    ```

* **JQuery에서 CSS 사용하기**

  * ```
    CSS 사용하기
    $("body").css("background-color","#ddd");
    $(".c1").css("border","1px solid red");
    $("#t1").css("background-color","lightblue");
    ```

* **JQuery에서 HTML 사용하기**

  * 속성=속성값이 존재하는 속성 : attr 사용

    * ```
      $("img").attr("src","../img/03.jfif");
      $("#txt").attr("value","홍길동");
      ```

  * 속성만 존재하는 속성 : prop 사용

    * ```
      readonly, checked, selected, disabled, controls ..
      $("#txt").prop("readonly",true); // true(적용)/false(해제)
      ```

### 선택자

* **태그 선택자** : $("태그")
* **클래스 선택자** : $(".클래스")
* **아이디 선택자** : $("#아이디")
* **자손 선택자** : $('a>b')
* **후손 선택자** : $('a b')
* **인접 선택자**
  * children() : 자손 객체를 선택
  * parent() : 부모 객체를 선택
  * siblings() : 형제 객체를 선택
  * next() : 선택자의 다음 객체를 선택
  * prev() : 선택자의 이전 객체를 선택
* **위치 선택자**
  * first : 첫번째 객체 선택
  * last : 마지막 객체 선택
  * even : 짝수번째 객체 모두 선택(객체 순서 0부터 시작)
  * odd : 홀수번째 객체 모두 선택(객체 0부터 시작)
  * nth-last-of-type(n) : 뒤에서 n번째 객체 선택
  * nth-child(3n) : 3의 배수번째 객체 모두 선택 (객체 1부터 시작)
  * only-child : 부모 중 자식이 1개인 부모를 선택
  * index를 이용한 선택자
    * slice(n) : index n부터 끝까지 선택
    * eq(n) : index n인 객체 선택
    * lt(n) : less than, index n보다 작은 객체 모두 선택
    * gt(n) : greater than, index n보다 큰 객체 모두 선택