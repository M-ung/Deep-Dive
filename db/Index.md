# Index
인덱스는 데이터베이스 테이블의 검색 속도를 향상시키기 위한 자료구조로 백과사전의 색인과 같습니다. 

저장되는 컬럼의 값을 사용하여 항상 정렬된 상태를 유지하는 것이 특징입니다. 이러한 특징으로 인해 인덱스는 INSERT, UPDATE, DELETE의 성능이 희생된다는 것이 단점입니다.

## 🤷🏻‍♂️ 인덱스는 어떤 자료 구조로 이루어져있나요?
MySQL InnoDB를 기준으로 설명드리자면, B+Tree와 같은 변형 B-Tree 자료구조를 이용해서 인덱스를 구현합니다. 

기본 토대는 B-Tree 인덱스이기 때문에 이를 기준으로 설명합니다. 
B-Tree 인덱스는 컬럼의 값을 변형하지 않고 인덱스 구조체 내에서 항상 정렬된 상태로 유지합니다.

B-Tree(Balanced-Tree)에서는 크게 3가지 노드가 존재합니다. 
최상위에 하나의 루트 노드가 존재하며, 가장 하위 노드인 리프 노드가 존재합니다. 
이 두 노드의 중간에 존재하는 브랜치 노드가 존재합니다. 최하위 노드인 리프 노드에는 실제 데이터 레코드를 찾아가기 위한 주소값을 가지고 있습니다.

InnoDB 스토리지 엔진에서는 세컨더리 인덱스(프라이머리 인덱스를 제외한 모든 인덱스)의 리프 노드에는 레코드의 PK가 저장됩니다. 따라서 세컨더리 인덱스 검색에서는 레코드를 읽기 위해 PK를 가지고 있는 B-Tree를 다시 한번 검색해야합니다.