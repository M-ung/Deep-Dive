# CORS

CORS(Cross Origin Resource Sharing)는 출처가 다른 곳의 리소스를 요청할 때 접근 권한을 부여하는 메커니즘입니다. 리소스를 주고받는 두 곳의 출처가 다르면 출처가 교차한다고 합니다. 이때 출처는 URL뿐만 아니라 프로토콜과 포트까지 포함됩니다. 

만약 클라이언트의 출처가 허용되지 않았다면 CORS 에러가 발생할 수 있습니다.

## 🤷🏻‍♂️ CORS는 왜 필요한가요?
과거에는 크로스 사이트 요청 위조(CSRF, Cross-Site Request Forgery) 문제가 있었습니다. 피해자의 브라우저에서 다른 애플리케이션으로 가짜 클라이언트 요청을 전송하는 공격입니다.

CSRF를 예방하기 위해 브라우저는 동일 출처 정책(SOP, same-origin policy)을 구현했습니다. SOP가 구현된 브라우저는 클라이언트와 동일한 출처의 리소스로만 요청을 보낼 수 있습니다.

하지만, SOP는 한계가 있습니다. 현대의 웹 애플리케이션은 다른 출처의 리소스를 사용하는 경우가 많기 때문입니다. 따라서, SOP를 확장한 CORS가 필요합니다.

## 🤷🏻‍♂️ CORS는 어떻게 작동할까요?
브라우저가 요청 메시지에 Origin 헤더와 응답 메시지의 Access-Control-Allow-Origin 헤더를 비교해서 CORS를 위반하는지 확인합니다. 이때, Origin에는 현재 요청하는 클라이언트의 출처(프로토콜, 도메인, 포트)가, Access-Control-Allow-Origin은 리소스 요청을 허용하는 출처가 작성됩니다.

이렇게 단순하게 요청하는 것을 Simple Request라고 합니다. Simple Request은 요청 메서드(GET, POST, HEAD), 수동으로 설정한 요청 헤더(Accept, Accept-Language, Content-Language, Content-Type, Range), Content-Type 헤더(application/x-www-form-urlencoded, multipart/form-data, text/plain)인 경우에만 해당합니다.

브라우저가 사전 요청을 보내는 경우도 있습니다. 이때 사전 요청을 Preflight Request라고 합니다. 브라우저가 본 요청을 보내기 이전, Preflight Request를 OPTIONS 메서드로 요청을 보내어 실제 요청이 안전한지 확인합니다.

Preflight Request는 추가로 Access-Control-Request-Method로 실 요청 메서드와, Access-Control-Request-Headers 헤더에 실 요청의 추가 헤더 목록을 담아서 보내야 합니다.

이에 대한 응답은 대응되는 Access-Control-Allow-Methods와 Access-Control-Headers를 보내야 하고, Preflight Request로 인한 추가 요청을 줄이기 위해 캐시 기간을 Access-Control-Max-Age에 담아서 보내야 합니다.

또한 인증된 요청을 사용하는 방식도 있는데요. 이를 Credential Request라고 합니다. 쿠키나 토큰과 같은 인증 정보를 포함한 요청은 더욱 안전하게 처리되어야 합니다. 이때 Credential Request를 수행합니다.

Credential Request를 요청하는 경우에는 서버에서는 Access-Control-Allow-Credentials를 true로 설정해야 하며 Access-Control-Allow-Origin에 와일드카드를 사용하지 못합니다.