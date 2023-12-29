# Lambda 용량 제한 Layer

Lambda 에서 배포하다보면 Layer 제한 에러가 발생하게 된다.

&#x20;

lambda serverless layer 배포 라고 검색하게 되면

많은 자료가 나온다.

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-28 오후 5.44.40.png" alt=""><figcaption></figcaption></figure>

{% embed url="https://docs.aws.amazon.com/ko_kr/lambda/latest/dg/chapter-layers.html" %}

위의 docs 를 반드시 한번은 읽어 주면 좋다. 또 안읽을거지 또&#x20;



Lambda 계층은 Lambda 함수와 함께 사용할 수 있는 라이브러리 및 기타 종속성을 패키징하는 편리한 방법을 제공합니다. 계층을 사용하면 업로드된 배포 아카이브의 크기가 줄어들고 코드를 더 빠르게 배포할 수 있습니다.

계층은 추가 코드 또는 데이터를 포함할 수 있는 .zip 파일 아카이브입니다. 계층에는 라이브러리, 사용자 정의 런타임, 데이터 또는 구성 파일이 포함될 수 있습니다. 계층은 코드 공유 및 책임 분리를 촉진하므로 비즈니스 로직 작성을 더 빠르게 반복 할 수 있습니다.



Layers는 람다 함수에서 사용하는 라이브러리 및 기타 종속성 패키징을 계층화 시켜 Lambda에 연결, 보다 빠른 배포 및 패키징을 공용으로 사용 할 수 있도록 하는 것이다.
