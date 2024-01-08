# 로드밸런서 생성

**4-3) 로드밸런서 생성**

* 위치 : EC2 > 로드 밸런싱 > 로드밸런서

&#x20;

**4-3-1) 로드밸런서 유형 선택**

* Application Load Balancer 를 선택

<figure><img src="https://lh6.googleusercontent.com/d4mamxaksrpJ0H_kKag7mftcSrwpJ-AN6G4aNIueeBrsXLzX5jLFXqjBmekKdLTCbESD9Jw8EWuVWyfx0JJ5aFFDZR-YnDi2sr1Z4eU64eklNTUIPzgMKeBLGnsnsAAlisNh2hlmFWF_DsVKSzRTVBBKK0gYwteneyi86RvkK_XJfY2ryv2BeSEdGw" alt=""><figcaption></figcaption></figure>

&#x20;

**4-3-2) 로드밸런서 생성**&#x20;

(1) 기본 구성

* 로드밸런서 이름 : saju-alb-prod
* 체계 : 인터넷 경계
* IP 주소 유형 :  IPv4

<figure><img src="https://lh4.googleusercontent.com/rClNKnpDq_p5-9wqsXfW9HeGgspipKeAGTUt-fu6GWHuxPUhVdU7XPNP_XV0TeKN8swNkDphogfjQXuOUghipXSN2cN755dTHoZWVjFwSTEK3tquTgP3bHaZFx6m9QpnfKinYX7HzewIaVuUq5KpyNeU7tuUg5wkJ7cvvu9CY0IiuxARbLPY2xbIqg" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 네트워크 매핑

* VPC : 디폴트 VPC
* 매핑 : ap-northeast-2a, ap-northeast-2b&#x20;

대상그룹에 등록된 EC2의 AZ(Availability Zone)와 일치 해야 합니다.

<figure><img src="https://lh4.googleusercontent.com/Ckmz_zFZeIudoZSTFxDXjRn0s6OArjrlFkxk1GHBhrS63-clw0dcWoP3EXcdsJMbyhqFjcUX7icSuFnP2DD4qBXd3Dq3qvqmdPCIM3ExvRwWsn2N6fIYyLAogACbSsfG9VewS7-4tLbbhRCSU-S39Y_0oF2UHiLcnBi-Qze0GFEEoaANiensjRujNw" alt=""><figcaption></figcaption></figure>

&#x20;

(3) 보안그룹&#x20;

* 보안 그룹 : saju-alb-sg-prod

<figure><img src="https://lh4.googleusercontent.com/Gf9HnxIlAiFsHl3YGTu17zEohoFhIz_QAwvm9NrcE79w51-P1kvP5x9ffExMS05JtfZX7HW6AwTf7sN_1H-DdaxuLFUbkJSgo8eWHh8btCxjy9RHQJwoTxOdRl8OZygWxpsW_TplvOa63gek04wSQHnQH2La7o-QvL6uldpVoDjwrXmTUa0-a0CtKA" alt=""><figcaption></figcaption></figure>

&#x20;

(4) 리스너 및 라우팅&#x20;

* 프로토콜 : HTTP
* 포트 : 80
* 기본 작업 : saju-tg-prod

<figure><img src="https://lh4.googleusercontent.com/WehTSJN3UaexeFvKXqn3OBiyHsEqzyi6pRsLPxgnpq2uqeabmGJCupYiFNG6P7zpdusFftwVCT5DRHpvqtEZiW8av_j8RopRe41F1uOfMO21umAN4zFQHFx85XsmpGCqYfZWEP1vnn9b1BojB6FV5XGcI7rXcBv7zjpQ9IfcAX2rjOr7fEuIq_NzPg" alt=""><figcaption></figcaption></figure>

(5) 태그

Name : saju-alb-prod

Service : saju-prod

![](https://cdn.inflearn.com/public/files/courses/329624/units/129032/fa1933af-3d82-4b30-88cd-e35a0e8c1dc8/blob)



\
