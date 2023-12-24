# Secret Manager

secret manager 를 사용해서 key value 를 관리할 수 있다.

`.env` 같은 파일에서 관리 해도 되지만 조금 더 보안을 신경쓴다면 secrets manaager 를 사용 할 수 있다.



![](<.gitbook/assets/스크린샷 2023-12-20 오전 11.03.48.png>)

들어오고 난뒤에 오른쪽에 `보안 암호 값 검색` 을 클릭해준다.



<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오전 10.59.00.png" alt=""><figcaption></figcaption></figure>

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오전 10.59.21.png" alt=""><figcaption></figcaption></figure>

그러면 key value 값들이 들어있다.&#x20;

## 적용방법

key value 값들을 저장했으면 위의 키값들을 어디다가 가져다 사용해야한다.

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오전 11.06.36.png" alt=""><figcaption></figcaption></figure>

{% embed url="https://awscloudsecvirtualevent.com/workshops/module4/fargate/" %}

AWS 에서는 친절하게도 공식문서까지 제공을 해준다.

{% embed url="https://docs.aws.amazon.com/ko_kr/AmazonECS/latest/developerguide/secrets-envvar-secrets-manager.html" %}

위의 공식문서에서도 나오지만,

ecs 배포를 할때 작업정의서를 작성해야합니다.



```markdown
{
  "containerDefinitions": [{
    "secrets": [{
      "name": "environment_variable_name",
      "valueFrom": "arn:aws:secretsmanager:region:aws_account_id:secret:secret_name-AbCdEf"
    }]
  }]
}
```

이렇게 설정하면 됩니다.



만약 위처럼 secrets 가 없을경우에는 파이프라인단에서 가져올 확률이 높습니다.

```markdown
version: 0.2

env:
  secrets-manager:
    SECRET_VALUE: ${secret_manager_arn}

phases:
  install:
    commands:
      - apt install jq
  pre_build:
    commands:
      - echo Logging in to Amazon ECR...
      - $(aws ecr get-login --region ap-northeast-2 --no-include-email)
      - IMAGE_TAG=$(echo $CODEBUILD_RESOLVED_SOURCE_VERSION | cut -c 1-7)
  build:
    commands:
      - echo Build started on `date`
      - echo Building the Docker image...
      - $(echo $SECRET_VALUE | jq -r 'to_entries|map("\(.key)=\(.value)")|.[]' > .env)
      - docker build -t $REPOSITORY_URI:latest .
      - docker tag $REPOSITORY_URI:latest $REPOSITORY_URI:$IMAGE_TAG
  post_build:
    commands:
      - echo Build completed on `date`
      - echo Pushing the Docker images...
      - docker push $REPOSITORY_URI:latest
      - docker push $REPOSITORY_URI:$IMAGE_TAG
      - echo Writing image definitions file...
      - aws ecs describe-task-definition --task-definition $TASK_NAME | jq '.taskDefinition' > taskdef.json
      - envsubst < appspec_template.yaml > appspec.yaml
artifacts:
  files:
    - appspec.yaml
    - taskdef.json

```

위의 빌드스펙을 보면 ,

#### 1. `apt install jq`

이 명령어는 `install` 단계에서 사용되며, `jq`라는 명령줄 도구를 설치하는 데 사용됩니다. `jq`는 JSON 데이터를 처리하는 데 매우 유용한 도구로, JSON 데이터를 파싱하고, 변형하고, 필터링하는 데 사용됩니다. `buildspec.yml` 파일에서 `jq`는 AWS Secrets Manager에서 가져온 JSON 형식의 비밀 값을 처리하는 데 필요합니다.

#### 2. `$(echo $SECRET_VALUE | jq -r 'to_entries|map("\(.key)=\(.value)")|.[]' > .env)`

이 명령어는 `build` 단계에서 사용되며, 여러 작업을 수행합니다:

* **`echo $SECRET_VALUE`**: AWS Secrets Manager에서 가져온 비밀 값을 출력합니다. 이 값은 JSON 형식일 가능성이 높습니다.
* **`| jq -r 'to_entries|map("\(.key)=\(.value)")|.[]'`**: `jq`를 사용하여 JSON 데이터를 처리합니다. 이 파이프라인은 JSON 객체를 키-값 쌍으로 변환하여 각 키-값 쌍을 `KEY=VALUE` 형태로 변환합니다. 여기서 `-r` 옵션은 raw 문자열 출력을 의미합니다, 즉, 출력된 데이터에서 따옴표를 제거합니다.
* **`> .env`**: 생성된 키-값 쌍을 `.env` 파일에 리디렉션하여 저장합니다. `.env` 파일은 일반적으로 환경 변수를 저장하는 데 사용되며, 이 경우 Docker 빌드 과정에서 환경 변수로 사용될 수 있습니다.

하지만 위에 보면 $SECRET\_VALUE 는 또 어디서 가져오는걸까??&#x20;

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오후 11.29.59.png" alt=""><figcaption></figcaption></figure>

AWS 에서 CodePipeline 으로 가서 프로젝트빌드로 들어간다.

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오후 11.31.05.png" alt=""><figcaption></figcaption></figure>

빌드 세부 정보에 들어가본다.

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오후 11.34.57.png" alt=""><figcaption></figcaption></figure>

위의 권한을 보면 ,&#x20;

iam -> codebuild\_role -> codebuild\_role\_policy

```markdown
{
	"Version": "2012-10-17",
	"Statement": [
		{
			"Action": [
				"ecs:DescribeTaskDefinition",
				"secretsmanager:GetSecretValue",
				"ssm:GetParameters"
			],
			"Effect": "Allow",
			"Resource": "*"
		}
	]
}
```

와 같이 나와있다.

그리고 더 밑에 내려보면 Buildspec 에 `SECRET_VALUE` 가 작성돼 있는것을 볼 수 있다.

<figure><img src=".gitbook/assets/스크린샷 2023-12-20 오후 11.34.09.png" alt=""><figcaption></figcaption></figure>
