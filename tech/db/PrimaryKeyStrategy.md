# Primary Key Strategy

**Primary Key**는 데이터베이스 테이블에서 각 행을 고유하게 식별하는 컬럼입니다.

데이터베이스 기본 키는 다음 3가지 조건을 모두 만족해야 합니다.

## 📋 기본 키의 3가지 조건

1. **`null` 값은 허용하지 않는다.**
2. **유일해야 한다.**
3. **변해선 안 된다.**

## 🤷🏻‍♂️ 테이블의 기본 키 선택 전략

테이블의 기본 키를 선택하는 전략은 크게 2가지가 있습니다.

### 1. 자연 키 (Natural Key)
비즈니스에 의미가 있는 키입니다.

**예시**
- 주민등록번호
- 이메일
- 전화번호

### 2. 대리 키 (Surrogate Key)
비즈니스와 관련 없는 임의로 만들어진 키로, 대체 키로도 불립니다.

**예시**
- 오라클 시퀀스
- auto_increment
- identity
- 키생성 테이블 사용

## 🤷🏻‍♂️ 자연키와 대리키 중 어떤 걸 사용할까요?

먼저 결론부터 말하자면, 자연 키보다는 대리 키를 권장합니다.

자연 키와 대리 키는 일장 일단이 있지만, 될 수 있으면 대리 키의 사용을 권장합니다.

**자연 키의 문제점**
예를 들어 자연 키인 전화번호를 기본 키로 선택한다면, 그 번호가 유일할 수는 있지만 전화번호가 없을 수도 있고 전화번호가 변경될 수도 있습니다. 따라서 기본 키로 적당하지 않습니다.

문제는 주민등록번호처럼 그럴듯하게 보이는 값입니다. 이 값은 `null`이 아니고 유일하며 변하지 않는다는 3가지 조건을 모두 만족하는 것 같습니다. 하지만 현실과 비즈니스 규칙은 생각보다 쉽게 변합니다. 주민등록번호조차도 여러 가지 이유로 변경될 수 있습니다.

비즈니스 환경은 언젠가 변합니다.

<details>
<summary><strong>실제 경험 사례</strong></summary>

레거시 시스템을 유지보수할 일이 있었는데, 분석해보니 회원 테이블에 주민등록번호가 기본 키로 잡혀 있었습니다. 회원과 관련된 수많은 테이블에서 조인을 위해 주민등록번호를 외래 키로 가지고 있었고, 심지어 자식 테이블의 자식 테이블까지 주민등록번호가 내려가 있었습니다.

문제는 정부 정책이 변경되면서 법적으로 주민등록번호를 저장할 수 없게 되면서 발생했습니다. 결국 데이터베이스 테이블은 물론이고 수많은 애플리케이션 로직을 수정했습니다.

만약 데이터베이스를 처음 설계할 때부터 자연 키인 주민등록번호 대신에 비즈니스와 관련 없는 대리 키를 사용했다면, 수정할 부분이 많지는 않았을 것입니다.

</details>

## 💡 결론

기본 키의 조건을 현재는 물론이고 미래까지 충족하는 자연 키를 찾기는 쉽지 않습니다. 대리 키는 비즈니스와 무관한 임의의 값이므로 요구사항이 변경되어도 기본 키가 변경되는 일은 드뭅니다.

대리 키를 기본 키로 사용하되, 주민등록번호나 이메일처럼 자연 키의 후보가 되는 컬럼들은 필요에 따라 유니크 인덱스를 설정해서 사용하는 것을 권장합니다.

참고로 JPA는 모든 엔티티에 일관된 방식으로 대리 키 사용을 권장합니다.

비즈니스 요구사항은 계속해서 변하는데, 테이블은 한 번 정의하면 변경하기 어렵습니다. 그런 면에서 외부 풍파에 쉽게 흔들리지 않는 대리 키가 일반적으로 좋은 선택이라고 생각합니다.

```java
@Entity
public class Member {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id; // 대리 키
    
    @Column(unique = true)
    private String email; // 자연 키 후보 (유니크 인덱스)
    
    // ... 다른 필드들
}
```

> **💡 핵심 포인트**: 비즈니스 환경의 변화에 대응하기 위해 대리 키를 사용하고, 자연 키 후보는 유니크 인덱스로 관리하는 것이 안전한 전략입니다. 