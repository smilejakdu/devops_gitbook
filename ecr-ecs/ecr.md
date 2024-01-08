# 📌 ECR

ECR 은 간단히 말해서 이미지 저장소이다.

dockerhub 에 이미지를 저장해서 사용해도 되지만 dockerhub 는 public 한 공간이다

다른사람들도 주소를 알고 있다면 얼마든지 접근이 가능하다.

그래서 ECR 를 사용하는것이 보안상으로도 좋다.



## ECR 생성을 한다.

<figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오후 3.16.41.png" alt=""><figcaption></figcaption></figure>

생성을 해준다.

생성을 하게 되면 친절하게도 push 명령어를 제공해준다.

하지만 여기서 바로 push 를 하게 되면 `platform` 에러가 발생하게 된다.

그래서 `platform` 에러를 신경쓰면서 배포를 진행 해야한다.



## ECR 로그인

{% embed url="https://docs.aws.amazon.com/ko_kr/AmazonECR/latest/userguide/getting-started-cli.html" %}

aws ecr get-login-password --region region | docker login --username AWS --password-stdin aws\_account\_id.dkr.ecr.region.amazonaws.com



ex )&#x20;

aws ecr get-login-password --region ap-northeast-2 | docker login --username AWS --password-stdin 430745341910.dkr.ecr.ap-northeast-2.amazonaws.com



## ECR 이미지 build



docker 명령어를 이용해서 buidl 를 해야합니다.

os 때문에 `--platform` 이라는 옵션을 추가해서 명령어를 입력해야합니다.

{% embed url="https://docs.docker.com/engine/reference/commandline/buildx_build/" %}





<figure><img src="../.gitbook/assets/스크린샷 2024-01-06 오후 8.21.11.png" alt=""><figcaption></figcaption></figure>



ex )

docker buildx build --platform linux/amd64 --tag 975421137881.dkr.ecr.ap-northeast-2.amazonaws.com/nest/dev/nginx:latest -f ./compose/dev/nginx/Dockerfile . --push



## ECR 이미지 push

{% embed url="https://docs.aws.amazon.com/ko_kr/AmazonECR/latest/userguide/docker-push-ecr-image.html" %}

docker tag e9ae3c220b23 aws\_account\_id.dkr.ecr.us-west-2.amazonaws.com/my-repository:tag

docker push aws\_account\_id.dkr.ecr.us-west-2.amazonaws.com/my-repository:tag



docker build 할때 조심을 해야한다.

이후에 tag 와 push 는 위의 공식문서를 따라서 push 하시면 됩니다.





