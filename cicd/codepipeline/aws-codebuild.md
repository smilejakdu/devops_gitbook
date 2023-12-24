# AWS CodeBuild 프로젝트 설정 내에 빌드 명령 포함



위는 프로젝트 파일에 buildspec.yml 이 없을것이다.&#x20;

그러면 buildspec.yml 이 어디에 있을까 ?

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-21 오후 9.30.49.png" alt=""><figcaption></figcaption></figure>

여기에서 밑에 내리다보면 `Buildspec` 이 보일것이다.

말고도 환경변수에 보면 이름과 값이 나와있다.

만약에 root 디렉토리에

`appspec_template.yaml` 파일이 존재하고

```markdown
version: 0.0
Resources:
  - TargetService:
      Type: AWS::ECS::Service
      Properties:
        TaskDefinition: '$TASK_DEFINITION'
        LoadBalancerInfo:
          ContainerName: '$CONTAINER_NAME'
          ContainerPort: '$CONTAINER_PORT'


```

이렇게 작성돼 있다면 ,

&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-21 오후 9.39.03.png" alt=""><figcaption></figcaption></figure>

여기를 잘 살펴봐야한다.

post\_build 는 빌드가 성공적으로 완료된 후 실행되는 명령어들의 집합이다.

여기에는 도커 이미지를 ECR 에 푸시하고 , ECS 의 태스크 정의를 업데이트하며,&#x20;

`appspec.yaml` 파일을 생성하는 단계가 포함되어 있습니다.

**envsubst < appspec\_template.yaml > appspec.yaml**

에서 envsubst 명령은 환경 변수로 설정된 값을 appspec\_template.yaml 파일의 변수들에 대체하고, 결과를 appspec.yaml 으로 출력합니다.  appspec.yaml 파일은 CodeDeploy 에 의해 사용되며 ECS 서비스를 업데이트하는 데 필요한 정보를 담고 있습니다.\


* `artifact`\
  `files` 빌드 아티팩트로 `appspec.yaml` 과 `taskdef.json 파일을 지정합니다.`\
  `이것은 프로세스가 완료된 후 이 파일들을 CodePipeline 의 다음 단계로 전달 할 때 사용됩니다. ( 매우 중요` :thumbsup:)

이과정을 통해 AWS CodeBuild 는 소스 코드를 빌드하고, 도커 이미지를 ECR 에 푸시하며, ECS 태스크 정의를 업데이트하고 , CodeDeploy 가 사용할 `appspec.yaml` 파일을 생성하여, 이 모든것을 CodePipeline 의 다음단계로 넘기는 역할을 합니다.\
\
다음단계는 CodeDeploy 로 넘어가게 됩니다.

* 빌드 ( CodeBuild ) : 소스 단계에서 받은 코드를 CodeBuild 가 빌드합니다. 여기서 Docker 이미지를 생성하고, 필요한 설정 파일들을 생성합니다.
* 배포( Deploy ) : CodeBuild 단계에서 생성된 아티팩트 (예를 들어 appspec.yaml 및 taskdef.json) 는 CodeDeploy 로 전달되어 배포 프로세스를 실행합니다. CodeDeploy 는 이 파일들을 사용하여 ECS 서비스를 업데이트 하거나 EC2 인스턴스에 새로운 애플리케이션 버전을 배포합니다.
