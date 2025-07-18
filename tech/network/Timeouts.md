# Connection Timeout, Socket Timeout and Read Timeout

**Connection Timeout** <br>
Connection Timeout은 클라이언트가 서버에 연결을 시도할 때, 일정 시간 내에 연결이 이루어지지 않으면 발생하는 타임아웃입니다. TCP 소켓 통신에서 클라이언트와 서버가 연결될 때, 정확한 전송을 보장하기 위해 사전에 세션을 수립하는데, 이 과정을 3-way-handshake라고 합니다. 

Connection Timeout은 이 3-way-handshake가 일정 시간 내에 완료되지 않을 때 발생합니다. 즉, 서버의 장애나 응답 지연으로 인해 연결을 맺지 못하면 Connection Timeout이 발생합니다.

**Socket Timeout** <br>
Socket Timeout은 Connection Timeout 이후에 발생할 수 있는 타임아웃입니다. 클라이언트와 서버가 연결된 후, 서버는 데이터를 클라이언트에게 전송합니다. 이때 하나의 데이터 덩어리가 아니라 여러 개의 패킷 단위로 쪼개서 전송되는데, 각 패킷이 전송될 때의 시간 차이 제한을 Socket Timeout이라고 합니다. 

만약 서버가 일정 시간 내에 다음 패킷을 보내지 않으면, 클라이언트는 Socket Timeout을 발생시키고 연결을 종료할 수 있습니다.

**Read Timeout** <br>
Read Timeout은 클라이언트와 서버가 연결된 후, 특정 I/O 작업이 일정 시간 내에 완료되지 않으면 발생하는 타임아웃입니다. 클라이언트와 서버가 연결된 상태에서, 서버의 응답이 지연되거나 I/O 작업이 길어져 요청이 처리되지 않을 때 클라이언트는 연결을 끊습니다. 

Read Timeout은 이러한 상황을 방지하기 위해 설정된 타임아웃으로, 일정 시간 내에 데이터가 읽혀지지 않으면 클라이언트가 연결을 종료합니다.

## 🤷🏻‍♂️ 네트워크 통신에 타임아웃이 필요한 이유는 무엇인가요? 그리고 정말 필요한가요?

가상 서버를 띄우고 임의로 지연을 추가하여 타임아웃을 테스트할 수 있습니다. 하지만, 테스트 환경을 구축하기 위한 시간이 들며 자동화된 테스트에 지연 시간이 추가되는 것이 단점입니다. 

타임아웃 설정을 테스트하여 얻을 수 있는 것과 테스트를 하기 위해서 잃어야 하는 것을 신중히 고려하여 필요성을 따지는 것이 중요하다고 생각합니다.