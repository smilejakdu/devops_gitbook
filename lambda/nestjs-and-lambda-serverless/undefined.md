---
description: 정
---

# 환경 변수 설정

lambda 를 사용하게 될때, 환경변수가 필요하다

환경변수 설정하는 여러 방법이 있는데 하나씩 알아보면 좋을것 같습니다.



## config 설정 방법

`mkdir config && config.dev.json` 으로 config.dev.json 파일을 생성해 줍니다.&#x20;

config.dev.json 파일안에는 환경변수 키 와 값을 넣어주도록 한다.

```typescript
{
  "MASTER_DB_HOST": "",
  "MASTER_DB_USERNAME": "",
  "MASTER_DB_PASSWORD": "",
  "MASTER_DB_PORT": "3306",
  "SLAVES_DB_HOST": "",
  "SLAVES_DB_USERNAME": "",
  "SLAVES_DB_PASSWORD": "",
  "SLAVES_DB_PORT": "3306",
  "COMMERCE_DB": "",
  "USER_DB": "user",
  "AUTH_NAVER_CLIENT_ID": "UdbNiYnoEmha0fVQe1PL",
  "AUTH_NAVER_SECRET": "hqnC7031JS",
  "JWT_SECRET": "f9$jfK1@zP9",
  "AUTH_KAKAO_CLIENT_ID": "3b47ea13fd84bd2da6a8f92ccd3b361e",
  "SERVER_URL": "https://api.dev.project.co.kr",
  "SHOP_CLIENT_URL": "https://dev-shop.project.co.kr",
  "IAMPORT_KEY": "",
  "IAMPORT_SECRET": "",
  "INFOBANK_ID": "socialclub",
  "INFOBANK_PASSWORD": "",
  "INFOBANK_REST_ID": "",
  "INFOBANK_REST_PASSWORD": "",
  "VPC": {
    "securityGroupIds": ["sg-", "sg-"],
    "subnetIds": ["subnet-", "subnet-", "subnet-"]
  }
}

```

이런식으로 설정을 해준다.

이후 `serverless.yml` 파일 셋팅을 해주면 된다.

vpc 와 subnet 셋팅은 database 가 private subnet 에 존재하기 때문에 접근하기 위해선 반드시 필요한 설정이다.

