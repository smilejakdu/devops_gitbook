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

이후 serverless.yml 파일을 수정합니다.

```javascript
service: lambda-test-node
frameworkVersion: "3"

plugins:
    - serverless-offline
    - serverless-dotenv-plugin
    - serverless-plugin-optimize
    - serverless-offline-scheduler

provider:
  name: aws
  runtime: nodejs18.x
  region: ap-northeast-2 # Seoul
  apiGateway:
    shouldStartNameWithService: true
    minimumCompressionSize: 1024

functions:
  app:
    handler: dist/main.handler
    timeout: 30
    events:
      - http:
          method: ANY
          path: /
      - http:
          method: ANY
          path: /{proxy+}

```

위 처럼수정하고 나서 ,&#x20;

`main.ts` 파일을 수정합니다.

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



이후 application 을 빌드하고나서, 실행을 시켜줍니다.

```javascript
 npx serverless offline                                                                                                                                                                               ─╯

DOTENV: Could not find .env file.

Starting Offline at stage dev (ap-northeast-2)

Offline [http for lambda] listening on http://localhost:3002
Function names exposed for local invocation by aws-sdk:
           * app: lambda-test-node-dev-app

   ┌───────────────────────────────────────────────────────────────────────┐
   │                                                                       │
   │   ANY | http://localhost:3000/dev                                     │
   │   POST | http://localhost:3000/2015-03-31/functions/app/invocations   │
   │   ANY | http://localhost:3000/dev/{proxy*}                            │
   │   POST | http://localhost:3000/2015-03-31/functions/app/invocations   │
   │                                                                       │
   └───────────────────────────────────────────────────────────────────────┘

Server ready: http://localhost:3000 🚀

ANY /dev (λ: app)
[Nest] 81452  - 12/26/2023, 7:43:20 AM     LOG [NestFactory] Starting Nest application...
(λ: app) RequestId: ddf3878e-ff45-47e7-97be-4f45c6b3fecb  Duration: 207.88 ms  Billed Duration: 208 ms
[Nest] 81452  - 12/26/2023, 7:43:20 AM     LOG [InstanceLoader] AppModule dependencies initialized +4ms
[Nest] 81452  - 12/26/2023, 7:43:20 AM     LOG [RoutesResolver] AppController {/}: +4ms
[Nest] 81452  - 12/26/2023, 7:43:20 AM     LOG [RouterExplorer] Mapped {/, GET} route +1ms
[Nest] 81452  - 12/26/2023, 7:43:20 AM     LOG [NestApplication] Nest application successfully started +1ms


```



serverless.yml 파일은

```yaml
service: microprotect-lambda-api
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
            - "arn:aws:s3:::microprotect-lambda-api/*"

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

<figure><img src="../.gitbook/assets/스크린샷 2023-12-26 오전 8.01.29.png" alt=""><figcaption></figcaption></figure>

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



