조남호 | Nathan Cho<br>
수업 일수 --.--.23 ~ ---

# JSP
***
## 웹과 서버
- 웹

        페이지 요청과 응답이 일어나는 장소.
- 서버

        사용자의 요청에 맞는 서비스를 제공해주는 것

        - 요청(request)   : 클라이언트 ===> 서버
        - 응답(response)   : 서버 ===> 클라이언트
- 웹 서버(http), Apache(아파치)

        사용자의 요청이 정적 데이터인지 동적 데이터인지 판단한다.
        정적 데이터일 경우 이미 준비된 HTML문서를 그대로 응답해주며,
        동적 데이터라면 웹 컨테이너에 요청을 보낸다.
- 웹 컨테이너(서블릿 컨테이너)

        동적 데이터일 경우 JSP, 서블릿으로 연산 및 제어 그리고 DB까지 접근한다.
        DB에 접근하는 연산을 복잡한 연산이라고 하며, JAVA로 처리한다.
        동적 데이터가 정제된 데이터(정적 데이터)로 완성되면 이를 웹 서버로 전달해준다.
- WAS(Web Application Server) - Tomcat

        동적 데이터를 처리할 서블릿을 메모리에 할당하며, 
        web.xml을 참조한 뒤 알맞는 서블릿에 대한 Thread를 생성한다.
        서블릿 요청과 서블릿 응답 객체 생성 후 서블릿에 전달하면, 
        연산 종료 후 메모리에서 해제시킨다.
- 서블릿(Servlet)

        Java 코드 안에 HTML 코드를 작성할 수 있는 Java 프로그램이다.
        Thread에 의해 서블릿에 있는 service() 메소드가 호출된다.
        전송 방식 요청에 맞게 doGet() 또는 doPost()등의 메소드를 호출한다.

***
## EL과 JSTL
    자바 구문을 라이브러리 형태로 만들어 놓고 필요할 때마다 태그로 꺼내쓰는 기술이다.
    JSP 페이지 내에서 자바 코드와 HTML 코드가 섞여 있으면 가독성이 떨어지고 복잡해진다.
    EL문과 JSTL문을 사용하면 HTML 태그로만 구성된 일관된 소스코드를 볼 수 있다는 장점이 있다.
    
### EL
    값을 간결하고 간편하게 출력할 수 있도록 해주는 기술
    
    자바                    EL
    <%=name%>               ${name}
    <%=member.getName()%>   ${member.name}
    
    값을 찾을 때에는 작은 Scope에서 큰 Scope로 찾는다.
    page > request > session > application
    
    ${param.name} : 전달받은 데이터 중 쿼리스트링으로 작성된 데이터에서 name을 찾는다.
    ${requestScope.name} : request 객체에 담긴 데이터 중 name을 찾는다.
    ${sessionScope.name} : session 객체에 담긴 데이터 중 name을 찾는다.

### EL 문법
    %, mod
    &&, and
    ||, or
    >, lt
    <, gt
    >=, le
    <=, ge
    ==, eq
    !=, ne
    !, not
    empty: 값 비어있으면 true, 아니면 false

### JSTL(JSP Standard Tag Libarary)
    연산자나 조건문, 반복문 등을 편하게 처리할 수 있으며, SJP 페이지 내에서 자바코드를 사용하지 않고
    로직을 구현할 수 있도록 효율적인 방법을 제공한다.
    
    자바                                  JSTL
     
    <%for(초기식; 조건식; 증감식){}%>      <c:forEach var="" begin="" end=""></c:forEach>
    <%for(자료형 변수명 : 반복자){}%>      <c:forEach var="" items="${반복자}"></c:forEach>

### Core 태그의 종류
    <c:set>      : 변수 선언
    <c:out>      : 변수 출력(사용)
    <c:if>      : if문
    <c:choose>   : else if문 시작
    <c:when>   : else if문
    <c:otherwise>   : else문
    <c:forEach>   : for문

***
## JSP
### JSP란?
    JAVA Server Page, HTML을 중심으로 자바와 같이 연동하여 사용하는 웹 언어이다.
    HTML코드 안에 JAVA코드를 작성할 수 있는 언어이다.

    각 페이지마다 필요 시 자바 코드가 작성되며, DB와 연결하는 코드도 jsp파일 안에서
    모두 작성된다. 분리되어 있지 않기 때문에 규모가 작은 프로젝트에 어울리는 방식이며,
    코드가 확장될 수록 가독성이 떨어지고 분업과 유지보수가 좋지 않다.

***
## MVC 패턴
1. Model 1

        a.jsp --> b.jsp --> c.jsp
                     ↓
                 DAO.java

        b.jsp에서 dao를 호출함으로써 자바코드가 섞이게 된다. 선언은 JAVA 페이지에 구현이 되어 있기 때문에
        jsp 내의 JAVA 코드 양이 줄어들지만 결국 사용은 jsp 페이지에서 하기 때문에
        Controller(DAO 메소드를 사용하고 어디 페이지로 이동할 지)와 View가 섞이게 된다.
        페이지가 확장될 수록 유지보수가 좋지 않다. 하지만 설계는 쉽다.
2. Model 2
