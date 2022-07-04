## JAVA와 MySQL 연동하기

* MySQL Connector 다운로드 후, 압축해제하기(http://dev.mysql.com/downloads/connector/j/)

* connector를 build path에 추가한다.

### 데이터베이스 연동과정

1. Driver 로딩
2. DB 연결 (Connection 객체 생성)
3. PreparedStatement 객체 생성 (sql 쿼리문)
4. 쿼리 실행
5. DB 연결 해제



**Driver 로딩**

```
Class.forName("com.mysql.cj.jdbc.Driver");
```

**DB 연결**

```
String url = "jdbc:mysql://localhost:3306/DB_name"; 
Connection conn = DriverManager.getConnection(url, "user", "password"); //db연결 시점
```

**PreparedStatement 객체 생성**

```
String sql = "insert * from emp";
pstmt = conn.prepareStatement(sql)
```

**쿼리 실행** 

```
int cnt = pstmt.executeUpdate();
ResultSet rs = pstmt.executeQuery();
```

select의 경우 executeQuery()를 사용하고 이경우 ResultSet 형의 데이터가 반환된다.

insert, delete, update는 executeUpdate를 사용하고 이때 int형 데이터가 반환된다.

**DB 연결 해제**

```
if(pstmt!=null) pstmt.close();
if(conn != null) conn.close();
```

아래에서부터 DB 연결 해제



-----

* SELECT 쿼리 예제

```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class SelectTest {
	Connection conn = null;
	PreparedStatement pstmt;
	ResultSet rs = null;
	static {//생성자메소드보다 먼저 실행됨
		try {
			//1. Driver 로딩
			Class.forName("com.mysql.cj.jdbc.Driver");
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	public SelectTest() {}
	public void start() {
		try {
			//2. db연결
			conn = DriverManager.getConnection("jdbc:mysql://@localhost/multi","root","root1234");
			
			String sql = "select mem_id, username, depart, phone, email, date_format(writedate, '%Y-%m-%d') writedate "
						+ "from member order by username asc";
			// 3. Statement 생성
			pstmt = conn.prepareStatement(sql);
			
			//4. 실행
			rs = pstmt.executeQuery();
			
			while(rs.next()) {
				int mem_id = rs.getInt(1); //rs.getInt('mem_id');
				String username = rs.getString(2); //rs.getString('username');
				String depart = rs.getString(3);
				String phone = rs.getString(4);
				String email = rs.getString(5);
				String writedate = rs.getString(6);
				System.out.printf("%-8d %-10s %-10s %-20s %-20s %-20s\n", mem_id, username, depart, phone, email, writedate);
			}
			
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			try {
				if (rs!=null) rs.close();
				if (pstmt!=null) pstmt.close();
				if (conn!=null) conn.close();
			}catch(Exception e) {
				e.printStackTrace();
			}
		}
	}
```



* INSERT 쿼리 예제

```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.SQLException;
import java.util.Scanner;

public class InsertTest {
	Connection conn = null;
	Scanner scan = new Scanner(System.in);
	PreparedStatement pstmt = null;
	public InsertTest() {}
	public void start() {
		try {
			// 1. Driver 로딩 
			Class.forName("com.mysql.cj.jdbc.Driver");
			
			// 2. DB 연결          
			String url = "jdbc:mysql://@127.0.0.1/multi"; 
			conn = DriverManager.getConnection(url, "root", "root1234"); //db연결 시점
			
			// 데이터 준비
			System.out.print("회원번호->");
			int mem_id = Integer.parseInt(scan.nextLine());
			System.out.print("회원명->");
			String username = scan.nextLine();
			System.out.print("부서명->");
			String depart = scan.nextLine();
			System.out.print("연락처->");
			String phone = scan.nextLine();
			System.out.print("이메일->");
			String email = scan.nextLine();
			
			// 3. PreparedStatement 객체를 생성 (sql 쿼리문)
			String sql = "insert into member(mem_id, username, depart, phone, email)"
					+ " values(?,?,?,?,?)"; // 문장 나눠쓸때 주의점 : 앞이나 뒤에 빈칸 하나 띄워야함
			
			pstmt = conn.prepareStatement(sql);
			
			pstmt.setInt(1, mem_id); 
			pstmt.setString(2, username); 
			pstmt.setString(3, depart);
			pstmt.setString(4, phone);
			pstmt.setString(5, email);
			
			//4. 실행
			int cnt = pstmt.executeUpdate();
			if(cnt>0) {
				System.out.println("레코드가 추가되었습니다.");
			}else {
				System.out.println("레코드 추가 실패하였습니다.");
			}
			
		}catch(ClassNotFoundException cnfe) {
			System.out.println("드라이브 로딩 실패");
			cnfe.printStackTrace();
		}catch(SQLException se) {
			System.out.println("DB연결 실패");
			se.printStackTrace();
		}catch(Exception e) {
			e.printStackTrace();
		}finally {
			try {
				//5. DB연결 해제
				if(pstmt!=null) pstmt.close();
				if(conn != null) conn.close();
			}catch(Exception e) {e.printStackTrace();}
		}
		
	}
```



* 반복해서 사용되는 DB 연동 과정을 클래스로 만들기

```
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;

public class DBConn {
	//Drive 로딩
	static {
		try {
			Class.forName("com.mysql.cj.jdbc.Driver");
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	//변수 선언
	protected Connection conn; 
	protected PreparedStatement pstmt;
	protected ResultSet rs;
	protected String sql = null; 
	protected final String URL = "jdbc:mysql://@127.0.0.1/multi";
	protected final String DB_ID = "root";
	protected final String DB_PWD = "root1234";
	
	//DB 연결
	protected void getConn() {
		try {
			conn = DriverManager.getConnection(URL, DB_ID, DB_PWD);
		}catch(Exception e) {
			e.printStackTrace();
		}
	}
	
	//DB 닫기
	protected void getClose() {
		try {
			if(rs != null) rs.close(); // 객체가 있는지 확인
			if(pstmt != null) pstmt.close();
			if(conn != null) conn.close();
		}catch(Exception e) {
			e.printStackTrace();
		}
	}

}
```



