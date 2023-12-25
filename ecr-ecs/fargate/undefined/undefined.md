---
description: 성
---

# 보안 그룹 생성

**4-1) 보안그룹 생성**

* 위치 : <mark style="background-color:purple;">EC2 > 보안 그룹 > 보안 그룹 생성</mark>

보안 그룹 (security group)을 사용해서 특정 IP와 포트 만 접근하도록 허용하는데, 여기서는 80 포트를 허용 합니다.

로드밸런서의 접근 허용은 80포트로 제한합니다.

(1) 보안 그룹 이름 : saju-alb-sg-prod

&#x20;

(2) 설명 : saju alb security group production

&#x20;

(3) VPC : 디폴트 VPC를 선택

&#x20;

(4) 인바운드 규칙 : 규칙 추가 버튼 클릭&#x20;

&#x20;

(5) 인바운드 규칙 설정

* 유형 : HTTP, 포트범위 : 80, 소스 : 0.0.0.0/0  &#x20;

(6) 태그

Name : saju-alb-sg-prod

Service : saju-prod

<figure><img src="https://lh5.googleusercontent.com/7vKpTkb5K4lZOfETO1ZS3guxGLMS637WUplHr2ptEy9QiHiQDDsAzB8VaOOJyDPQ4Iyz_dVVIr3zvnoPRqqzWwh1b4JqtXv-r8lQAWmcut9g7Z9ivaUE38GxdPByG0fC9kWvcW_CAMtP1rjJE0isqqF-am46llDMcCpsz6_B305xR5Jq1kXg64nERQ" alt=""><figcaption></figcaption></figure>



![](https://cdn.inflearn.com/public/files/courses/329624/units/129025/470b6918-14f5-4961-b5fc-749e166f4c9b/blob)

\


