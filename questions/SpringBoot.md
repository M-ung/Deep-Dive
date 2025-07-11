# SpringBoot Questions

## 🤷🏻‍♂️ Spring Boot에서 YAML 설정 파일을 사용해 환경별로 다른 프로파일을 설정하고 적용하는 방법에 대해 설명해보세요. 이를 통해 효율적으로 환경 관리를 어떻게 할 수 있는지 경험을 공유해 주세요.

### 🙆🏻‍♂️ 답변
> Spring Boot의 YAML 파일을 사용하면 환경별로 프로파일을 설정할 수 있습니다. `application-{profile}.yml` 형식으로 파일을 작성하고 활성화할 프로파일을 `spring.profiles.active`로 설정하면 됩니다. <br>이전 프로젝트에서는 개발, 테스트, 프로덕션 환경에 따라 다른 데이터베이스 설정을 적용하여 관리했습니다. 이를 통해 코드 변경 없이 환경에 따라 자동으로 설정이 적용되어 효율성을 극대화할 수 있었습니다. 

### 🔑 키워드
> Spring Boot, YAML, 프로파일 설정

<hr>

## 🤷🏻‍♂️ 복잡한 비즈니스 로직을 구현하는 코드에 대해 단위 테스트를 작성할 때, 발생할 수 있는 일반적인 문제 중 하나는 무엇이며, 이를 어떻게 해결하셨나요?

### 🙆🏻‍♂️ 답변
> 복잡한 비즈니스 로직은 테스트 경계를 정의하는 데 어려움을 줍니다. 제 경험상, 로직을 작게 분리하여 각 모듈을 개별적으로 테스트하는 접근이 효과적이었습니다. <br>이러한 분리로 인해 테스트 범위가 명확해지고, 유지보수가 용이해졌습니다. 또한, 모의 객체(Mock)를 활용하여 외부 의존성을 제거하고 로직 자체에 집중할 수 있었습니다.

### 🔑 키워드
> 테스트 & 코드 품질, 단위 테스트, 모듈화, 모의 객체, 비즈니스 로직, 테스트 경계

<hr>

## 🤷🏻‍♂️ SpringBoot에서 빈(Bean) 등록 방식 중 @Component와 @Bean의 차이점과, 실무에서 이를 효과적으로 사용한 사례를 설명하시오.

### 🙆🏻‍♂️ 답변
> @Component는 자동 탐지를 통해 빈을 등록하고, @Bean은 메서드를 통해 명시적으로 정의합니다. 프로젝트 초기 단계에서 자동 탐지된 빈들이 예외를 발생시켰을 때, @Bean으로 전환하여 문제를 해결했던 경험이 있습니다. 복잡한 설정이 필요한 경우에는 @Bean을 사용하여 더욱 세밀한 제어가 가능했습니다.

### 🔑 키워드
> SpringBoot, Bean, @Component, @Bean, 빈 등록

<hr>

## 🤷🏻‍♂️ Spring Boot 기반의 마이크로서비스 아키텍처에서 AOP를 이용하여 서비스 간 로깅을 구현할 때, 성능 이슈를 최소화하면서도 효과적인 로그 관리를 위해 어떠한 전략을 사용했는지 설명해 주세요.

### 🙆🏻‍♂️ 답변
> 실무에서 우리는 서비스 간의 로깅을 AOP로 구현했으며, 성능 저하를 막기 위해 비동기 로깅을 채택했습니다. 또한, 로그 레벨을 동적으로 변경할 수 있는 설정을 추가하여 필요 시에만 상세 로그를 기록하도록 했습니다. 이를 통해 시스템 부하를 줄이면서도 문제가 발생했을 때 빠르게 대응할 수 있었습니다.

### 🔑 키워드
> SpringBoot, AOP, 비동기 로깅, 성능 최적화

<hr>