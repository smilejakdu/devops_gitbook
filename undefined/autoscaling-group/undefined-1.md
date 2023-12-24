# 오토 스케일링 그룹 실습하기

## 오토스케일링 그룹 실습



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/1ed18438-96c5-4e87-bf94-09370fde799b.png" alt=""><figcaption></figcaption></figure>

## VPC 확인하기

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/b19ebe14-de89-44a7-a42a-f55bca3d08bd.png" alt=""><figcaption></figcaption></figure>



위처럼 작업이 되어있다고 가정을 한다.

만약 위처럼 셋팅이 돼있지 않다면 셋팅을 먼저 하는것도 좋다.

아니면 이전강의를 듣고와도 좋을것 같다.

## 보안그룹 생성하기

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/c19ef1e2-4151-4c74-819b-b4a33e456026.png" alt=""><figcaption></figcaption></figure>



vpc 는 우리가 생성한 vpc 로 설정한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/1ff5a90a-fba2-4646-b9ee-2c7a15f03447.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/22b54912-ece9-41b3-adb1-d90a5004aa81.png" alt=""><figcaption></figcaption></figure>



이후 보안그룹 생성을 클릭한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/b9726236-a71f-4574-9241-02f68943db92.png" alt=""><figcaption></figcaption></figure>



그리고 보안그룹을 하나 더 생성해본다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/2478917c-e617-4d3d-b090-1d5d36ee6b62.png" alt=""><figcaption></figcaption></figure>

그리고 두번째 보안그룹에서는 22 port 를 설정합니다.

22port 로 들어올땐 open vpn 으로 들어 올 수 있게 설정을 해준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/510817e9-9b35-4f25-946f-00d0ba79e5ca.png" alt=""><figcaption></figcaption></figure>

80 port 도 open vpn 으로 들어 올 수 있게 설정을 해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/7b928f82-947c-4206-9d44-d9aa0d2e45bd.png" alt=""><figcaption></figcaption></figure>



또 다른 80 에는 아까 만든 alb를 선택해준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/57846603-ef1a-42f4-af42-3c4677d8f6ba.png" alt=""><figcaption></figcaption></figure>



그리고 보안그룹 생성을 클릭한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/11bb0889-cc5e-42c9-8904-127deba21269.png" alt=""><figcaption></figcaption></figure>

생성이 완료가 됐고 vpc 를 복사해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/6108ec4b-17c5-44d2-ae10-41717ad37c52.png" alt=""><figcaption></figcaption></figure>

같은 vpc 에 있는 보안그룹을 확인을 해보면

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/86b21eca-ddd8-49e9-a11f-da898c2c48fd.png" alt=""><figcaption></figcaption></figure>

우리가 방금 만든 보안그룹 2개가 보이게 된다.

my-asg-alb-sg, my-asg-ec2-sg

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/337db312-0203-4441-8e1d-1b68670ac81e.png" alt=""><figcaption></figcaption></figure>

## EC2 를 생성하여 AMI 이미지 만들기

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/72e5821c-7870-4fa3-bbb8-0936c063860b.png" alt=""><figcaption></figcaption></figure>

이미지는 amazon linux 를 그대로 사용하고 인스턴스 유형도 t2.micro 를 사용하도록 하자.

key pair 는 그전 수업시간에 생성한 key pair 를 선택해준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/61e5a3af-409e-4cc0-a41d-f8e7d2a4ef57.png" alt=""><figcaption></figcaption></figure>

네트워크 설정에서 편집을 클릭하고

vpc → my-vpc

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/9572d6a5-4f12-4fff-a78d-91ec00d2598a.png" alt=""><figcaption></figcaption></figure>

보안그룹은 우리가 만들어 놓았던 보안그룹을 선택한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/4be52339-679c-45fa-ac59-b17f19531fdd.png" alt=""><figcaption></figcaption></figure>



이후 인스턴스 시작을 눌러서 인스턴스를 생성한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/58824f04-e11f-48a2-aa28-3b369a6ad0a7.png" alt=""><figcaption></figcaption></figure>

인스턴스를 생성했다면 open vpn 이 동작하고 있는지 확인해야한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/326618fc-f406-4c10-91ad-3f6981e4ff05.png" alt=""><figcaption></figcaption></figure>

연결이 잘 되었다면 ssh 로 접속하도록한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/ad016429-f5a6-4c51-96ec-99ae6fe0f5af.png" alt=""><figcaption></figcaption></figure>

github.com/kimdragon50/ec2meta-webpage

에 들어가서 설치를 진행한다.

```
sudo su
sudo yum -y install httpd php mysql php-mysql git
sudo systemctl start httpd
sudo systemctl enable httpd
curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
sudo cd /var/www/html/ && sudo git clone https://github.com/kimdragon50/ec2meta-webpage.git
```

