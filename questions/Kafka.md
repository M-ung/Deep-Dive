# Kafka Questions

## 🤷🏻‍♂️ Kafka에서 여러 팀이 동일한 토픽을 사용할 때 발생할 수 있는 문제는 무엇이며, 이를 어떻게 효과적으로 해결할 수 있을까요?

### 🙆🏻‍♂️ 답변
> 여러 팀이 같은 토픽을 사용할 경우 메시지 포맷 변경이나 토픽 설정 조정이 어려워지고 충돌이 발생할 수 있습니다. 이를 해결하기 위해서는 스키마 레지스트리를 활용해 메시지 포맷을 관리하고, 각 팀과의 명확한 협업 규칙을 설정합니다. <br>실제로, 과거 프로젝트에서는 스키마 레지스트리를 통해 포맷 호환성을 유지하며 협업 문제를 해결했던 경험이 있습니다.

### 🔑 키워드
> Kafka, 토픽 공유, 스키마 레지스트리, 협업 규칙

<hr>