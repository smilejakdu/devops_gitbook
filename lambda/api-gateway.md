# Api Gateway

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

API Gateway는 API의 소비자, 즉 클라이언트가 백엔드 서비스의 데이터 비즈니스 로직 또는 기능에 액세스할 수 있게 해주는 게이트 역할을 한다.

백엔드의 HTTP 엔드포인트 역할을 제공하는 서비스라고 생각하면 된다.

람다는 함수의 역할을 수행한다.

실제로 해당 람다에 접근할 수 있도록 하기 위해서는 API Gateway 를 연결하여 엔드포인트를 만들어 줘야 한다.



그러면 클라이언트는 API Gateway 를 통해서 Lambda 함수를 호출 할 수 있다.

클라이언트가 GET /products HTTP 요청을 보내면, API Gateway 가 이것을 받아서 해당 path 에 매칭되는 람다 함수를 실행시켜 주는 방식으로 동작한다.



먼저 API Gateway 를 생성해줘야 한다.

{% embed url="https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vs-rest.html" %}

