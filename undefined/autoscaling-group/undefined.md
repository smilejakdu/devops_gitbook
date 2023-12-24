# 오토 스케일링 그룹 개요

## Autoscaling Group



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/d15192b369944f8ea5c434055ec1a74d/ef6e3bf5-2100-4916-a7c1-26f121ea0efd.png" alt=""><figcaption></figcaption></figure>



오토스케일링은 자동으로 EC2 인스턴스에 개수가 늘었다가 줄었다가 할 수 있는 기능을 말합니다.

## Launch Template 와 Golden AMI

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/d15192b369944f8ea5c434055ec1a74d/84397ee3-6147-40d6-b7dd-93b2468e7e92.png" alt=""><figcaption></figcaption></figure>

Launch template 은 인스턴스를 생성할때 설정하는 network 정보나 인스턴스 타입 또는 키페어 등 설정값들을 미리설정하게 해준다.

오토스케일링 그룹을 생성할때 해당 런치 템플릿을 사용해서 인스턴스를 생성할 수 있도록 구성 할 수 있습니다. 일반적으로 여기에 사용되는 가상머신 이미지를 golden ami 라고 한다.

골든 이미지는 os 영역을 포함해서 필수 패키지가 설치된 표준 이미지를 말합니다.

AWS 에서는 가상 이미지를 AMI 라고 하는데요.

아마존 머신 이미지라고 해서 AMI 라고 합니다.

## Autoscaling group 의 policy

AWS(Amazon Web Services)에서 제공하는 오토스케일링 그룹의 정책에는 세 가지 유형이 있습니다: 단순 조정 정책(Simple Scaling Policies), 대상 추적 조정 정책(Target Tracking Scaling Policies), 그리고 단계 조정 정책(Step Scaling Policies). 각각의 특징과 차이점에 대해 설명하겠습니다.



### 단순 조정 정책 (Simple Scaling Policies)

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/92ff88d900a343c4aac838883ce8b002/8ef723f3-477a-435b-821c-7628e1f4022c.png" alt=""><figcaption></figcaption></figure>

**단순 조정 정책 (Simple Scaling Policies)**

* 단순 조정 정책은 가장 기본적인 오토스케일링 정책입니다.
* 이 정책은 CloudWatch 알람을 기반으로 동작합니다. 예를 들어, CPU 사용률이 설정된 임계값을 초과하면 인스턴스를 추가합니다.
* 조정 이벤트는 연속적으로 발생하지 않도록 '쿨다운' 기간을 설정할 수 있습니다. 쿨다운 기간 동안은 추가적인 조정 활동이 일어나지 않습니다.
* 이 정책은 간단하고 직관적이지만, 더 복잡한 조정 요구 사항을 충족시키기에는 제한적일 수 있습니다.

**대상 추적 조정 정책 (Target Tracking Scaling Policies)**

* 대상 추적 조정 정책은 좀 더 고급 기능을 제공합니다.
* 이 정책은 특정 지표(예: CPU 사용률)를 설정된 목표값(예: 50% 사용률)에 가깝게 유지하기 위해 자동으로 조정합니다.
* 이 정책은 더 세밀하고 지능적인 조정이 가능하여, 리소스 사용의 효율성을 극대화할 수 있습니다.
* 예를 들어, 트래픽이 증가하여 CPU 사용률이 목표치를 초과하면 자동으로 인스턴스를 추가하여 목표치에 가깝게 조절합니다.



위의 정책보다 업그레이드 버전이 있습니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/92ff88d900a343c4aac838883ce8b002/c4786dbe-14ac-4a6b-bb92-aecdbed6a176.png" alt=""><figcaption></figcaption></figure>

**단계 조정 정책 (Step Scaling Policies)**

* 단계 조정 정책은 더 복잡한 조정 요구 사항에 적합합니다.
* 이 정책은 여러 단계의 조정 규칙을 설정할 수 있으며, 각 단계는 다른 조정 행동을 정의합니다.
* 예를 들어, CPU 사용률이 70%를 초과하면 2개의 인스턴스를 추가하고, 80%를 초과하면 4개의 인스턴스를 추가하는 식으로 더 세분화된 조정이 가능합니다.
* 이 정책은 더 복잡한 환경에서의 세밀한 리소스 관리를 가능하게 합니다.



물론 Fargate 에서도 오토스케일링이 가능하다.

1. **ECS(Elastic Container Service) 서비스 사용:** Fargate는 ECS와 함께 사용됩니다. 따라서, ECS 서비스 정의를 생성하고 Fargate를 실행 유형으로 선택합니다.
2. **CloudWatch 알람 설정:** 오토스케일링을 위해 필요한 메트릭스(예: CPU 사용률, 메모리 사용률)에 대한 CloudWatch 알람을 설정합니다. 이 알람은 스케일링 정책을 트리거하는 데 사용됩니다.
3. **오토스케일링 정책 생성:** ECS 서비스에 대한 오토스케일링 정책을 생성합니다. 이 정책은 CloudWatch 알람에 응답하여 컨테이너의 수를 자동으로 늘리거나 줄입니다.
4. **타겟 트래킹 스케일링 정책 활용:** Fargate에서는 타겟 트래킹 스케일링 정책을 사용하여 특정 메트릭스의 목표값을 유지하도록 할 수 있습니다. 예를 들어, 평균 CPU 사용률을 일정 수준으로 유지하도록 설정할 수 있습니다.
5. **조정 테스트 및 모니터링:** 설정한 오토스케일링 정책이 예상대로 작동하는지 테스트하고, 필요에 따라 조정합니다.

즉, 메트릭스( CPU 사용률, 메모리 사용률 ) 에 클라우드와치를 연결시켜서 클라우드와치가 알람을 주면 오토스케일링이 발동하는형식이 맞나요 ?
