# RDS 보안그룹 셋팅

RDS 는 Fargate 와는 전혀 상관이 없지만 서버를 올리는데 무조건 사용하는 녀석이라.

여기에도 그냥 함께 메모를 하도록 하겠습니다.

* RDS는 관계형 DB 서버로 여기서는 MySQL를 사용합니다.
  * PostGreSQL 를 사용해도 설정 방법은 같습니다. \

* DB 서버를 EC2에 설치할 수 있지만 서비스 안정성 및 확장성을 고려했을 때 AWS RDS 를 사용해서 별도로 분리하는 것이 좋습니다.\
  만약에 EC2 가 죽게 되면 데이터베이스도 그럼 사라지게 됩니다. \
  서버가 죽더라도 데이터는 남겨두는게 좋습니다.



## 보안그룹 생성

**1-1) 보안 그룹 생성**

* 위치 : EC2 > 보안 그룹 > 보안 그룹 생성

보안 그룹 (security group)을 사용해서 특정 IP와 포트 만 접근하도록 허용할 수 있는데, 모든 IP 허용과 MySQL 3306 포트를 허용 합니다.

(1) 보안 그룹 이름 : saju-db-sg-prod

&#x20;

(2) 설명 : saju db security group production

&#x20;

(3) VPC : 디폴트 VPC를 선택

* 지금은 디폴트 VPC 를 선택을 하지만, vPC 로가서 VPC , Subnet , Nat gateway, Internet Gateway 생성 하는것이 좋다. \
  데이터베이스이니까 Public Subnet 에 두면 좋지 않다. Private Subnet 에 두는것이 좋다.

(4) 인바운드 규칙 : 규칙 추가 버튼 클릭&#x20;

&#x20;

(5) 인바운드 규칙 설정

유형 : 사용자 지정 TCP, 포트범위 : 3306, 소스 : 0.0.0.0/0

* 지금은 테스트이기때문에, 다 열어준 상태이지만&#x20;
*   EC2 나 Fargate 에게만 RDS에 요청해야하기 때문에 RDS 접근을 요청보내는 서버 에게만 허용하는것이 좋다.\


    <figure><img src="../../../.gitbook/assets/스크린샷 2023-12-23 오후 12.18.50.png" alt=""><figcaption></figcaption></figure>

    이와같이 EC2 서버 보안그룹을 생성하고 난뒤에 불러오는것이 좋다.

(6) 태그 &#x20;

Name : saju-db-sg-prod

Service : saju-prod

Service 로 태그를 다는 이유는 Resource Group & Tag Editor 에서 한 번에 해당 프로젝트의 리소스를 검색 할 때 필요합니다. \
Name 태그는 리소스 마다 이름이 다른 경우가 발생해서 모든 리소스를 한 번에 볼 때 사용할 수 없습니다.

<figure><img src="https://lh4.googleusercontent.com/tmers2BKc14PMESD0xILvgha1izJ-KWa3-L_-XL0vTfkamfTsHf_rADKMQ0nB9K4hrHAxty74NprTid1_4k39nPON3VVtP8koFS5iO6iF8DXVeabJyVKEWOSIZeKBz-qnksaU4xmQ_8oPf43z1N7VWnfZ-9UF2YeJUftqDza34uDrv54wN_DyxcQeQ" alt=""><figcaption></figcaption></figure>

<figure><img src="https://cdn.inflearn.com/public/files/courses/329624/units/129025/7d5847b9-676f-4b42-8cda-ab3fb4bca84c/blob" alt=""><figcaption></figcaption></figure>
