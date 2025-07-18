# Log and Metric

로그는 서버가 동작할 때, 서버의 상태와 동작 정보를 시간 경과에 따라 기록된 결과입니다. 즉, 시스템의 오류와 문제들을 쉽게 찾아낼 수 있도록 도와주는 역할을 합니다.

반면, 메트릭은 시스템의 성능과 상태에 대한 통계적인 정보를 의미합니다. 메트릭을 잘 수집하면, 시스템의 현재 상태를 손쉽게 파악할 수 있으며 사업현황에 관한 유용한 정보를 얻을 수 있습니다. 예를 들어, DAU, Retension, CPU 사용량, 메모리 사용량 등이 있습니다.

## 🤷🏻‍♂️ 로깅과 메트릭을 어떻게 수집하나요?

### 1. 메트릭 수집 방법

**Spring Boot Actuator**
- 애플리케이션의 상태와 메트릭을 자동으로 수집
- `/actuator` 엔드포인트를 통해 메트릭 노출

**Prometheus**
- 메트릭 데이터를 수집하고 저장
- 시계열 데이터베이스로 장기 보관

**Grafana**
- 수집된 메트릭을 시각화
- 대시보드를 통한 실시간 모니터링

**수집 가능한 지표**
- **시스템 리소스**: CPU, 메모리, JVM 힙 사용량
- **애플리케이션 상태**: 톰캣 스레드 풀과 데이터베이스 커넥션 풀 상태
- **에러 모니터링**: error 레벨 로그 증가량

### 2. 로깅 수집 방법

**Logback**
- Spring Boot의 기본 로깅 프레임워크
- 다양한 로그 레벨과 출력 형식 지원

**Loki**
- 로그 수집 및 저장 시스템

**MDC (Mapped Diagnostic Context)**
- 로그 추적을 위한 컨텍스트 정보 추가
- 요청별 고유 식별자로 로그 연결

## 🤷🏻‍♂️ 왜 로깅과 메트릭이 중요한가요?

### 1. 문제 진단
- **에러 로그**: 문제 발생 원인 파악
- **메트릭**: 성능 병목 지점 식별

### 2. 성능 모니터링
- **실시간 모니터링**: 시스템 상태 파악
- **트렌드 분석**: 성능 변화 추이 확인

### 3. 사용자 경험 개선
- **응답 시간**: 사용자 만족도에 직접적 영향
- **가용성**: 서비스 중단 시간 최소화

## 🤷🏻‍♂️ `System.out.println`을 사용하면 로깅 프레임워크는 사용하지 않아도 되지 않나요?
로그 출력에도 대기 시간이 발생합니다. 그리고 로그 자체는 하나의 데이터이기 때문에 저장 공간 또한 요구합니다. 

따라서 필요한 경우에만 로그 수행하는 것이 비용적으로 좋습니다. 하지만 `System.out.println`은 로그 레벨 설정과 환경 별 필터링을 적용하기가 까다롭습니다. 

그렇기 때문에 로깅 프레임워크를 사용하는 것이 효율적입니다.