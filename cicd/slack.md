# Slack 연동

slack 과 aws 연동

slack 에서 aws 를 추가했는지 확인한다.

slack 에서 aws 추가를 했으면,&#x20;

aws -> CodePipeline -> 알림 을 클릭한다.

<figure><img src="../.gitbook/assets/스크린샷 2023-12-18 오전 10.42.58.png" alt=""><figcaption></figcaption></figure>

## :white\_check\_mark: AWS 설정&#x20;

알림 규칙을 생성한다.

<figure><img src="../.gitbook/assets/스크린샷 2023-12-18 오전 10.45.23.png" alt=""><figcaption></figcaption></figure>

noti 하고 싶은곳을 체크한다.\


<figure><img src="../.gitbook/assets/스크린샷 2023-12-18 오전 10.52.40.png" alt=""><figcaption></figcaption></figure>

하고 submit 을 누르면 끝 !&#x20;

## :white\_check\_mark: 에러



The notification rule could not be created because the service-linked role for AWS CodeStar Notifications is not currently available. This might have been caused by another user deleting the role at the same time you created the notification rule. Wait a few minutes, and then try again. The service-linked role will be recreated when you create the rule.



위와 같이 에러가 발생한다면 조금 기다렸다가 다시 시도해 보도록 하자 .



<figure><img src="../.gitbook/assets/스크린샷 2023-12-18 오후 6.15.03.png" alt=""><figcaption></figcaption></figure>

그러면 위와 같이 되는것을 확인 할 수 있다.

