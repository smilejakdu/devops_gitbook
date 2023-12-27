# Nestjs & Lambda Serverless

{% embed url="https://docs.nestjs.com/faq/serverless" %}

{% embed url="https://www.serverless.com/framework/docs/providers/aws/events/apigateway" %}

nest js 공식문서와 serverless 공식문서를 반드시 참고하는것이 좋다.



우선 위의 공식문서를 정독 3번정도 하는것을 추천합니다.



```javascript
 npm install -g @nestjs/cli
```

## 셋팅

```javascript
npm i @vendia/serverless-express aws-lambda
npm i -D @types/aws-lambda serverless-offline
```

이후  `main.ts` 파일을 수정합니다.

```typescript
import { NestFactory } from '@nestjs/core';
import serverlessExpress from '@vendia/serverless-express';
import { Callback, Context, Handler } from 'aws-lambda';
import { AppModule } from './app.module';

let server: Handler;

async function bootstrap(): Promise<Handler> {
  const app = await NestFactory.create(AppModule);
  await app.init();

  const expressApp = app.getHttpAdapter().getInstance();
  return serverlessExpress({ app: expressApp });
}

export const handler: Handler = async (
  event: any,
  context: Context,
  callback: Callback,
) => {
  server = server ?? (await bootstrap());
  return server(event, context, callback);
};
```



이후 tsconfig.json 파일을 수정합니다.

```typescript

{
  "compilerOptions": {
    ...
    "esModuleInterop": true
  }
}

```

serverless.yml 파일을 수정해 줍니다&#x20;

필요한 옵션이 있다면 공식문서를 참고해서 추가 삭제하면 될것 같습니다.



```yaml
service: serverless-lambda-api
frameworkVersion: "3"

plugins:
    - serverless-offline
    - serverless-plugin-optimize
    - serverless-vpc-plugin
    - serverless-offline-scheduler


provider:
  name: aws
  runtime: nodejs18.x
  memorySize: 1024
  timeout: 30
  region: ap-northeast-2 # Seoul
  apiGateway:
    shouldStartNameWithService: true
    minimumCompressionSize: 1024
    binaryMediaTypes:
      - '*/*'
  iam:
    role:
      statements:
        - Effect: "Allow"
          Action:
            - "s3:PutObject"
            - "s3:PutObjectAcl"
          Resource:
            - "arn:aws:s3:::serverless-lambda-api/*"

functions:
  app:
    handler: dist/lambda.handler
    timeout: 30
    events:
      - http: "ANY /{proxy+}"
      - http: "GET /"
      - http:
          path: api/{proxy+}
          method: any
  # Worker
  consultingNotifier:
    handler: dist/worker/consulting_notifier.handler
    timeout: 900
    events:
      - schedule: cron(* * * * ? *)

custom:
  serverless-offline:
    noPrependStageInUrl: true  # 스테이지 이름을 URL에 추가하지 않도록 설정
    httpPort: 5504
    prefix: ''
    babelOptions:
      presets: ["env"]
  optimize:
    external: ['swagger-ui-dist']
```

작성하고 나서 ,&#x20;

main.ts 파일은

```typescript
import { NestFactory } from '@nestjs/core';
import serverlessExpress from '@vendia/serverless-express';
import { Callback, Context, Handler } from 'aws-lambda';
import { AppModule } from './app.module';

let server: Handler;

async function bootstrap(): Promise<Handler> {
  const app = await NestFactory.create(AppModule);
  app.setGlobalPrefix('api');
  await app.listen(3000);

  const expressApp = app.getHttpAdapter().getInstance();
  return serverlessExpress({ app: expressApp });
}

export const handler: Handler = async (
    event: any,
    context: Context,
    callback: Callback,
) => {
  server = server ?? (await bootstrap());
  return server(event, context, callback);
};
```

작성해주고 난후 npx serverless offline -> http://localhost:3000/dev/api 로 접속을 해줍니다.

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-26 오전 8.01.29.png" alt=""><figcaption></figcaption></figure>

동작이 잘되는것을 확인했으면 aws lambda 에 배포를 해줍니다.

```typescript
 serverless deploy
```

또는&#x20;

```typescript
sls deploy
```

라고 입력해도 된다.

{% embed url="https://velog.io/@m16khb/NestJs-Lambda-Serverless" %}

위의 링크를 참고할것&#x20;



## 에러 상황

#### Swagger Error



```markdown
Errors
Hide
 
Resolver error at paths./api/app.get.responses.200.content.application/json.schema.$ref
Could not resolve reference: Could not resolve pointer: /components/schemas/ does not exist in document
```

위와 같은 에러가 발생했을때,&#x20;

위의 에러가 발생했다면 내가 뭔가 Swagger 문서를 잘못 적용했는지 살펴본다.



