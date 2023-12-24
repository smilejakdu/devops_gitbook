# CodePipeline

CICD 적용하는 툴은 많다.  지금은 다른 툴은 사용하지 않고 AWS 에서 제공하고 있는 CodePipeline 을 사용하도록 하자.

Git push를 통해 AWS CodePipeline CI/CD 프로세스를 트리거하는 경우, `buildspec.yml` 파일의 존재 여부는 선택 사항입니다. AWS CodePipeline과 CodeBuild를 사용하여 CI/CD 파이프라인을 구성할 때, `buildspec.yml` 파일은 두 가지 방식으로 사용될 수 있습니다:

1. **소스 저장소 내에 `buildspec.yml` 파일 포함**:
   * 이 방법에서는 프로젝트의 루트 디렉토리에 `buildspec.yml` 파일을 포함시킵니다.
   * CodeBuild 프로젝트가 시작될 때, 이 파일이 자동으로 감지되어 빌드 명령을 실행하는 데 사용됩니다.
   * 이 방식의 장점은 `buildspec.yml` 파일이 프로젝트와 함께 버전 관리될 수 있다는 것입니다. 따라서 빌드 프로세스를 프로젝트의 특정 상태에 맞춰 쉽게 관리할 수 있습니다.
2. **AWS CodeBuild 프로젝트 설정 내에 빌드 명령 포함**:
   * CodeBuild 프로젝트 설정에서 직접 빌드 명령을 정의할 수 있습니다. 이 경우, `buildspec.yml` 파일은 소스 코드 저장소에 포함되지 않아도 됩니다.
   * AWS CodeBuild의 콘솔 또는 AWS CLI를 사용하여 빌드 명령을 설정할 수 있습니다.
   * 이 방식은 `buildspec.yml` 파일을 프로젝트와 분리하고 싶을 때 유용할 수 있습니다.

따라서 `buildspec.yml` 파일은 필수적이지 않으며, 프로젝트 요구 사항과 팀의 작업 방식에 따라 선택할 수 있습니다. 프로젝트에 포함시키면 빌드 프로세스가 프로젝트의 소스 코드와 밀접하게 연관되고, 프로젝트 설정 내에 정의하면 빌드 프로세스를 중앙에서 관리할 수 있게 됩니다.

AWS CodePipeline은 `buildspec.yml` 파일의 존재 여부에 관계없이 작동할 수 있으며, 주로 소스 코드 저장소에서 변경 사항이 발생했을 때 해당 변경 사항을 감지하고, 이를 트리거로 하여 CodeBuild, CodeDeploy 등의 서비스를 통해 CI/CD 파이프라인을 진행합니다.
