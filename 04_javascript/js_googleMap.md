## Javascript에서 Google Map 사용하기

* https://cloud.google.com/maps-platform/ 에 접속하여 API 키를 발급받는다.

* js와 google map 라이브러리 연결하기

  * ```
    <script async defer src="https://maps.googleapis.com/maps/api/js?key=본인의 API Key 작성&callback=함수명"></script>
    ```

* 콜백 함수 작성하기 : googlemap이 호출하는 함수

  * ```
    function 콜백함수명(){
    	실행문 작성....
    }
    ```

  * 원하는 위치의 위도와 경도를 선언한다. (전역변수로)

  * ```
    위도, 경도 정보가 담긴 객체 생성
    var myCenter = new google.maps.LatLng(latitude, logitude);
    ```

  * ```
    표시할 맵 옵션
    var mapProperty{
    	center:myCenter, 
    	zoom:14, //0~21사이, 숫자가 클수록 확대됨
    	mapTypeId: google.maps.MapTypeId.ROADMAP
    }
    ```

    * mapTypeId 지도 종류 :  ROADMAP, HYBRID, STEELITE, TERRAIN

  * ```
    map 객체 생성
    var map = new google.maps.Map(document.getElementById("지도를 표시할 곳"), 맵옵션);
    ```

  * ```
    마커 표시하기
    var marker = new google.maps.Marker({//Json 데이터
    	position:위치객체, //마커를 표시할 위치
    	map:map객체, //마커를 표시할 지도
    	title:"마우스오버시 표시할 내용",
    	icon:"마커로 표시할 아이콘 이미지" //생략하면 기본 아이콘으로 생성
    })
    ```

  * ```
    마커 클릭하면 정보 대화상자 표시
    var infoMsg = "위도 : "+latitude+"<br>경도 : "+longtitude;
    	infoMsg += "<br><a href="링크"><img src="원하는 이미지 링크"></a>"
    var info = new google.maps.InfoWindow({
    	content:infoMsg //표시할 정보내용 
    })
    ```

  * ```
    이벤트 등록하기			이벤트 발생대상, 이벤트종류, 대화상자
    google.maps.event.addListener(marker, 'click', function(){info.open(map, marker);})
    ```

  * ```
    여러곳에 마커 표시하기(위도,경도 데이터가 배열에 들어있을때)
    반복문 작성한다...
    for(var i=0; i<lat.length; i++){
    	var mk = new google.maps.Marker({
    		position:new.google.maps.LatLng(위도배열[i], 경도배열[i]),
    		map:map객체,
    		title:"위도="+위도배열[i]+",경도="+경도배열[i]
    	})
    }
    ```

  * ```
    위치 주위로 반경 표시하기
    var myCity = new google.maps.Circle({
    	center : 위치객체,
    	radius : 반지름,
    	strokeColor : 선의 색상,
    	strokeWidth : 선의 두께,
    	strokeOpacity : 선의 투명도 (0~1)
    	fillColor : 면의 색상,
    	fillOpacity : 면의 투명도
    })
    ```

  * 지명을 이용한 지도표시를 하기위해서 Geocoder객체가 필요하다.

    * ```
      geoCode = new google.maps.Geocoder();
      
      //배열의 지명을 이용하여 마커 표시하기
      for(var i=0;i<배열.length;i++){
      	setMapPosition(주소배열[i],홈페이지배열[i],이미지배열[i])
      }
      ```

  * ```
    위치이동하는 함수 
    function setMapPosition(주소값, 홈페이지값, 이미지값){
    	geoCode.geocode({address:지도에서 찾을 위치}, function(results지도에서 찾은 정보, status검색성공여부){//status='OK'면 성공
    		if(status=='OK'){
    			//지도의 중앙위치 변경               위도,경도 객체 ->console에서 확인
    			map.setCenter(results[0].geometry.location);
    			//마커표시
    			var marker = new google.maps.Marker({
    				map:map객체, icon:'사용할 이미지',....
    			})
    		}else{
    			alert("입력한 주소가 존재하지 않습니다.")
    		}
    	})
    }
    ```

  * ```
    //지역명을 이용한 지도 검색
    function searchMap(){
    	var addr = document.getElementById("address").value;
    	if(addr==""){//검색한게 없을때
    		alert("검색할 지역 또는 건물명을 입력하세요.");
    	}else{
    		setMapPosition(addr, "홈페이지", '이미지');
    	}
    }
    ```

    

