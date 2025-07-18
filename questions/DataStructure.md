# Data Structure Questions

## 🤷🏻‍♂️ 대규모의 사용자 데이터를 처리하고 검색하는 시스템에서 이진 탐색 트리(BST)의 사용이 적합하지 않은 경우를 설명하고, 이에 대한 대안으로 사용할 수 있는 자료구조를 제안하세요.

### 🙆🏻‍♂️ 답변
> 이진 탐색 트리는 데이터가 정렬된 경우 삽입과 삭제 시, 불균형 문제가 발생할 수 있습니다. 이로 인해 최악의 경우 O(n)의 시간 복잡도를 가지게 됩니다. 대안으로는 AVL 트리나 레드-블랙 트리처럼 균형을 유지하는 자가 균형 이진 탐색 트리를 사용하여 삽입과 삭제 시에도 O(log n)의 성능을 보장할 수 있습니다.

### 🔑 키워드
> 자료구조, 이진 탐색 트리, AVL 트리, 레드-블랙 트리

<hr>

## 🤷🏻‍♂️ 우리 서비스의 유저 추천 시스템에서 리스트를 사용하여 데이터를 처리하고 있습니다. 이 시스템의 성능을 개선하기 위해 어떤 자료구조나 알고리즘을 고려해야 하는지 설명해 주세요.

### 🙆🏻‍♂️ 답변
> 추천 시스템에서 리스트를 사용하고 있다면, 대량의 데이터 처리에 효율적인 자료구조로 전환하는 것이 좋습니다. 예를 들어, 데이터 탐색 시간이 중요한 경우 해시맵을 사용하거나, 데이터가 정렬된 경우 이진 탐색 트리로 전환하여 성능을 향상시킬 수 있습니다. 과거에 유사한 문제를 해결하기 위해 우리는 큐와 해시맵을 결합하여 실시간 처리를 최적화했던 경험이 있습니다.

### 🔑 키워드
> 자료구조, 리스트, 자료구조, 추천 시스템, 성능 최적화, 알고리즘

<hr>

## 🤷🏻‍♂️ 대규모 소셜 네트워크 서비스를 운영하면서 사용자 간의 관계를 그래프로 모델링했습니다. 데이터베이스의 성능 문제로 인해 요청 시간이 증가하는 상황에서, 어떤 최적화 방법을 고려할 수 있을까요?

### 🙆🏻‍♂️ 답변
> 사용자 관계를 그래프로 모델링했다면, 네오4j 같은 그래프 데이터베이스로 마이그레이션을 고려할 수 있습니다. 또한, 사용자 간의 관계를 캐싱하여 요청 시에 즉시 조회할 수 있도록 하는 것도 성능 개선에 유의미합니다. 예를 들어, 자주 조회되는 사용자 관계를 Redis에 저장하여 응답 시간을 단축할 수 있습니다. 최적화는 시스템 성능 및 사용자 경험에 직접적인 영향을 미치기 때문에 중요한 결정이었습니다.

### 🔑 키워드
> 자료구조, 그래프 데이터베이스, 성능 최적화, 캐싱

<hr>