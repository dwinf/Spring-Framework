# 1강 Framework 개념

> SW 재사용성을 높일 수 있는 방안데 대해 이해
>
> 디자인패턴과 프레임워크의 관련성에 대해 이해
>
> 프레임 워크 구성요소와 종류 이해



## 1. SW 재사용 방안

### 1) 복사(copy) & 붙이기(paste)

- 가장 기본적
- A라는 클레스에서 Data 타입을 String 타입으로 변환하는 코딩, 클래스 B에 동일한 로직이 필요해 복사한 경우
  - 변동이 생길 경우 A, B클래스 모두 변경해야 한다.

```java
GregorianCalendar date = (GregorianCalendar)Calendar.getInstance();
SimpleDateFormat df = new SimpleDateFormat("yyyyMMdd");
String date = df.format(date);
```



### 2) Method(function)

- 필요한 코드를 메서드로 정의
- 필요한 경우 메서드를 호출하여 사용
- 수정이 필요한 경우 메서드만 수정하면 된다.
- 단, 메서드의 Signature가 바뀐 경우 이 메서드를 호출하는 모든 클래스에 영향을 준다.
  - 메서드의 Signature란, 메서드 명, 리턴타입, 아규먼트 갯수, 타입 등을 의미
- 복붙보다 발전된 형태지만 작업 영역간의 결합도(Coupling) 문제가 여전히 존재
  - 결합도 - 작업 영역간 연관관계, 영향을 미치는 정도..?

```java
public class DateUtility{
    public static String toStringToday(String format){
        GregorianCalendar date = (GregorianCalendar)Calendar.getInstance();
		SimpleDateFormat df = new SimpleDateFormat("yyyyMMdd");
		String date = df.format(date);
    }
}
String sdate = DateUtility.toStringToday("yyyyMMdd");
```



### 3) Class(Inheritance)

- 클래스 재사용(상속)
- 자주 사용되는 기능들을 모아 메서드로 정의하여 사용
- Person을 상속받은 모든 클래스는 자동적으로 변경된 printBirthDate() 메서드 사용
- 부모 클래스의 Signature가 바뀌지 않는한 다른 클래스는 영향을 받지 않는다.

```java
public class Person{
	public String printBirthDate(String format){
		DateUtility.toStringToday(birthDate, format);
	}
}
```



### 4) AOP(Aspect Oriented Programming)

- 관심의 분리(Seperatrion of Concerns)

-  oop 대체보다는 support 느낌
  - oop를 더 oop스럽게
- oop뿐 아니라 절차적 프로그래밍에도 적용
- **`위빙`** : 핵심관심모듈과 횡단관심모듈을 합쳐지게 만드는 작업
  - F/W에서 한다.

- AOP에서 **위빙**작업을 통해 핵심 모듈 사이에 필요한 횡단 관심 코드가 동작하도록 엮어지게 만든다.





## 2. 디자인 패턴과 프레임워크의 관련성

### 디자인패턴의 정의

> 프로그램 개발에서 자주 나타나는 과제를 해결하기 위한 방법 중 하나로, 소프트웨어 개발과정에서 발견된 **Know-How**를 축적하여 이름을 붙여 이후에 **재사용하기 좋은 형태로 특정 규약을 묶어서 정리**한 것.

- 대표적으로 GoF(Gang of Four)패턴이 있다.
  - 4명의 과학자가 만들어서 Four
  - 23가지 디자인 패턴 제공



#### 디자인 패턴을 사용하는 이유

- 요구사항은 수시로 변경 -> 요구사항 변경에 대한 Source Code 변경을 최소화
- 여러 사람이 같이 하는 팀 프로젝트 진행 -> 범용적인 코딩 스타일을 적용
- 상황에 따라 인수 인계하는 경우 발생 -> 직관적인 코드를 사용



### 프레임워크의 정의

> **비기능적 요구사항(성능, 보안, 확장성, 안정성 등)을 만족하는 구조**와 구현된 기능을 **안정적으로 실행하도록 제어**해주는 잘 만들어진 구조의 라이브러리 덩어리

