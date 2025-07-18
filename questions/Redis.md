# Redis Questions

## 🤷🏻‍♂️ Redis의 Sorted Set은 어떻게 사용하며, 이 데이터 구조를 활용하여 실시간 랭킹 시스템을 구현한 경험에 대해 설명해주세요.

### 🙆🏻‍♂️ 답변
> 과거에 이벤트 프로모션의 실시간 랭킹을 구현할 때 Redis의 Sorted Set을 사용했습니다. 점수에 따라 사용자 ID를 Sorted Set에 저장하여 상위 사용자 순위를 빠르게 조회할 수 있었습니다. <br>덕분에 실시간으로 업데이트되는 이벤트 랭킹을 효율적으로 제공할 수 있었고, 사용자 참여도가 크게 향상되었습니다.

### 🔑 키워드
> Redis, Sorted Set, 실시간 랭킹 시스템

<hr>

## 🤷🏻‍♂️ Redis의 Pub/Sub을 사용하여 실시간 알림 시스템을 구축하려고 합니다. 사용자가 많아지면서 메시지 전송 지연이 발생했을 때, 어떤 조치를 취할 수 있을까요?

### 🙆🏻‍♂️ 답변
> 실시간 알림 시스템에서 메시지 전송 지연이 발생할 경우, 첫 번째로 Redis 클러스터를 통해 스케일링을 고려할 수 있습니다. 그런 다음, 메시지를 브로드캐스트 방식이 아닌 그룹별로 특정 대상에게만 전송하는 방법으로 최적화할 수 있습니다. 마지막으로, 메시지 큐 시스템을 병렬로 사용하여 메시지 처리량을 분산시켜 성능을 개선할 수 있습니다.

### 🔑 키워드
> Redis, Pub/Sub, 메시지 큐, 스케일링, 성능 최적화

<hr>

## 🤷🏻‍♂️ 웹 서비스의 성능 최적화를 위해 캐싱을 도입할 때, 데이터 일관성과 캐시 갱신 주기를 어떻게 설정했는지 설명하고, 그 결정이 서비스에 어떤 영향을 미쳤는지 사례를 들어 이야기해 주세요.

### 🙆🏻‍♂️ 답변
> 대량의 사용자 요청으로 발생하는 부하를 줄이기 위해 캐싱을 도입했습니다. 데이터 일관성이 중요한 경우, Redis를 사용하여 TTL(Time-To-Live)을 짧게 설정해 주기적으로 갱신했습니다. 이를 통해 실시간 데이터와의 차이는 최소화하면서도 서버 부하를 줄일 수 있었습니다. 이 결정은 사용자 경험을 개선하고 서버 운영 비용을 줄이는 데 큰 기여를 했습니다.

### 🔑 키워드
> Redis, 트래픽 처리, 인프라, 캐싱, 데이터 일관성, TTL, 서버 부하

<hr>

## 🤷🏻‍♂️ Redis Pub/Sub을 사용하여 실시간 알림 시스템을 구축할 때, 구독자가 너무 많아서 메시지 전송 속도가 느려지는 상황이 발생했습니다. 이 문제를 해결하기 위해 어떤 접근법을 사용했나요?

### 🙆🏻‍♂️ 답변
> 실시간 알림 시스템에서 구독자가 많아져 전송 속도가 느려질 경우, 메시지를 큐잉 시스템과 함께 사용하여 해결했습니다. Redis Pub/Sub는 구독자에게 즉시 메시지를 전달하지만, 구독자 사이의 처리 속도 차이로 인해 병목이 발생할 수 있습니다. 이를 개선하기 위해, 메시지를 메시지 큐(예: RabbitMQ)로 전달한 다음 각 구독자가 큐에서 메시지를 비동기적으로 가져가도록 하여 처리 속도를 개선했습니다.

### 🔑 키워드
> Redis, Pub/Sub, 메시지 큐, 비동기 처리, Redis, RabbitMQ

<hr>