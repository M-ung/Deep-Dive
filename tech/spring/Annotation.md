# Annotation
애너테이션은 자바 코드에 붙여서 컴파일러나 실행 환경에게 특별한 의미나 지시를 전달하는 메타데이터입니다.

## 🤷🏻‍♂️ `@Component`, `@Controller`, `@Service`, `@Repository`의 차이점에 대해서 설명해주세요.
`@Component`, `@Service`, `@Controller`, `@Repository`는 각각의 클래스를 특정 역할을 수행하는 Spring Bean으로 등록할 때 사용됩니다. 

각 애너테이션은 클래스가 어떤 역할을 하는지를 명시적으로 나타내며, Spring의 `@ComponentScan` 기능을 통해 자동으로 Bean으로 등록됩니다. `@Service`, `@Controller`, `@Repository` 어노테이션은 내부적으로 `@Component` 어노테이션을 사용하고 있으며, 각 특징과 용도는 아래와 같습니다.

>`@Component` <br>
가장 일반적인 형태의 어노테이션으로, 특정 역할에 종속되지 않는 일반적인 Spring Bean을 나타냅니다. 공통 기능을 제공하는 유틸리티 클래스나, 특정 계층에 속하지 않는 일반적인 컴포넌트를 정의할 때 사용됩니다.

>`@Service` <br> 
비즈니스 로직을 수행하는 클래스에 사용되며 서비스 레이어의 Bean을 나타냅니다.

>`@Controller` <br> 
Spring MVC에서 웹 요청을 처리하는 컨트롤러 클래스에 사용되며 프레젠테이션 레이어의 Bean을 나타냅니다.

>`@Repository` <br>
데이터베이스와의 상호작용을 수행하는 클래스에 사용되며. 데이터 액세스 레이어의 Bean을 나타냅니다.

## 🤷🏻‍♂️ @Controller, @Repository 대신 @Component 사용하면 안되나요?
Spring 6(Spring Boot 3) 이전 버전에서는 `@Component` + `@RequestMapping`으로도 Bean 및 핸들러로 등록되었습니다. 하지만 Spring 6 이후 부터 `@Controller` 외에는 핸들러로 등록하지 않아 웹 요청을 정상적으로 수행할 수 없습니다.

그렇기 떄문에 `@Controller` 대신에 `@Component`를 사용하는 것은 불가능합니다.

`@Repository`를 `@Component`로 대체할 경우, `PersistenceExceptionTranslationPostProcessor`에 의해 예외가 `DataAccessException`으로 변환되지 않습니다. 이 경우 데이터 액세스 계층에서 발생하는 예외 처리에 영향을 미칠 수 있습니다.

또 `@Service`, `@Controller`, `@Repository`는 각각 특정 계층을 나타내므로, AOP의 포인트컷을 정의할 때 유용하게 사용될 수 있습니다. `@Component`를 사용하면 이러한 계층 구분이 불분명해져 AOP 적용이 어려울 수 있습니다.

> **AOP의 포인트컷이란?** <br>
> AOP에서 “어디에” 공통 로직을 적용할지를 결정하는 조건입니다.