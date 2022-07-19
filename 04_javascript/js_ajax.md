## Ajax란?

* Ajax란 자바스크립트의 라이브러리 중 하나이며, 비동기 자바스크립트와 XML (**A**synchronous **J**avaScript **A**nd **X**ML)을 말한다. 간단히 말하면, 서버와 통신하기 위해 `XMLHttpRequest` 객체를 사용하는 것이다. AJAX의 특징은 페이지 새로고침 없이 서버에 요청하는 "비동기성"과 서버로부터 데이터를 받고 작업을 수행할 수 있다는 점이다. 

* **XMLHttpRequest** : ajax처리를 하는 자바스크립트 내장 객체

* 사용방법 (실행순서 : 1-3-4-2)

  1.  ```
      //웹서버와 통신하는 httpRequest 객체 생성
      var xHttp = new XMLHttpRequest();
      ```

  2. ```
     //서버에서 데이터가 넘어오면 전송받을 기능 구현
     xHttp.onreadystatechange = function(){
     	//서버에서 정보가 오면 이벤트에 의해 실행되는 함수
     	if(this.readyState==4 && this.status==200){//정상처리됨
     		document.getElementById("아이디").innerHTML = this.responseText;
     	}else{//전송실패
     		document.getElementById("아이디").innerHTML = "서버에서 정보를 가져오지 못하였습니다."
     	}
     }
     
     //전송결과 확인 변수
     //readyState : XMLHttpRequest의 처리 결과를 갖고 있음
     			   0:초기화실패, 1:서버연결, 2:요청접수됨, 3:처리요청, 4:요청완료됨
     //status : 요청처리 상태 번호를 반환
     		   200:정상처리, 403:금지, 404:찾을 수 없음
     //statusText : 'OK', 'Not Found'
     //responseText : 실행결과 값 -> 서버에서 전송받은 내용이 있는 변수
     ```

  3. ```
     //객체열기
     xHttp.open('전송방식GET/POST', '가져올 데이터파일명', 'true(비동기식)/false(동기식)');
     ```

  4. ```
     //객체보내기 : 실제 서버에 접속
     xHttp.send(); //서버에 정보를 요청
     ```

* jquery에서 ajax로 text 데이터 가져오기

  * ```
    //서버에서 txt파일의 내용 가져오기
    $("선택자").load('파일명');
    ```

* jquery에서 ajax로 json 데이터 가져오기

  * ```
    //서버에서 json데이터 가져오기
    $.ajax({
    	url:'접속할 파일명', //서버에 접속할 대상
    	dataType:'json',
    	success:function(result){//서버에서 정상전송 받았을때
    		$("선택자").append("<ol>")
    		$.each(result.key, function(idx, data){//반복실행
    			$("선택자>ol").append("<li>"+data.key2+" : "+data.value+"</li>")
    		})
    		$("선택자").append("</ol>")
    	},error(function(request, status, error){서버에서 전송 받지 못했을때(생략가능)
    		console.log(request.code);
    		console.log(request.reponseText);
    		consloe.log(error);
    	})
    })
    ```

* jquery에서 ajax로 xml 데이터 가져오기

  * ```
    //서버에서 xml데이터 비동기식으로 가져오기
    $.ajax({
    	url:'접속할 파일명',
    	dataType:'xml',
    	success:function(result){
    		//find('태그'):태그선택
    		if($(result).find('row').length>0){//row태그 레코드가 있으면
    			$(result).find('row').each(function(idx,row){
    				var name = $(this).find('username').text();
    				var tel = $(this).find('tel').text();
    				var addr = $(this).find('addr').text();
    				
    				var tag = "<tr><td>"+name+"</td><td>"+tel+"</td><td>"+addr+"</td><td>"
    				$("선택자").append(tag)
    			})
    		}
    	}, error:function(){
    		console.log("가져오기 실패..")
    	}
    })
    ```

