# Shared Lock And Exclusive Lock
DBMS에서 트랜잭션을 특별한 제어 없이 병행 수행을 허용한다면, 데이터의 일관성과 무결성을 보장하기 어려울 수 있습니다. 이때 병행 수행되는 트랜잭션들을 제어하기 위해서 락을 사용할 수 있으며, DBMS에서 락은 크게 공유 락과 배타 락으로 분류할 수 있습니다.

공유 락(Shared Lock)은 읽기 락(Read Lock)이라고 부르며, 공유 락이 걸린 데이터에 대해서 다른 트랜잭션에서도 공유 락을 획득할 수 있지만, 배타 락은 획득할 수 없습니다. 즉, 공유 락을 사용하면 트랜잭션 내에서 조회한 데이터가 변경되지 않는다는 것을 보장합니다.

```sql
SELECT * FROM table_name WHERE id = 1 FOR SHARE;
```

그리고 배타 락(Exclusive Lock)은 쓰기 락(Write Lock)이라고 부르며, 배타 락이 걸린 데이터에 대해서 다른 트랜잭션에서는 공유 락과 배타 락을 획득할 수 없습니다. 즉, 배타 락을 획득한 트랜잭션은 데이터에 대한 독점권을 가집니다.

```sql
SELECT * FROM table_name WHERE id = 1 FOR UPDATE;
```

정리하자면, 공유 락이 걸린 데이터는 다른 트랜잭션에서 공유 락을 획득 할 수 있고, 배타 락이 걸린 데이터는 다른 트랜잭션에서 어떤 종류의 락도 획득할 수 없어서 대기하는 상황이 발생할 수 있습니다.

## 🤷🏻‍♂️ 데드 락은 언제 발생하며 어떻게 해결할 수 있나요?
데드 락(Dead Lock)이란 교착 상태로, 두 개 이상의 트랜잭션이 서로 필요로 하는 데이터의 락을 점유하고 있어서 무한히 대기하는 상황을 말합니다. 

트랜잭션은 락을 획득하지 못하는 경우, 다른 트랜잭션이 점유하고 있는 락이 해제될 때까지 대기합니다. 예를 들어, 다음과 같은 트랜잭션들이 존재한다고 가정하겠습니다.

>트랜잭션 A, B가 있고 id가 1, 2인 데이터가 있는 상황에 두 트랜잭션이 시작합니다. <br>
>트랜잭션 A는 id 1번을 읽고, 2번 데이터를 변경하는 트랜잭션입니다. <br>
>트랜잭션 B는 id 2번을 읽고 1번을 변경하는 트랜잭션입니다. <br>

이때 다음과 같은 상황에서 데드 락이 발생할 수 있습니다.

>A는 1번, B는 2번 데이터에 대해 공유 락을 획득합니다. <br>
>A는 2번 데이터의 공유 락을 가지고 있는 B 트랜잭션이 락을 해제할 때까지 대기합니다. <br>
>B는 1번 데이터의 공유 락을 가지고 있는 A 트랜잭션이 락을 해제할 때까지 대기합니다. <br>

데드 락을 해결하기 위해서 트랜잭션에서 락 획득 순서를 일관되게 할 수 있습니다. 모든 트랜잭션에서 1번 데이터, 2번 데이터 순으로 락을 획득할 시 데드 락이 발생하지 않습니다. 혹은 락 타임 아웃을 설정하여 데드 락 상황을 해결할 수 있습니다.