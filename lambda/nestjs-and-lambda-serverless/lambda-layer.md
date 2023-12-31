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



## Layer/Nodejs

Layer 를 만들때 nodejs 폴더안에 모듈들을 만들어야 합니다.

그후에 `serverless.yml` 파일이 위치한 곳에서 `sls deploy` 명령어를 입력하게되면 AWS Lambda layer 에 올라가게 됩니다.

`sls deploy` 명령어는 Serverless Framework를 사용하여 AWS Lambda와 관련된 자원(함수, Layer 등)을 배포할 때 사용하는 명령어입니다. 이 명령어는 프로젝트의 루트 디렉토리에서 실행해야 합니다. 프로젝트의 루트 디렉토리는 `serverless.yml` 파일이 위치한 곳입니다.

구조가 다음과 같다고 가정할 때:

```
/your-project-root
  /node-utils
    /nodejs
      /node_modules
        /aws-serverless-express
      package.json
  serverless.yml
```

여기서 `/your-project-root`는 프로젝트의 최상위 폴더이고, `serverless.yml` 파일이 이 위치에 있어야 합니다. `node-utils` 폴더는 Layer의 코드와 종속성을 포함하고 있습니다.

다음 단계를 따르세요:

1.  터미널을 열고 프로젝트의 루트 디렉토리로 이동합니다.

    ```
    cd /path/to/your-project-root
    ```
2.  프로젝트 루트에서 `sls deploy` 명령어를 실행합니다.

    ```
    sls deploy
    ```

이 명령을 실행하면 Serverless Framework가 `serverless.yml` 파일의 설정에 따라 AWS에 자원을 배포합니다. Layer의 경우 `node-utils` 디렉토리 내용이 Layer로 패키징되어 AWS Lambda에 업로드됩니다.

모든 설정이 올바르고 `serverless.yml` 파일이 올바르게 구성되어 있다면, `sls deploy` 명령은 해당 Layer를 포함하여 필요한 모든 AWS 자원을 배포할 것입니다.



그런데 불편한 사항이 있습니다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-01-01 오후 8.46.47.png" alt=""><figcaption></figcaption></figure>

`package.json` 파일과 `package-lock.json` 파일 과 node\_modules 파일 위치가 다릅니다.

package.json 파일이 있는곳에서 npm install 하게되면 ,&#x20;



```
nodejs/
node_modules/
  └── 여기에 필요한 npm 패키지들이 위치
package.json (선택 사항)

```

하지만 우리가 원하는것은 nodejs 폴더 안에 node\_modules 가 위치해야합니다

```markdown
nodejs/
└── node_modules/
    └── 여기에 필요한 npm 패키지들이 위치
package.json (선택 사항)

```

이렇게 위치해야합니다.

이럴경우 그럼 어떻게 해야할까요 ?



## nodejs 폴더로 node\_modules 이동

자동화를 위해, `npm install`이 실행된 후에 `node_modules` 디렉토리를 `nodejs` 폴더로 이동시키는 작업을 스크립트로 만들 수 있습니다. 이 스크립트는 `package.json` 파일에 사용자 정의 스크립트로 추가할 수 있으며, `npm` 명령으로 실행될 수 있습니다.

아래는 `package.json`에 추가할 수 있는 스크립트 예시입니다:

```json
"scripts": {
  "postinstall": "mv node_modules nodejs",
  "predeploy": "npm install && npm run postinstall",
  "deploy": "sls deploy"
}
```

이 스크립트들의 역할은 다음과 같습니다:

* `postinstall`: `npm install`이 실행된 직후에 자동으로 `node_modules` 디렉토리를 `nodejs` 디렉토리로 이동시킵니다.
* `predeploy`: 배포하기 전에 필요한 패키지를 설치하고 `postinstall` 스크립트를 실행합니다.
* `deploy`: Serverless Framework를 사용하여 배포를 실행합니다.

이제 터미널에서 다음과 같이 `npm run deploy`를 실행하면, `npm install`이 실행되고, 모듈들이 적절한 위치로 이동된 후, Serverless Framework를 통해 배포가 진행됩니다.

```bash
npm run predeploy
npm run deploy
```

이 스크립트를 사용하면 수동으로 디렉토리를 이동시키는 단계를 자동화할 수 있습니다. 이 과정은 `node-utils` 디렉토리에서 실행되어야 합니다.

또한, `package.json`의 `scripts` 섹션에 명령을 추가하기 전에, 현재 디렉토리가 `node-utils` 디렉토리인지 확인하세요. 이 스크립트는 `node-utils` 디렉토리 안에 `node_modules`가 생성되고, 이후 `nodejs`로 옮겨져야 하는 상황에 맞게 설정된 것입니다.

마지막으로, `sls deploy`는 Serverless Framework가 설치된 위치에서 실행되어야 하며, 모든 경로와 커맨드는 실행 환경에 따라서 조정해야 합니다.

`sls create --template aws-nodejs --path workerModules --name workerModules`

명령어를 통해 serverless.yml 을 만들어 질거에요

필요없는 handler.js 를 삭제해 줍니다.&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2024-01-02 오전 4.37.28.png" alt=""><figcaption></figcaption></figure>

package.json 파일은 layer 폴더의 제일 최상단에 둔다. 위의 package.json 파일은 전체 모듈들이 들어있다.

<figure><img src="../../.gitbook/assets/스크린샷 2024-01-02 오전 4.38.54.png" alt=""><figcaption></figcaption></figure>

commonModules 안 package.json 파일에는 공통으로 사용하는 모듈들을 모아둔다.

그리고 functionModules 는 함수에 가져다가 사용할 모듈들만 가져다가 사용하도록 한다.

`functionModules` 폴더안에 serverless.yml 파일을 작성합니다.

```yaml
service: functionModules
frameworkVersion: "3"

provider:
  name: aws
  runtime: nodejs18.x
  region: ap-northeast-2

layers:
  NodeFunctionUtils:
    path: node-utils
    description: "Node Function Utils"
    compatibleRuntimes:
      - nodejs18.x

```

package.json 파일은&#x20;

```json
{
  "name": "utils",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "postinstall": "mv node_modules nodejs",
    "predeploy": "npm install && npm run postinstall"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "@nestjs/swagger": "^7.1.17",
    "swagger-ui-express": "^5.0.0"
  }
}

```

이렇게 작성해줍니다.
