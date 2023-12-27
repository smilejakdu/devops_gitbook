# worker

nest js lambda serverless 에서 worker 를 돌리는 방법은 조금 다르다.

기존 nest js 에서는 @Cron 데코레이터를 사용해서 스케쥴러를 돌렸지만



lambda serverless 에서 스케쥴러는 worker 를 사용해야 한다.



## worker 돌릴 파일설정

```typescript
import { Context } from 'aws-lambda';
import dayjs from 'dayjs';
import { DataSource } from 'typeorm';
import dotenv from 'dotenv';
const NODE_ENV = process.env.NODE_ENV;

if (NODE_ENV === 'local') {
  dotenv.config({ path: 'local.env' });
} else if (NODE_ENV === 'dev') {
  dotenv.config({ path: 'dev.env' });
} else if (NODE_ENV === 'prod') {
  dotenv.config({ path: 'prod.env' });
}

const dbDataSource = new DataSource({
  type: 'postgres',
  host: process.env.MAIN_DB_URI,
  port: Number(process.env.MAIN_DB_PORT),
  username: process.env.MAIN_DB_USER,
  password: process.env.MAIN_DB_PASSWORD,
  database: process.env.MAIN_DB_DATABASE,
  entities: [__dirname + '/entities/*.entity{.ts,.js}'],
});

export async function handler(event: any, context: Context) {
  const TIME_UNIT = 'minutes';
  const start = dayjs().startOf(TIME_UNIT);
  const end = dayjs().endOf(TIME_UNIT);
  console.log(start, end);
  console.log('consulting notifier start');
  await dbDataSource.initialize();
  const customerRepository = await dbDataSource.query(
    'select * from user where id = 4',
  );
  console.log('foundCustomer =>', customerRepository);
  return 'nts hello';
}

```

파일을 작성했으면 , 이제 serverless.yml 파일로 가서 ,

worker 설정을 해준다.

```typescript
service: project-lambda-api
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
            - "arn:aws:s3:::project-lambda-api/*"

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
    handler: dist/worker/consultingNotifier.handler
    timeout: 900
    events:
      - schedule: cron(* * * * ? *)

custom:
  serverless-offline:
    noPrependStageInUrl: true  # 스테이지 이름을 URL에 추가하지 않도록 설정
    httpPort: 8001
    prefix: ''
    babelOptions:
      presets: ["env"]
  optimize:
    external: ['swagger-ui-dist']
```



## worker cron 설정

AWS Lambda 함수는 매 분마다 실행됩니다. 여기서 사용된 cron 표현식 `cron(* * * * ? *)`의 의미는 다음과 같습니다:

* 첫 번째 `*` : 분 (매 분)
* 두 번째 `*` : 시간 (매 시간)
* 세 번째 `*` : 일 (매월의 모든 날)
* 네 번째 `*` : 월 (매월)
* 다섯 번째 `?` : 요일 (특정 요일 없음)
* 여섯 번째 `*` : 연도 (매년)

이 cron 표현식은 매 시간의 모든 분(즉, 매 분)마다 Lambda 함수를 실행하도록 합니다. 각 `*`는 해당 필드의 모든 가능한 값에 대해 일치한다는 의미입니다. 따라서, 이 표현식은 매 시간, 매 일, 매월, 매년의 매 분마다 함수를 실행하라는 의미입니다.

정리하자면, 이 설정은 함수를 몇 초마다 실행하는 것이 아니라 정확히 매 분마다 실행하도록 설정하는 것입니다. AWS의 cron 스케줄링은 최소 단위가 1분이므로, 초 단위로 실행을 설정하는 것은 불가능합니다.
