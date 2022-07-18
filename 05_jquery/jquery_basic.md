## 목차

1. [JQuery란?](#JQuery란?)
2. [JQuery 사용하기](#JQuery-사용하기)
   1. [선택자](#선택자)
   2. [객체](#객체)
   3. [이벤트](#이벤트)
   4. [efftect](#effect)
   5. [JQuery/JS/CSS](#JQuery/JS/CSS)

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
* **속성 선택자**
  * 속성 선택 : $('태그명[속성]')
  * 속성값 선택 : $('태그명[속성="속성값"]')
  * 속성이 특정값으로 시작 : $('태그명[속성^="속성값 일부"]')
  * 속성이 특정값으로 끝남 : $('태그명[속성$="속성값 일부"]')
  * 속성이 특정값을 포함함 : $('태그명[속성*="속성값 일부"]')
* **상태 선택자**
  * :text : 속성값이 text인 객체를 선택
  * :checked : 속성이 checked가 설정되어 있으면 선택
  * :selected : 속성이 selected가 설정되어 있으면 선택
* **컨텐츠 선택자**
  * :contains() : 특정한 문자가 포함되어 있으면 선택
  * :has() : 특정태그가 포함되는 경우 선택
  * :not() : 특정선택자를 제외한 나머지를 선택
  * .closest() : 조상선택자 선택
  * .filter() : 특정 속성 선택
  * .contents() : 특정태그의 하위태그를 선택

### 객체

* .html() : 특정객체에 html태그를 추가, 기존의 내용 초기화 후 새로운 값 셋팅 (js에서 innerHTML의 기능)
  * html()의 ()안이 공백일때는 값을 가져옴
* .text() : 특정객체에 문자를 추가 (태그가 포함되어 있어도 모두 문자로 적용됨)
  * ()안이 공백이면 값을 얻어옴
* .removeAttr() : 객체의 속성을 제거
* 클래스 handler : css의 클래스 조작하는 방법
  * addClass() : 클래스 추가
  * removeClass() : 클래스 삭제
  * toggleClass() : 클래스가 있으면 지우고 없으면 추가
  * hasClass() : 클래스가 존재하는지 유무 확인 (true, false)
  * val() : 폼의 value를 구하거나 셋팅
  * html(), text(), attr(), prop()
* before(), insertBefore() : 선택자 이전에 객체를 추가
* after(), insertAfter() : 선택자 다음에 객체를 추가
* append(), appendTo() : 선택자의 내용 중 제일 마지막에 객체를 추가 (본래 내용 유지)
* prepend() , prependTo() : 선택한 요소 내의 제일 처음에 객체를 추가
* clone() : 요소 복사하기 -> 사용은 한번만 가능
* empty() : 선택자의 내용 지우기
* remove() : 선택자와 내용 모두 지우기
* replaceAll(), replaceWith() : 선택자를 다른 객체로 치환
* wrap() : 선택자를 특정 태그로 각각 감싼다
* wrapAll() : 선택자를 태그로 한번에 감싼다
* wrapInner() : 선택자의 안쪽을 특정태그로 묶음
* unwrap() : 선택자의 부모태그 지움
* each()  : 여러개의 객체를 순차적으로 적용(반복처리)
  * $("선택자").each(function(idx,obj){실행문})
* map() : 배열을 이용한 반복실행
  * 배열명.map(function(data, index){실행문})

### 이벤트

* **이벤트 처리 방법 1 : $(선택자).이벤트**

  * ```
    //h1에서 onclick 이벤트 발생하면
    $("h1").click(function(){
    	//이벤트 발생시 실행되는 코드
    })
    ```

  * **this** : 이벤트가 발생한 객체

* **이벤트 처리 방법 2 : $(선택자).on(이벤트종류, 실행할 함수)**

  * ```
    $("h1").on('click',function(){
    	$(this).css("color","red");
    });
    ```

* **이벤트 처리 방법 3 : $(선택자).on( {이벤트:실행함수, 이벤트:실행함수,...} )**

  * ```
    $("h1").on({mouseenter:function(){//마우스오버일때
    	$(this).css("color","blue");	
    }, mouseleave:function(){//마우스아웃일때
    	$(this).css("color","green");	
    }})
    ```

* **이벤트 처리 방법 4 : $(선택자).on('이벤트1 이벤트2', 실행함수)**

  * 1개의 요소에 2개 이상의 이벤트를 한번에 작성하기

  * ```
    $("input").on('click focus',function(){
    	$(this).css("background","yellow");
    });
    ```

* **이벤트 처리 방법 5 : $(document).on(이벤트종류, 이벤트대상, 실행함수)**

  * 실행이 끝난 후 추가된 부분에 대한 이벤트 처리하기

  * ```
    $(document).on('click','h1',function(){
    	$(this).css("background","cyan");
    })
    ```

* **이벤트 처리 방법 6 : document.getElementById("아이디").addEventListener(이벤트, 실행함수)**

  * ```
    document.getElementById("i").addEventListener('click',function(){
    	$(this).css("color","orange");
    });
    ```

---

* **hover() 이벤트** 

  * 하나의 이벤트에 두개의 기능 실행하기

  * ```
    $('h1').hover(function(){//마우스오버시
    	$(this).addClass('s1');
    },function(){//마우스아웃시
    	$(this).removeClass('s1');
    });
    ```

* **one()**

  * 이벤트 1번씩만 발생

  * ```
    $("h2").one('click',function(){
    	$(this).addClass('s2');
    })
    ```

* **key 이벤트**

  * keyup, keydown, keypress, keyrelease

  * ```
    $(선택자).keyup(function(){
    	var cnt = 100 - $(선택자).val().length;
    	$("#cnt").text(cnt+'');	
    })
    ```

* **trigger()**

  * 이벤트 강제로 발생시키기

  * ```
    setInterval(function(){
    	$(선택자).trigger('click');
    }, 1000)
    ```

### effect

* **hide() : 폭, 높이 점점 흐리게 숨기기**

  * hide(사라지는 속도[slow,fast,normal,밀리초], 콜백함수)

* **show(속도) : 숨겨진걸 보여주기**

* **toggle(속도) : 숨기고 보여주기 반복 실행**

* **fadeOut(속도) : 점점 흐리게 숨기기**

* **fadeIn(속도) : 점점 진하게 나타남**

* **fadeToggle(속도) : 흐리게와 진하게 반복 실행**

* **slideUp(속도) : 높이 줄어들면서 숨기기**

* **slideDown(속도) : 높이 늘어나면서 나타남**

* **slideToggle(속도) : 높이 줄어듦과 나타남 반복 실행**

* **animate() : 객체를 이동시키기**

  * animate({JSon형식으로 속성 설정}, 속도)
  * 속성 : marginLeft, width, marginTop, opacity, marginRight  ....
  * delay(시간) : 출발을 지연시킴
  * $(this).stop() : animate 중지시키기

* **easing : 움직이는 모양**

  * http://jqueryui.com/easing/ 에서 easing 종류 확인 가능

  * easeOutBounce, easeInBounce, easeOutBack .....

  * ```
    $("img:first").animate({marginLeft:"1200px"},6000,"easeOutBounce");
    ```



## JQuery/JS/CSS

### ckeditor

* 글 작성 시 사용할 수 있는 editor

* textarea에 작성한 문자를 html코드로 변환하여 인식

* https://ckeditor.com/ckeditor-4/download/에서 다운로드

* getData() : ckeditor로 셋팅된 textarea의 값을 가져오는 함수

  * ```
    CKEDITOR.instances.content.getData()
    ```

### Innerfade

* http://gist.github.com/coolniikou/665255 에서 다운로드
* 속성 : {animationtype : 'slide, fade', speed : 'slow, fast, normal, 밀리초', timeout  : 대기시간, type : 'random, sequence, random_start' ....}

### bxslider

* https://github.com/stevenwanderski/bxslider-4 에서 다운로드
* 속성
  * mode : 'horizontal(기본값, vertical, fade'
  * slideWidth : 슬라이드 폭
  * slideHeight : 슬라이드 높이
  * speed : 속도
  * auto : true(자동시작), false(기본값)
  * randomStart : true(랜덤시작), false(기본값)
  * captions : title속성의 값을 설명으로 표시 true, false(기본)
  * infiniteLoop : true(반복여부), false
  * hideControlOnEnd : true(처음과 마지막에 좌우컨트롤 표시안함) , false(표시)
  * useCSS: true(easing 사용안함), false(사용)
  * easing : 'easing 종류'
  * onSliderLoad : function(){} -> slide가 로딩이 완료되면 호출되는 콜백함수
  * onSlideAfter: function(){} -> slide가 움직인 후 호출되는 콜백함수

### accordion

* http://github.com/alaingoga 에서 다운로드
* 속성
  * position : 'horizontal, vertical'
  * openItem : 기본선택목록, index위치의 내용이 크게 나옴
  * openDim : 확장된 목록의 크기
  * closeDim : 닫힌 목록의 크기
  * width : 전체 폭 (horizontal에는 적용안됨)
  * height : 전체 높이 (vertical에는 적용안됨)
  * duration : 전환 속도
  * effect : easing 효과
  * border 
  * color

### dialog/datepicker

* jquery-ui를 통해 사용
* dialog : 다이얼로그 창
  * $(선택자).dialog('open') : 다이얼로그 창 열기
  * autoOpen : 실행시 자동열림 true(기본), false
  * modal : 창이 떠있을때 뒷배경 사용금지(true), 사용허용(false)
* datepicker : 날짜입력박스
  * dateFormat : 'yy년 mm월 dd일' , 'yy-mm-dd'
  * numberOfMonths : 한번에 보일 월의 수



