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



## Layer 분리시키기

Layer 를 분리시키면 위의 문제점이 해결 됩니다.



* 공통으로 사용하는 모듈을 layer 로 올린다.
* 각각 함수별로 사용하는 layer 를 올려둔다.

AWS Lambda에서 공통 Layer와 각 함수에 특화된 Layer를 함께 사용하려면, 각 Lambda 함수의 설정에서 이 Layer들을 명시적으로 참조해야 합니다. serverless.yml 파일을 사용하는 경우, 각 함수의 정의에 필요한 Layer들의 ARN을 나열하여 이를 구성할 수 있습니다.

다음은 `serverless.yml`에서 공통 Layer와 각 함수에 특화된 Layer를 함께 사용하는 방법의 예시입니다:

```yaml
service: my-service

provider:
  name: aws
  runtime: nodejs18.x

functions:
  functionOne:
    handler: handler.functionOne
    layers:
      - {Common Layer ARN}      # 공통 Layer
      - {FunctionOne Specific Layer ARN}  # functionOne에 특화된 Layer

  functionTwo:
    handler: handler.functionTwo
    layers:
      - {Common Layer ARN}      # 공통 Layer
      - {FunctionTwo Specific Layer ARN}  # functionTwo에 특화된 Layer
```

이 설정에서:

* 각 함수(`functionOne`, `functionTwo`)는 두 개의 Layer를 참조합니다.
* `{Common Layer ARN}`는 모든 함수에서 공통으로 사용되는 Layer의 ARN입니다.
* `{FunctionOne Specific Layer ARN}`과 `{FunctionTwo Specific Layer ARN}`는 각각 `functionOne`과 `functionTwo`에 특화된 Layer의 ARN입니다.

실제로 이 설정을 사용할 때는 `{Common Layer ARN}`, `{FunctionOne Specific Layer ARN}`, `{FunctionTwo Specific Layer ARN}`를 해당하는 실제 Layer의 ARN으로 대체해야 합니다.

이 방식을 통해 각 Lambda 함수가 공통적으로 사용하는 코드나 라이브러리를 공유하는 동시에, 각 함수의 특정 요구 사항을 만족시키는 Layer를 별도로 관리할 수 있습니다. 이는 코드 중복을 줄이고, 배포 패키지의 크기를 최적화하는 데 도움이 됩니다.