- 어플리케이션들의 최소한의 공통점을 찾아 하부 구조를 제공함으로써 개발자들로 하여금 시스템의 하부 구조를 구현하는데 들어가는 노력을 절감하게 해줌



#### 프레임워크를 사용하는 이유

- 비기능적인 요소들을 개발 초기 단계마다 구현해야 하는 불합리함을 극복
- 기능적인 요구사항에 집중할 수 있게 해줌
- 디자인 패턴과 마찬가지로 반복적으로 발견되는 문제(한글이 깨져서 인코딩 등)를 해결하기 위한 특화된 Solution을 제공



### 디자인패턴과 프레임워크의 관련성

> 디자인 패턴은 프레임워크의 핵심적인 특징, 프레임워크에서 디자인패턴을 내부적으로 사용. **하지만 프레임워크는 디자인패턴이 아니다.**

- 프레임워크는 디자인 패턴과 함께 패턴이 적용된 **기반 클래스 라이브러리를 제공**해서 프레임워크를 사용하는 **구조적인 틀과 구현코드를 함께 제공**한다.
- 프레임워크는 디자인 패턴을 내부적으로 사용하기 때문에 개발자가 프레임워크를 사용하면 자연스럽게 프레임워크에 적용된 디자인패턴을 적용할 수 있다.



## 3. 프레임워크의 구성요소와 종류

### 1.  IoC(Inversion of Control) : 제어의 역전

> IoC란, "제어의 역전" 즉, 인스턴스 생성부터 소멸을 개발자가 아닌 컨테이너가 대신 해준다. 컨테이너 역할을 해주는 프레임 워크에게 제어하는 권한을 넘겨서 개발자의 코드가 신경쓸 부분을 줄이는 전략

| F/W(IoC)                               | Library                    |
| -------------------------------------- | -------------------------- |
| 프레임워크가 개발자가 작성한 코드 호출 | 개발자가 라이브러리를 호출 |
| 프레임워크에게 주도권                  | 개발자에게 주도권          |

- 프레임워크가 주도권을 가지고 있기 때문에 일반적인 프로그램 흐름과 반대로 동작
- Spring 컨테이너가 IoC 지원, 메타데이터(XML설정)을 통해 beans를 관리하고 어플리케이션의 중요부분을 구성
  - `bean` : Spring 컨테이너에서 생성되는 객체
- Spring 컨테이너는 bean들을 **의존성주입(Dependency Injection)**을 통해 IoC 지원

####  IoC/DI?



### 2. Class Library

> 프레임워크는 특정 부분의 기술적인 구현을 라이브러리 형태로 제공. 프레임워크를 "Semi Complete(반제품)"이라고 해석하게 만듬

#### 라이브러리와 프레임워크의 차이점

- 실행제어가 어디서 일어나는가
- `라이브러리`는 개발자가 만든 클래서에서 직접 호출하여 사용하므로 **실행흐름에 대한 제어를 개발자 코드가 관장**
- `프레임워크`는 **프레임워크에서** 개발자가 만든 클래스를 호출하여 **실행의 흐름에 대한 제어를 담당**
  - IoC를 지원한다.



### 3. Design pattern

> **디자인 패턴 + 라이브러리 = 프레임워크**

- 라이브러리를 살펴볼 때 적용된 패턴을 보면 구성을 이해하기 쉽다.

- 프레임워크를 확장하거나 커스터마이징 할때 적용된 패턴에 대한 이해가 꼭 필요하다.

  

#### 프레임워크의 종류

> 아키텍쳐 결정 = 사용하는 프레임워크의 종류 + 사용전략

| 기능                       | 프레임워크 종류                          |
| -------------------------- | ---------------------------------------- |
| 웹(MVC)                    | **Spring MVC**, Struts2, Webwork         |
| OR(Object=Relational) 매핑 | **MyBatis**, Hibernate, JPA, Spring JDBC |
| AOP                        | **Spring AOP**, AspectJ, JBoss AOP       |
| DI(Dependency Injection)   | **Spring DI**                            |
| Build와 Library 관리       | **Maven**                                |
| 단위 테스트                | **jUnit**                                |
| JavaScript                 | **jQuery**                               |