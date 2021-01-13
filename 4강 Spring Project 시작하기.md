# 4강 Spring Project 시작하기

 >STS 소개 및 제공하는 기능
 >
 >Maven과 Library 관리
 >
 >Spring Project 작성방법



### STS란?

- SpringSource가 직접 만들어 제공하는 **이클립스의 확장판**
- 이클립스를 기반으로 주요한 Spring 지원 플러그인과 관련된 도구를 모아서 **Spring 개발에 최적화 되도록 만들어진 IDE**



#### STS가 제공하는 기능

- Bean 클래스 이름 자동완성
  - 클래스 이름 입력시 'SDD'를 입력하면 SDD로 시작하는 클래스를 자동으로 보여줌
- 설정파일(XML) 생성 위저드
  - Bean 설정파일 생성 위저드 중 사용할 Namespace와 Schema 버전을 선택
- Bean 의존관계 그래프
  - Spring IDE가 XML 설정파일을 읽어서 자동으로 그래프 그려줌
  - 어떤 **Property**를 가지는지 알 수 있음
- AOP(관점 지향 프로그래밍) 적용 대상 표시
  - XML 설정파일 편집기를 이용하면 AOP의 적용 대상을 손쉽게 확인



## 2. Maven과 Library 관리

> http://maven.apache.org 참고, 라이브러리 관리 + 빌드 툴
>
> 빌드란 Java코드를 컴파일하고, jar로 묶고, 배포(ANT의 역할)



#### 사용하는 이유

- 편리한 **Dependent Library** 관리
  - jar간의 호출관계 : Dependent Library
- 여러 프로젝트에서 프로젝트 정보나 **jar파일**들을 공유하기 쉬움
- 모든 프로젝트의 **빌드 프로세스**를 일관되게 가져갈 수 있음



### pom.xml

- Maven 프로젝트를 생성하면 pom.xml 파일이 생성
- Project Object Model 정보를 담고 있다.



### pom.xml 의존관계(dependency) 추가

- 의존관계 추가란 Library 추가
- http://mvnrepository.com 접근
- org.springframework로 검색
- spring-jdbc 모듈과 spring-web 모듈을 추가



- Eclipse에서 Maven Repositories View 보기
  - window - show view - Other - Maven - Maven Repository



## 3. Spring Project 작성하기

- Java Project -> Convert to Maven Project -> Add Spring Project Nature