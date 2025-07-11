# Kafka Questions

## 🤷🏻‍♂️ Kafka에서 여러 팀이 동일한 토픽을 사용할 때 발생할 수 있는 문제는 무엇이며, 이를 어떻게 효과적으로 해결할 수 있을까요?

### 🙆🏻‍♂️ 답변
> 여러 팀이 같은 토픽을 사용할 경우 메시지 포맷 변경이나 토픽 설정 조정이 어려워지고 충돌이 발생할 수 있습니다. 이를 해결하기 위해서는 스키마 레지스트리를 활용해 메시지 포맷을 관리하고, 각 팀과의 명확한 협업 규칙을 설정합니다. <br>실제로, 과거 프로젝트에서는 스키마 레지스트리를 통해 포맷 호환성을 유지하며 협업 문제를 해결했던 경험이 있습니다.

### 🔑 키워드
> Kafka, 토픽 공유, 스키마 레지스트리, 협업 규칙

<hr>

## 🤷🏻‍♂️ 당신이 관리하는 Kafka 클러스터에서 토픽의 파티션 수를 조정해야 하는 상황이 생겼습니다. 토픽 사용량의 급격한 증가로 인해 성능 문제를 겪고 있을 때, 어떤 방식을 통해 문제를 진단하고 파티션 수 조정 결정을 내리겠습니까? 구체적인 상황과 대응 과정을 설명해주세요.

### 🙆🏻‍♂️ 답변
> 이전에 서비스의 사용자 수가 폭발적으로 증가하면서 특정 토픽의 메시지 처리 속도가 병목 현상을 일으켰습니다. 먼저, 모니터링 툴을 통해 토픽의 메시지 처리량과 소비자 그룹의 소비 속도를 분석했습니다. 이후 병목 구간을 확인한 뒤, 파티션을 늘렸고, 소비자 그룹의 스케일링 전략을 조정하여 성능을 최적화했습니다.

### 🔑 키워드
> Kafka, 파티션 조정, 성능 최적화, 모니터링, 소비자 그룹

<hr>