# Table of contents

* [devops\_gitbook](README.md)
* [✅ Docker](docker/README.md)
  * [docker 삭제](docker/docker.md)
  * [doker 중단](docker/doker.md)
* [✅ CICD](cicd/README.md)
  * [Slack 연동](cicd/slack.md)
  * [CodePipeline](cicd/codepipeline/README.md)
    * [소스 저장소 내에 buildspec.yml 파일 포함](cicd/codepipeline/buildspec.yml.md)
    * [AWS CodeBuild 프로젝트 설정 내에 빌드 명령 포함](cicd/codepipeline/aws-codebuild.md)
* [✅ ECR ECS](ecr-ecs/README.md)
  * [📌 ECR](ecr-ecs/ecr.md)
  * [📌 ECS](ecr-ecs/ecs/README.md)
    * [EC2](ecr-ecs/ecs/ec2.md)
    * [Fargate](ecr-ecs/ecs/fargate/README.md)
      * [RDS 보안그룹 셋팅](ecr-ecs/ecs/fargate/rds.md)
      * [RDS 생성](ecr-ecs/ecs/fargate/rds-1.md)
      * [MySQL 접속 연결](ecr-ecs/ecs/fargate/mysql.md)
      * [운영 DB 연결 테스트](ecr-ecs/ecs/fargate/db.md)
      * [로드밸런싱](ecr-ecs/ecs/fargate/undefined/README.md)
        * [보안 그룹 생성](ecr-ecs/ecs/fargate/undefined/undefined.md)
        * [대상 그룹 생성](ecr-ecs/ecs/fargate/undefined/undefined-1.md)
        * [로드밸런서 생성](ecr-ecs/ecs/fargate/undefined/undefined-2.md)
        * [백엔드 실행 & 프론트엔드 설정](ecr-ecs/ecs/fargate/undefined/and.md)
* [✅ 오토스케일링](undefined/README.md)
  * [스케일 업](undefined/undefined.md)
  * [스케일 아웃](undefined/undefined-1.md)
  * [스케일 인](undefined/undefined-2.md)
  * [Autoscaling Group](undefined/autoscaling-group/README.md)
    * [오토 스케일링 그룹 개요](undefined/autoscaling-group/undefined.md)
    * [오토 스케일링 그룹 실습하기](undefined/autoscaling-group/undefined-1.md)
    * [Fargate 오토스케일링](undefined/autoscaling-group/fargate.md)
* [Secret Manager](secret-manager.md)
* [Route53](route53/README.md)
  * [ALB 와 Route53 연결](route53/alb-route53.md)
  * [가비아 도메인 등록](route53/undefined.md)
* [CloudWatch](cloudwatch/README.md)
  * [CloudWatch 슬랙 알람](cloudwatch/cloudwatch.md)
* [✅ Lambda](lambda/README.md)
  * [Api Gateway](lambda/api-gateway.md)
  * [Lambda serverless 배포](lambda/lambda-serverless.md)
  * [Nestjs & Lambda Serverless](lambda/nestjs-and-lambda-serverless/README.md)
    * [worker](lambda/nestjs-and-lambda-serverless/worker.md)
    * [환경 변수 설정](lambda/nestjs-and-lambda-serverless/undefined.md)
    * [Lambda 용량 제한 Layer](lambda/nestjs-and-lambda-serverless/lambda-layer.md)
    * [Api Gateway & Route53](lambda/nestjs-and-lambda-serverless/api-gateway-and-route53.md)
* [FrontEnd Deploy](frontend-deploy/README.md)
  * [S3 를 이용한 배포](frontend-deploy/s3/README.md)
    * [개요](frontend-deploy/s3/undefined.md)
    * [S3](frontend-deploy/s3/s3.md)
    * [로드밸런서](frontend-deploy/s3/undefined-1.md)
* [AWS 크레딧](aws/README.md)
  * [Page 1](aws/page-1.md)
  * [Page 2](aws/page-2.md)