curl "https://d1vvhvl2y92vvt.cloudfront.net/awscli-exe-linux-x86\_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

sudo ./aws/install

부분은 아마존 리눅스2 에 아마 설치가 되어있을것이다.

그래서 설치안하고 지나쳐도 된다.

sudo /cd/var/www/html/ 경로로 이동한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/8a0be4e1-231d-4e71-8f5b-f741bf3e3b05.png" alt=""><figcaption></figcaption></figure>

sudo git clone https://github.com/kimdragon50/ec2meta-webpage.git

cd ec2meta-webpage/

systemctl restart httpd

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/9229a2d9-e9c3-4ff9-b90a-245788f7f1b7.png" alt=""><figcaption></figcaption></figure>

이제 ec2 인스턴스에 private 아이피를 복사를 해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/af60eee5-89bd-485a-83b4-72d84350a282.png" alt=""><figcaption></figcaption></figure>

복사한 아이피주소로 접속을 하게되면 접속이 잘 되는것을 볼 수 있다.

필요한 필수 패키지들을설치했고 해당 인스턴스를 가지고 IAM 를 만들어준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/a6f9d6b6-c7c8-4286-a786-4743fe771487.png" alt=""><figcaption></figcaption></figure>

이미지 생성을 눌러준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/e868c8ab-b3b7-4940-bd1b-297de0c1dcb2.png" alt=""><figcaption></figcaption></figure>

그리고 재부팅 안함을 반드시 활성화 하는것이 좋다 .

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/3ac0bd2c-0210-48b4-a3d6-7e3584a58928.png" alt=""><figcaption></figcaption></figure>

나머지는 위와같이 설정을 하고 이미지 생성을 눌러줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/292f16d0-4657-4933-aec0-9381839c442d.png" alt=""><figcaption></figcaption></figure>

잘 만들어진것을 확인할 수 있다.

이제는 시작 템플릿을 생성할때 해당 AMI 이미지를 사용해서 시작템플릿을 과 연결해보도록 합니다.

## 시작 템플릿 생성하기

생성해둔 AMI 이미지를 가지고

런치 템플릿을 만들어보도록 하자

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/af12b796-4d0f-42da-8dc2-304a7585ccba.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/e4752698-be6e-47fb-8e4b-f2051b39e43d.png" alt=""><figcaption></figcaption></figure>

이후 밑으로 내려가서

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/e126a358-7c2e-4d5d-a0cd-8616552a447f.png" alt=""><figcaption></figcaption></figure>

내 AMI 를 선택한다.

그리고 저번시간에 만들어 놓았던

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/acadf77c-e9a3-40bc-8e84-20bbca68058f.png" alt=""><figcaption></figcaption></figure>

를 선택하도록 한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/0b9db754-7702-48cf-8179-4520f99547e6.png" alt=""><figcaption></figcaption></figure>

인스턴스 유형은 t2.micro 로 설정해준다 .

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/c082184b-5d48-41c5-bcc4-ee60388f52fb.png" alt=""><figcaption></figcaption></figure>

key pair 는 저번에 만들어두었던

키페어 선택

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/980fbdc4-0101-4232-b8f0-deaa9ad54686.png" alt=""><figcaption></figcaption></figure>



나머지는 default 로 두고 시작 템플릿 생성을 클릭한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/409b7b45-cefa-426d-8502-8dfedd94fd5c.png" alt=""><figcaption></figcaption></figure>



잘 넣었는지 확인하기 위해서 AMI 이미지를 복사한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/58745ea6-bc68-4326-8c3d-956b12c154ba.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/68396e97-bb9b-4e4b-88ad-8fe7d6054f41.png" alt=""><figcaption></figcaption></figure>



시작 템플릿 까지 생성을 했습니다.

로드밸런서와 대상그룹을 생성하고 Route53 까지 생성하도록 하겠습니다.

## ELB 셋팅하기

ALB 를 생성한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/a4d7e9ea-ab73-430f-b428-0cd06c7ef4d8.png" alt=""><figcaption></figcaption></figure>



vpc 는 my-vpc 를 선택해준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/78e8ea31-28e9-42e5-9c28-4d615e9908a6.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/165104a1-9dee-4cbf-9d38-45512cd5de8b.png" alt=""><figcaption></figcaption></figure>



subnet 은 public subnet a , c 를 선택해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/43f6e743-061e-4e77-9f97-e1df48387b31.png" alt=""><figcaption></figcaption></figure>



리스너 및 라우팅에는 대상그룹이 존재해야한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/8af81cd1-e3eb-47e4-97e6-59d38f3b5b2f.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/ed86025d-6a6a-4257-a3fe-2a4c431db33d.png" alt=""><figcaption></figcaption></figure>



