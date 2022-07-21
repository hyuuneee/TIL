## 목차

1. [JSP란?](#JSP란?)
2. [JSP 기초](#JSP-기초)

## JSP란?

* JSP란 JavaServer Pages의 약자이며 HTML코드에 JAVA코드를 넣어 동적웹페이지를 생성하는 웹어플리케이션 도구이다. JSP가 실행되면 자바 서블릿(Servlet)으로 변환되며 웹 어플리케이션 서버에서 동작되면서 필요한 기능을 수행하고 생성된 데이터를 웹페이지와 함께 클라이언트로 응답한다.

* JSP 기본구조

  * ```
    <!-- 지시부 -->
    <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
    <%! //선언부
    	//메소드나 변수를 선언하는 영역
    %>
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style></style>
    <script></script>
    </head>
    <body>
    <div>
    	<%
    		//스크립트 릿 : 명령어 입력하는 곳
    		
    	%>
    </div>
    </body>
    </html>
    ```

## JSP 기초

* **JSP 내장 객체** : request, response, session, out, application, cookie

  * ```
    out.print(변수); -> client가 봐야하는 결과 output하기
    
    //하나의 값을 output할때 out.print()대신 HTML영역에 =변수명을 사용가능하다
    a=<%=a %>
    name=<%=name %>
    ```

### request

* request : 클라이언트측의 데이터를 서버로 가져오는 객체

* aLink를 이용하여 서버로 데이터 보내기

  * a태그는 GET방식으로 데이터가 전송된다.

  * ```
    //html 페이지
    
    <a href="aLinkOk.jsp?num=125&username=홍길동&tel=010-2345-3443">a 태그로 데이터 전송하기</a>
    ```

  * ```
    //서버 페이지(aLinkOk.jsp)
    
    <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
    <%
    	//request : 클라이언트측의 데이터를 서버로 가져오기, 단 이전 페이지에 있는 데이터만 가져올 수 있다.
    	int num = Integer.parseInt(request.getParameter("num"));
    	String username = request.getParameter("username");
    	String tel = request.getParameter("tel");
    	
    %>
    ---------html영역------------
    <!-- 가져온 데이터 다시 보내기 -->
    번호 : <%=num%><br>
    이름 : <%=username%><br>
    연락처 : <%=tel%>
    ```

* form을 이용하여 서버로 데이터 보내기

  * ```
    //html 페이지
    
    <form method="post" action="formOk.jsp">
    <!-- readonly:서버로 데이터 보내기 가능, disabled : 서버로 데이터 보내기 불가 -->
    	아이디: <input type="text" name="userid" value="gildong" disabled><br>
    	비밀번호 : <input type="password" name="userpwd"><br>
    	이름 : <input type="text" name="username"><br>
    	동의여부 : <input type="radio" name="state" value="Ok">동의함
    			<input type="radio" name="state" value="No">동의안함<br>
    	취미 : <input type="checkbox" name="hobby" value="농구">농구
    		  <input type="checkbox" name="hobby" value="축구">축구
    		  <input type="checkbox" name="hobby" value="야구">야구
    		  <input type="checkbox" name="hobby" value="배구">배구
    		  <input type="checkbox" name="hobby" value="탁구">탁구<br>
    	<input type="hidden" name="num" value="1234">  <!-- hidden : 화면상에는 안보이는 데이터 -->	  
    	<input type="submit" value="전송">
    </form>
    ```
    
  * ```
    //서버 페이지(formOK.jsp)
    
    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
    <%
    	//post방식의 전송일때 request객체에 인코딩해준다
    	out.print(request.getCharacterEncoding()+"<br>"); //인코딩 셋팅 전에는 null
    	request.setCharacterEncoding("UTF-8");
    	
    	String userid = request.getParameter("userid"); //form의 name과 같아야함
    	String userpwd = request.getParameter("userpwd");
    	String username = request.getParameter("username");
    	String state = request.getParameter("state");
    	//하나의 변수에 값이 여러개일때
    	String[] hobby = request.getParameterValues("hobby");
    %>
    --------html영역--------
    <!-- 가져온 데이터 다시 보내기 -->
    아이디 : <%=userid %><br>
    비밀번호 : <%=userpwd %><br>
    이름 : <%=username %><br>
    동의여부 : <%=state %><br>
    취미 : <%=Arrays.toString(hobby) %><br>
    ```

* request 객체의 메소드
  * form의 name 구하기 : `Enumeration<String> nameList = request.getParameterNames();`
  * 접속자의 컴퓨터 IP : `request.getRemoteAddr()`
  * 인코딩 코드값 : `request.getCharacterEncoding()`
  * contentType : `request.getContentType()`
  * 전송방식 : `request.getMethod()`
  * protocol : `request.getProtocol()`
  * URI : `request.getRequestURI()` ->경로와 파일명
  * ContextPath : `request.getContextPath()`
  * 서버이름 : `request.getServerName()` -> 도메인
  * 포트 : `request.getServerPort()`
  * 절대주소 : `request.getServletContext().getRealPath("/")` -> 파일의 물리적 주소

### response

* 다른 페이지로 이동하는 객체

* ```
  //클라이언트 페이지(login.jsp)
  
  ---html영역----------
  <h1>로그인</h1>
  <form method="post" action="loginOk.jsp">
  	아이디 : <input type="text" name="userid" id="userid"><br>
  	비밀번호 : <input type="password" name="userpwd" id="userpwd"><br>
  	<input type="submit" value="로그인">
  </form>
  ```

* ```
  //서버 페이지(loginOk.jsp)
  
  <%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
  <%
  	String userid = request.getParameter("userid");
  	String userpwd = request.getParameter("userpwd");
  	
  	if(userid.equals("gildong")&& userpwd.equals("1234")){//로그인 성공
  		//다른 페이지로 이동
  		response.sendRedirect(request.getContextPath()+"/index.jsp");
  	}else{//로그인실패
  		//response.sendRedirect("/webJSP/jsp02_response/login.jsp");
  	%>
  	<script>
  		history.back();//js의 history객체 : 로그인페이지로 돌아가기 
  		// history.back():이전페이지로이동/history.forward():다음페이지로/history.go(-1):전페이지로
  	</script> 
  	<%
  	}
  %>
  ```

### cookie

* 쿠키 : 클라이언의 컴퓨터에 저장된 데이터

* ```
  <%
  	//클라이언트 컴퓨터의 쿠키 정보를 서버로 가져오기
  	Cookie[] coo = request.getCookies();
  	
  	for(int idx=0;idx<coo.length;idx++){
  %>		
  		<li><%=coo[idx].getName() %> : <%=coo[idx].getValue() %></li>
  <%	}%>
  ```

* ```
  //jsp에서 쿠키 저장하기
  //Cookie클래스를 객체로 만들어 response를 이용하여 클라이언트 컴퓨터에 정보를 보내기
  Cookie cookie = new Cookie("변수","값");
  //소멸시점설정
  cookie.setMaxAge(정수); //초단위
  //클라이언트에게 전송
  response.addCookie(cookie);
  
  <script>
  	//js에서 쿠키 저장하기
  	document.cookie="변수=값";
  </script>
  ```

### session

* session은 cookie와 달리 서버에 저장되며, 모든 페이지에서 접근 가능함.

* ```
  <%
  	session.setAttribute("logId", "gildong");
  	session.setAttribute("logStatus", "Y");
  	session.setAttribute("logName", "홍길동");
  %>
  ```

* ```
  //로그아웃시 세션에 있는 모든 기록을 제거하고 홈페이지로 이동하기
  //세션객체를 삭제하면 기록이 제거되고 새로운 세션이 할당됨
  
  session.invalidate();
  response.sendRedirect("홈페이지파일");
  ```

* ```
  //홈페이지 파일(index.jsp)
  
  <% if(session.getAttribute("logStatus")!=null && session.getAttribute("logStatus").equals("Y")){//로그인된 경우 %>
  	<%=session.getAttribute("logName") %><a href="/webJSP/jsp04_session/sessionLogout.jsp">로그아웃</a>
  <% }else{//로그인 안된경우 %>
  	<a href="<%=request.getContextPath()%>/jsp02_response/login.jsp">로그인</a>
  <% } %>
  ```

### error

* ```
  //클라이언트 페이지(에러가 발생할 페이지)
  
  <!-- 지시부에 작성 -->
  <%@ page errorPage="errorPage.jsp" %>
  ```

* ```
  //에러 발생하면 실행될 페이지
  
  <!-- 지시부에 작성 -->
  <%@ page isErrorPage="true" %>
  
  ------html영역-------
  에러메세지 : 
  <%
  	out.print(exception.getMessage());
  %>
  <a href="/webJSP/index.jsp"><img src="../img/oops.png"></a>
  ```

### include

* 페이지에서 header, footer, 배너등과 같이 항상 같은 내용이 표시되는 부분은 매번 같은 내용을 작성하기보다 `<jsp:include>`를 이용하여 다른 jsp파일이나 html파일을 가져와 그 페이지에 그대로 적용할 수 있다.

* jsp 파일 붙여넣기 : jsp의 include는 변수를 호환하지 않는다.

  * ```
    //상단바(top.jsp)
    
    <%
    	String name ="세종대왕";
    %>
    <!-- main과 중복되는 소스들 제거하기  
    <style>
    	#top{height:50px; background:pink}
    </style> 
    main의 css에 작성가능-->
    
    <div id="top">
    	<%=name %>
    </div>
    ```

  * ```
    //하단바(bottom.jsp)
    
    <%
    	int num = 1234;
    %>
    <!--  
    <style>
    	#bottom{height:50px; background:#ddd}
    </style>
    -->
    <div id="bottom">
    	<%=num %>
    </div>
    ```

  * ```
    //메인페이지
    
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style>
    	.container{
    		width:80%; margin:0 auto;
    	}
    	.container>img{width:100%;}
    	#top{height:50px; background:pink}
    	#bottom{height:50px; background:#ddd}
    </style>
    </head>
    <body>
    <!-- top.jsp include -->
    <jsp:include page="top.jsp"></jsp:include>
    <div class="container">
    	<img src="../img/06.jpg">
    	<%
    		//jsp의 include는 변수를 호환하지 않는다.
    		//out.print(name); //사용불가
    	%>
    </div>
    <!-- bottom.jsp include -->
    <jsp:include page="bottom.jsp"></jsp:include>
    </body>
    </html>
    ```

* jspf 파일 붙여넣기 : include한 파일의 변수 사용 가능하다.

  * ```
    //상단바(header.jspf)
    
    <%
    	String username = "홍길동";
    %>
    <!-- 중복코드 삭제 -->
    <div id="header">
    <%=username %>
    </div>
    ```

  * ```
    //하단바(footer.jspf)
    
    <!-- 중복코드 삭제-->
    <div id="footer">
    	<%=username %>
    </div>
    ```

  * ```
    //메인페이지
    
    <!DOCTYPE html>
    <html>
    <head>
    <meta charset="UTF-8">
    <title>Insert title here</title>
    <style>
    	#main{
    		width:80%;
    		margin:0 auto;
    	}
    	#main>img{
    		width:100%;
    	}
    	#header{height:50px; background:lightblue}
    	#footer{height:50px; background:orange}
    </style>
    </head>
    <body>
    <%@ include file="header.jspf" %>
    <div id="main">
    	<%=username %><br>
    	<img src="../img/07.jpg">
    </div>
    <%@ include file="footer.jspf" %>
    </body>
    </html>
    ```

### JSTL (JSP Standard Tag Library)

* 사용법 : JSTL은 라이브러리이기 때문에 지시부에 추가해줘야 한다.

  * ```
    <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>  
    ```

  * core 태그 라이브러리를 사용하는 선언문이다. (prefix="c")

* **set, remove 태그** : 변수의 선언 및 삭제

  * ```
    //변수 선언하기
    
    <%
     int a = 123;
    %>
    
    <c:set var="num" value="<%=a%>"/>
    <c:set var="no" value="${456}"/>
    <c:set var="name">홍길동</c:set>
    
    //변수 사용하기
    num = ${num}
    no = ${no}
    name = ${name}
    
    //데이터 request하기 : param.변수
    <c:set var="name" value="${param.name}"/>
    ```

  * ```
    //변수 삭제하기
    
    <c:remove var="no"/>
    ```

* **if 태그** : 조건문 사용하기

  * ```
    <c:set var="x" value="${10}"/>
    <c:set var="y" value="${5}"/>
    
    <c:if test="${x>y}">
    	조건문이 참일때 실행된다....
    </c:if>
    ```

* **forEach 태그** : 반복문 사용하기

  * ```
    //숫자를 이용한 반복문
    //					시작      종료     증가(생략시 1씩 증가)
    <c:forEach var="n" begin="2" end="9" step="2">
    	%{n}
    </c:forEach>
    
    //배열을 이용한 반복문
    <%
    	int arr[] = {23,43,5,65}
    %>
    <c:forEach var="date" items="<%=arr%>">
    	[${data}]
    </c:forEach>
    
    //컬렉션 : ArrayList를 이용한 반복문
    <%
    	List<String> lst = new ArrayList<String>();
    	lst.add("홍길동");
    	lst.add("유재석");
    	lst.add("김연아");
    %>
    <c:forEach var="name" items="<%=lst%>">
    	[${name}]
    </c:forEach>
    
    //Map을 이용한 반복문
    <%
    	HashMap<String,String> hm = new HashMap<String,String>();
    	hm.put("name", "홍길동");
    	hm.put("addr", "서울시 영등포구");
    	hm.put("tel", "010-2334-2543");
    %>
    <c:forEach var="mapData" items="<%=hm%>">
    	key : ${mapData.key}, value : ${mapData.value}
    </c:forEach>
    ```

* **forTokens 태그** : 문자열을 특정문자로 조각내기

  * ```
    <c:forTokens var="t" items="빨강색,파랑색,,노랑색.보라색.오렌지색-갈색" delims=",.-">
    	[${t}]
    </c:forTokens>
    ```

* **url 태그** : url주소를 가지는 태그

  * ```
    <c:url var="home" value="/index.jsp"/>
    <c:url var="login" value="/jsp_response/login.jsp">
    	//데이터 보내기
    	<c:param name="userid" value="gildong"></c:param>
    </c:url>	
    
    //url 사용하기
    <a href="${home}">홈</a>
    <a href="${login}">로그인</a>
    ```

* **choose 태그** : switch문, if문과 비슷하게 사용

  * ```
    <c:set var="name" value="${param.name}"/>
    <c:set var="age" value="${param.age}"/>
    
    <c:choose>
    	<c:when test="${name=='hong'}">
    		당신의 이름은 ${name}입니다.
    	</c:when>
    	<c:when test="%{age>20}">
    		당신은 20세 이상입니다.
    	</c:when>
    	<c:otherwise>
    		당신의 이름은 hong이 아니고 나이가 20세 이상이 아닙니다.
    	</c:otherwise>
    </c:choose>
    ```

* **redirect 태그** : 자동으로 페이지 이동하기 

  * html의 Refresh, js의 location.href, jsp의 response.sendRedirect와 같음

  * ```
    <c:redirect url="/login.jsp">
    	<c:param name="username">홍길동</c:param> //데이터보내기 가능
    </c:redirect>
    ```

  
