# Lambda serverless 배포

{% embed url="https://medium.com/@ritikparikh98/deploying-node-js-functions-to-aws-lambda-serverless-d0143e0d15c8" %}

위의 블로그 내용을 그대로 따라해도 된다.

```javascript
sudo npm install -g serverless
mkdir lambda_test_node
serverless create --template aws-nodejs
```

<figure><img src="../.gitbook/assets/스크린샷 2023-12-26 오전 1.04.08.png" alt=""><figcaption></figcaption></figure>

이렇게 생성이 된다.&#x20;

handler.js 파일을 다음과 같이 수정해줍니다.

```javascript
module.exports.handlerFunction = async (event, context) => {
    console.log("I am inside aws lambda function");
    return {
        statusCode: 200,
        body: JSON.stringify({ message: "Alright, It is working test!" }),
    };
};

```

serverless.yml 파일을 다음과 같이 수정해줍니다.

```javascript
service: lambda-test-node
frameworkVersion: "3"

provider:
  name: aws
  runtime: nodejs18.x
  region: ap-northeast-2 # Seoul
  apiGateway:
    shouldStartNameWithService: true
    minimumCompressionSize: 1024

functions:
  hello:
    handler: handler.handlerFunction
    events:
      - http:
          path: /api/hello
          method: get
          cors: true

```

이후 `serverless deploy` 명령어를 입력해서 배포를 해줍니다.&#x20;

