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

* JSP 내장 객체 : request, response, session, out, application, cookie

  * ```
    out.print(변수); -> client가 봐야하는 결과 output하기
    
    //하나의 값을 output할때 out.print()대신 HTML영역에 =변수명을 사용가능하다
    a=<%=a %>
    name=<%=name %>
    ```

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
    	//request : 클라이언트측의 데이터를 서버로 가져오기
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
    	아이디: <input type="text" name="userid"><br>
    	비밀번호 : <input type="password" name="userpwd"><br>
    	이름 : <input type="text" name="username"><br>
    	<input type="submit" value="전송">
    </form>
    ```

  * ```
    //서버 페이지(formOK.jsp)
    
    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
    <%
    	//post방식의 전송일때 request객체에 인코딩해준다.
    	request.setCharacterEncoding("UTF-8");
    	
    	String userid = request.getParameter("userid"); //form의 name과 같아야함
    	String userpwd = request.getParameter("userpwd");
    	String username = request.getParameter("username");
    %>
    --------html영역--------
    <!-- 가져온 데이터 다시 보내기 -->
    아이디 : <%=userid %><br>
    비밀번호 : <%=userpwd %><br>
    이름 : <%=username %><br>
    ```



