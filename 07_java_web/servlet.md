## Servlet이란?

* 서블릿(Servlet)이란 동적 웹 페이지를 만들 때 사용되는 자바 기반의 웹 애플리케이션 프로그래밍 기술이다. 서블릿은 웹 요청과 응답의 흐름을 간단한 메서드 호출만으로체계적으로 다룰 수 있게 해준다. 서버에서 실행되다가 웹 브라우저에서 요청을 하면 해당 기능을 수행한 후 웹브라우저에 결과를 전송한다. (참고 : https://velog.io/@falling_star3/Tomcat-%EC%84%9C%EB%B8%94%EB%A6%BFServlet%EC%9D%B4%EB%9E%80)

* 사용방법

  * tomcat의 web.xml을 webapp/WEB_INF에 붙여넣기
  * web.xml을 열어 `<servlet>, <sevlet-mapping> `태그를 추가한다.

  ```
  <servlet>
  	<servlet-name>home</servlet-name>
  	<servlet-class>패키지명.서블릿파일명</servlet-class>
  	<init-param>
  		<param-name>userid</param-name>
  		<param-value>gildong</param-value>
  	</init-param>
  </servlet>
  <servlet-mapping>
  	<servlet-name>home</servlet-name>
  	<url-pattern>/main.do</url-pattern>
  </servlet-mapping>
  ```

  * main.do 페이지에 접속하면 home으로 실행이 옮겨간다.

  * ```
    //서블릿 파일코드
    
    public class ServletTest extends HttpServlet {
    	private static final long serialVersionUID = 1L;
           
        public ServletTest() {
            super();
        }
    
    	protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException {
    		System.out.println("doGet()메소드 실행됨");
    		
    		//web.xml의 값을 Servlet클래스로 가져오기
    		
    		String userid = getInitParameter("userid");
    		System.out.println("userid->"+userid);
    		
    		//client컴퓨터에 html 데이터 보내기
    		res.setContentType("text/html; charset=UTF-8");
    		
    		PrintWriter pw = res.getWriter();
    		
    		pw.print("<html>");
    		pw.print("<head>");
    		pw.print("<title>로그인 폼</title></head><body>");
    		pw.print("<h1>로그인</h1><form method='post' action=''/>");
    		pw.print("아이디 : <input type='text' name='userid'/><br>");
    		pw.print("비밀번호 : <input type='password' name='userpwd'/><br>");
    		pw.print("<input type='submit' value='Login'/></form></body></html>");
    		pw.close();
    	}
    
    	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    		System.out.println("doPost()메소드 실행됨...");
    	}
    
    }
    ```

  * getInitParameter() : 데이터 가져오기

  * response.setContentType() : 보낼 데이터 정보

  * response.getWriter() : 데이터 보낼(작성) 기능이 있는 메소드?

* servlet에 db연결하기

  * 