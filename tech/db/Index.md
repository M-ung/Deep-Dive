# Index
인덱스는 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조로 백과사전의 목차와 같습니다. 

저장되는 컬럼의 값을 사용하여 항상 정렬된 상태를 유지하는 것이 특징입니다. 이러한 특징으로 인해 인덱스는 INSERT, UPDATE, DELETE의 성능이 희생된다는 것이 단점입니다.

## 🤷🏻‍♂️ 인덱스는 어떤 자료 구조로 이루어져있나요?
MySQL InnoDB를 기준으로 설명드리자면, B+Tree와 같은 변형 B-Tree 자료구조를 이용해서 인덱스를 구현합니다. 

기본 토대는 B-Tree 인덱스이기 때문에 이를 기준으로 설명하겠습니다.
B-Tree 인덱스는 컬럼의 값을 변형하지 않고 인덱스 구조체 내에서 항상 정렬된 상태로 유지합니다.

B-Tree(Balanced-Tree)에서는 크게 3가지 노드가 존재합니다. 
최상위에 하나의 루트 노드가 존재하며, 가장 하위 노드인 리프 노드가 존재합니다. 
이 두 노드의 중간에 존재하는 브랜치 노드가 존재합니다. 최하위 노드인 리프 노드에는 실제 데이터 레코드를 찾아가기 위한 주소값을 가지고 있습니다.

InnoDB 스토리지 엔진에서는 세컨더리 인덱스의 리프 노드에는 레코드의 PK가 저장됩니다. 따라서 세컨더리 인덱스 검색에서는 레코드를 읽기 위해 PK를 가지고 있는 B-Tree를 다시 한번 검색해야 합니다.

## 🤷🏻‍♂️ MySQL 스캔 방식은 어떤 게 있나요?
MySQL에는 크게 아래와 같은 방식들로 구성되어 있습니다. 그리고 InnoDB는 상황에 맞게 아래 세 가지 인덱스 조회 방식을 자동으로 선택해서 사용합니다.

1️⃣ 인덱스 레인지 스캔 <br>
인덱스 레인지 스캔은 검색할 인덱스 범위가 결정되었을 경우 사용하며 가장 빠릅니다.

1. `index seek` : 인덱스에서 조건을 만족하는 값이 저장된 시작 리프 노드를 찾습니다.
2. `index scan` : 시작 리프 노드부터 필요한 만큼 인덱스를 차례대로 읽습니다.
3. 인덱스 키와 레코드 주소를 이용해 저장된 페이지를 가져오고 레코드를 읽어옵니다.

하지만 레코드를 읽어오는 과정에서 랜덤 IO가 발생할 수 있습니다. 그렇기 때문에 읽어야할 데이터 레코드가 전체 20-25%의 경우에는 풀 테이블 스캔이 더 좋을 수 있습니다.

2️⃣ 인덱스 풀 스캔 <br>
인덱스 풀 스캔은 인덱스를 사용하지만 인덱스를 처음부터 끝까지 모두 읽는 방식입니다.

- 인덱스를 ABC 순서로 만들었는데 조건절에 B 혹은 C로 검색하는 경우 사용됩니다.
- 인덱스를 생성하는 목적은 아니지만, 그래도 풀 테이블 스캔보다는 낫습니다.

3️⃣ 루스 인덱스 스캔 <br>
루스 인덱스 스캔은 듬성듬성하게 인덱스를 읽는 것을 의미합니다.

- 중간에 필요하지 않은 인덱스 키 값은 무시하고 다음으로 넘어가는 형태로 처리합니다.
- `group by`, `max()`, `min()` 함수에 대해 최적화하는 경우에 사용됩니다.

## 🤷🏻‍♂️ B-Tree 말고, 다른 자료구조도 궁금해요.
데이터베이스 인덱스에서 사용되는 주요 자료구조들을 간략히 알아보겠습니다.

### 1. B+Tree
B-Tree의 변형으로, 리프 노드들이 연결 리스트로 연결되어 있습니다.

**특징**
- 모든 데이터는 리프 노드에만 저장됩니다.
- 범위 검색이 매우 효율적입니다.
- MySQL InnoDB의 기본 인덱스 구조입니다.

### 2. Hash Index
해시 함수를 사용하여 키를 해시 값으로 변환하는 인덱스입니다.

**특징**
- 정확한 일치 검색이 O(1) 시간 복잡도입니다.
- 범위 검색에는 비효율적입니다.
- MySQL MEMORY 스토리지 엔진에서 사용됩니다.