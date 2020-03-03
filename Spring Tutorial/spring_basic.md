# Spring Tutorial

- Project: https://github.com/spring-projects/spring-petclinic
- 프로젝트 빌드: ./mvnw package

mvnw(maven wrapper): Apache Maven을 프로젝트에서 요구하는 버전으로 유지하기 위해 사용하는 도구(Maven 설치 없이 빌드 가능)
.mvn/wrapper/maven-wrapper.properties 파일의 distributionUrl 속성에 Maven 버전 정의
- 프로젝트 실행: java -jar target/*.jar

jar(JAVA Archive): 복수개의 자바 클래스 파일, 리소스, 메타데이터를 하나의 파일로 모아 배포하기 위한 소프트웨어 패키지 포맷
- Apache Tomcat

  * Apache: 클라이언트 요청이 왔을때만 응답하는 정적 웹 서버/ 정적 데이터(HTML, CSS, 이미지 등)만 처리/80 포트

  * Tomcat: 동적 웹페이지를 만들기 위한 웹(서블릿) 컨테이너/8080 포트

  * Apache Tomcat: Apache는 정적인 데이터만 처리, JSP 처리는 웹 컨테이너로 넘겨주어 분산처리, WAS(Web Application Server)
  
- [ERROR] The port may already be in use or the connector may be misconfigured.
  
  [SOLUTION] netstat -ano | findstr \<Port Number\>
 
               taskkill /F /PID <Process Id>
