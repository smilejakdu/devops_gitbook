# ECR

ECR 은 간단히 말해서 이미지 저장소이다.&#x20;

dockerhub 에 이미지를 저장해서 사용해도 되지만 dockerhub 는 public 한 공간이다

다른사람들도 주소를 알고 있다면 얼마든지 접근이 가능하다.

그래서 ECR 를 사용하는것이 보안상으로도 좋다.



## ECR 생성을 한다.

<figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오후 3.16.41.png" alt=""><figcaption></figcaption></figure>

생성을 해준다.

생성을 하게 되면 친절하게도 push 명령어를 제공해준다.

하지만 여기서 바로 push 를 하게 되면 `platform` 에러가 발생하게 된다.

그래서 `platform` 에러를 신경쓰면서 배포를 진행 해야한다.