대상그룹에 인스턴스를 선택해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/980ff553-246c-478b-b358-587f004772b8.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/941b1853-b70c-45e6-84d2-39a43c0ee330.png" alt=""><figcaption></figcaption></figure>



다음을 눌러준다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/15d95a44-958f-4b69-8fd4-d977ffd42e2b.png" alt=""><figcaption></figcaption></figure>



아래에 보류 중인 것으로 포함 을 클릭해줍니다.

이후 대상그룹생성을 클릭해줍니다.

다시 alb 로 돌아가서 대상그룹을 새로고침해서 선택해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/9a9f7bdf-0b23-4197-8d99-e914cd5032f3.png" alt=""><figcaption></figcaption></figure>



이후 로드 밸런서 생성을 클릭해줍니다.

잘 설정이 되었으면 해당 ALB 에 Route 53을 설정하도록 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/4c97f732-7a46-416a-bd8f-209572fb261c.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/63f58a8c-7b7c-46a0-9dc6-848a375179c0.png" alt=""><figcaption></figcaption></figure>



이후 웹 사이트에 들어가게 되면

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/70a81d3c7eaa4eda89e2650dc64cb805/65c76262-8143-4cb9-b086-204bab83d06a.png" alt=""><figcaption></figcaption></figure>



다음과 같이 웹 페이지가 보이게 됩니다.



## 오토스케일 그룹 생성하기

AWS 콘솔에 인스턴스에 접속한다.

![https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture\_images/5e142e316f984b2c9c8ed5a33ef66e77/3a27cf55-eb6b-4f5a-98ea-7d8ef184aad9.png](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture\_images/5e142e316f984b2c9c8ed5a33ef66e77/3a27cf55-eb6b-4f5a-98ea-7d8ef184aad9.png)

오토스케일링 그룹을 선택합니다.

오토스케일링 그룹 이름을 지정합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/image_upload/5e142e316f984b2c9c8ed5a33ef66e77/fd5f4996-9ea2-419d-bcf0-812547bc526c.png" alt=""><figcaption></figcaption></figure>

이후 시작템플릿은 이전에 만들어 놓았던 선택을 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/e22b5ffd-3197-4f07-aa38-75bc15e509e7.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/c78f8ebb-f777-4b8e-8b6d-b21ab7c72fa8.png" alt=""><figcaption></figcaption></figure>

다음을 눌러줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/58cc6210-df48-409b-ab4c-28e8c859d573.png" alt=""><figcaption></figcaption></figure>



VPC 설정을 하고 subnet 설정을 합니다.

subnet 은 private subnet a,c 각각 설정합니다.

이후 다음을 눌러줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/23f4679f-caf6-415b-8bed-e5a6c5e04bac.png" alt=""><figcaption></figcaption></figure>



앞시간에 만들어놓았던 대상그룹을 선택합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/5a99a279-d965-4581-9f6f-72b959d0df7b.png" alt=""><figcaption></figcaption></figure>





<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/38f6f6c6-da43-4e10-aebb-7d9523541f1c.png" alt=""><figcaption></figcaption></figure>



이렇게 선택해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/ca267cd5-fe2b-4e0c-b6e2-4e392ad64d27.png" alt=""><figcaption></figcaption></figure>



상태 확인 기간이 300초로 되어있습니다.

300 초는 너무 길수 있기때문에 수정해주도록 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/0c2aee13-e02a-4983-8ba7-d17ebd3c090a.png" alt=""><figcaption></figcaption></figure>



이후 다음을 다시 눌러줍니다.

이후 계속 다음을 눌러줍니다.

마지막으로 태그만 추가하도록 한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/ecf17db1-77e8-49aa-a068-5414619074c6.png" alt=""><figcaption></figcaption></figure>



<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/18fc9659-d658-4994-afc6-a286f27e49c6.png" alt=""><figcaption></figcaption></figure>

이제 Auto Scaling 그룹을 생성하도록 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/47abed2f-519f-4661-81b4-44daf1f39f52.png" alt=""><figcaption></figcaption></figure>

현재는 용량이 전부 1로 되어있다.

편집을 눌러서 수정해주도록 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/453fe7fb-5cd3-49e2-abd4-6469833911c6.png" alt=""><figcaption></figcaption></figure>

강의에서는 1 1 3 으로 다시 설정을 했습니다.

이후 자동 크기 조정을 클릭해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/480068c1-e967-47bd-a19b-af004161efd6.png" alt=""><figcaption></figcaption></figure>

동적 크기 조정 정책 생성을 클릭해줍니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/42e32ada-c53f-47e4-9153-efab7272131a.png" alt=""><figcaption></figcaption></figure>

CPU 사용률을 70 으로 설정합니다.

