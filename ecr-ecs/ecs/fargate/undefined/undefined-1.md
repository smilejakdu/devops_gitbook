# 대상 그룹 생성

**4-2) 대상그룹 생성**

* 위치 : EC2 > 로드밸런싱 > 대상 그룹

대상 그룹은 로드밸런서 트래픽을 분산 시켜주는 EC2 그룹입니다.&#x20;

(1) 기본 구성

* 대상 유형 선택 : 인스턴스&#x20;
* 대상 그룹 이름 : saju-tg-prod
* 프로토콜 : HTTP&#x20;
* 포트 : 3000    //로드밸런서(80포트)에서 EC2(3000포트) 타겟 그룹 전달

<figure><img src="https://lh3.googleusercontent.com/fvLYRGI3VC7Q0TeOdGBInNJk5x4puSaHJomSdbxfVEYZ7wTIyuVJvoukiywORxhHa9Cv7o0k53w1BeWSEgPcbyAByx4MkpBukkwVLniEd0ZpNtBYW8q0E-5PGO-7JCQnPNv_t9rOkuk2vh49I9Sai7UU0gzD9RfU4sJmb2gVnEbOGIUxJUTF5VrJEA" alt=""><figcaption></figcaption></figure>



<figure><img src="https://lh3.googleusercontent.com/fj_Tozsachpy06ztrulSijn1EXsg6QqetX-JxDp45h88-bAqqCYow8OHTwuiCfSp3gHKPiFTAKRzKgQydV_qSubyJ7yISQQTWjBC-6GmjUh6M0y8VtBGxpV1DwYfDbvSw8GLwHf5WoJAXbk0ro8tcFUF0m6wYKUyHCSPxMzU1Rg9S-N4VzkeOsKHcQ" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 상태 검사

* 상태 검사 프로토콜 : HTTP
* 상태 검사 경로 : /

상태 검사 시 로드밸런서가 / 루트 API 가 실행되는지 테스트 하기 때문에 해당 API는 반드시 있어야 합니다.

<figure><img src="https://lh5.googleusercontent.com/KHvywfbRItbZfsLZ3cbHR3YEWnoZujoEBjgZNPVDsjXL41hVgUokSJ5AF1ZHaU5POQx2WWL6L1oA-KIX_XoZS5p39SBdXMRJnk50ZMEOmcEUJVrmIdXHHDeony2RLGro-THKtdtwAnzh0XzMNN3-T5vAPE1Sq3_iMpmVG-tErsCIfiYtMw3JWJSU8Q" alt=""><figcaption></figcaption></figure>



![](https://cdn.inflearn.com/public/files/courses/329624/units/129032/041d1155-9bb7-4ec2-9306-c5ba4c3bb162/blob)

&#x20;

(3) 대상 등록

* 선택한 인스턴스를 위한 포트 : 3000

&#x20;인스턴스를 선택하고 아래에 보류 중인 것으로 포함을 클릭 후 대상 그룹 생성 버튼을 클릭 합니다.

<figure><img src="https://lh4.googleusercontent.com/QLKDfppxlDMq05fqCx4wTsL86hxBP8aWO5WgvEG6BF_fVLMBlVA8EXC9uOwmO6N4q_nwDw1C98ETYv_go6KeZxa_l9kOX9lFjCpoo6lwSjdPDqCW1dMx7XGGEZ-cY0ncisCSMX5UUZsmc3pLiMHWVng1yl7Jqe1MUsnMojvY3-Ss0-X0pedifOQIvw" alt=""><figcaption></figcaption></figure>