그리고 인스턴스 요구 사항을 10초로 가져갑니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/25d72c30-f462-4c1a-811b-876c0cc960ae.png" alt=""><figcaption></figcaption></figure>

생성을 눌러줍니다.

이후 대상그룹으로 가게되면,

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/8b7bb3ed-a58d-4aef-a8f5-22ecbef0fe94.png" alt=""><figcaption></figcaption></figure>

두개가 존재합니다.

임의로 인스턴스 지정해서 넣어두었던 my-asg-ec2 가 존재합니다.

하나를 등록 취소해주도록 하자.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/8258bba0-47ef-4ca2-9654-96b3f6e09e06.png" alt=""><figcaption></figcaption></figure>

Auto Scaling 그룹으로 만들어 놓은 EC2 가 온전히 ALB 대상으로 들어가게 됩니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/7946161b-6e0a-47f8-82ca-dc06a7041d41.png" alt=""><figcaption></figcaption></figure>

해당 인스턴스만 ALB 에 붙어있는 상태가 됩니다.

이후 사이트로 들어가서 제대로 동작하고 있는지 확인을 합니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/5e142e316f984b2c9c8ed5a33ef66e77/93aa3218-1296-4426-b503-afcd7ea53dad.png" alt=""><figcaption></figcaption></figure>

오토스케일링 그룹에 의해서 만들어진 인스턴스가 맞는지 확인을 해봐야합니다.

이후 EC2 안으로 들어가서 CPU 사용량을 늘려보고 실제로 스케일 아웃이 잘 되는지 확인을 해보겠습니다.



## Autoscaling Group Scale Out 테스트

인스턴스의 IP 정보를 가져온다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/7d257227-3b6f-4ade-938d-ae51d6bc5cd2.png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/146b9f24-d92d-47b5-bcf9-366cf258a622.png" alt=""><figcaption></figcaption></figure>



계정으로 로그인합니다.

amazon-linux-extras install epel

하게 되면 패키지가 설치가 됩니다.

이후 yum install stress 로 설치를 한다.

이후 해당 EC2 에 테스트를 위해 stress 를 주도록 한다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/5a3ca9ff-de98-4cf8-9d1c-aa95c4715c0b.png" alt=""><figcaption></figcaption></figure>



동작을 하고있다.

top 명령어를 치게되면

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/fe28cb8f-8279-4ec5-a78a-a2089f5f2d71.png" alt=""><figcaption></figcaption></figure>



CPU 가 99퍼센트로 부하가 계속 걸리고 있다.

다시 AWS 관리 콘솔로 들어와서 Auto Scaling 그룹에

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/cc928a49-2d44-4b24-99c0-317c2c5e3836.png" alt=""><figcaption></figcaption></figure>



앞시간에 만들어 놓았던 곳으로 간다.

![https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture\_images/b0a7234f89674dff956b8c635ad3d883/67e91953-ad87-47ed-8fed-f66d95c22b4e.png](https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture\_images/b0a7234f89674dff956b8c635ad3d883/67e91953-ad87-47ed-8fed-f66d95c22b4e.png)



활동 탭을 클릭한다.

현재 저희가

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/2bf06b49-66c9-4508-b775-488e97fcaf03.png" alt=""><figcaption></figcaption></figure>



크기조정에 70으로 설정했기때문에

사용률 70 이상이면 인스턴스가 늘어나게 됩니다.

늘어나는 활동을 활동탭에서 확인할 수 있습니다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/13a57373-4fce-431b-953a-c053d841466f.png" alt=""><figcaption></figcaption></figure>





<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/0cec9bfe-1b48-45d3-8819-b1f2d61b8bb4.png" alt=""><figcaption></figcaption></figure>





모니터링 탭에서 ec2 를 눌러보면

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/f4221822-55dd-4625-a03e-ac3a734c6ec5.png" alt=""><figcaption></figcaption></figure>





지표수집을 하도록 해줍니다.

작업기록을 새로고침하게 되면

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/1c6b87ba-1f18-438e-aab5-bcae7458310a.png" alt=""><figcaption></figcaption></figure>





인스턴스가 생성이 된다는 메세지를 확인할 수 있다

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/a99b9249-b37b-4028-95ff-55aa1af959f5.png" alt=""><figcaption></figcaption></figure>





pending 상태로 스케일아웃이 되고있다.

<figure><img src="https://slid-users-assets-v1-seoul.s3.ap-northeast-2.amazonaws.com/public/capture_images/b0a7234f89674dff956b8c635ad3d883/c58eb5fb-6ac1-460e-8bc1-c06c101d9011.png" alt=""><figcaption></figcaption></figure>





이제 도메인으로 들어가서 서비스를 확인해보면

이제는 해당 부하를 없애고 난후에 스케일인까지 해보도록하자
