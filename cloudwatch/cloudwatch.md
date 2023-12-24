# CloudWatch 슬랙 알람



**10-1) CloudWatch 슬랙 알람**&#x20;

* 경보는 특정 지표를 넘는 경우 발생하는데, 경보(Alert)가 발생하면 Slack과 같은 알람을 보내 줘야 합니다.
* 로드밸런서, ECS, RDS, Auto Scaling 등에 경보(Alert)를 발생 시킬 수 있습니다.

**10-1-1) SNS (Simple Notification Service)**&#x20;

* 위치 : SNS > 주제 > 주제 생성
* 주제 : 표준
* 이름 : saju-alert-prod

<figure><img src="https://lh3.googleusercontent.com/xCxXuOIlncYbivMnc6718s99Ip7khqoYfwQDlPkQh6A8rRHE4hQj_AxlqgZYPgAYsGvZ_Gi0Uc4xxWYYWau-c0BWfTI-PxRlgdypbhjUJXxh98saVxTQQyxLzVgBWz3m6J97rgWu9Ki_KMLYaEvHiIaMCIYhgFo5Gpo7uCQNEcT8j1OjLhHYKSXAZw" alt=""><figcaption></figcaption></figure>

&#x20;

**10-1-2) IAM 정책 생성**

* 위치 : IAM > 정책 > 정책 생성 > JSON

<figure><img src="https://lh6.googleusercontent.com/vc4G9UUKfzVXjGvBZ5C5mcaRUxnjx9lMfmiFFdj291UH-aqibQHxVtV4FHqJeuMsQBORpd7CPmdnAEibi9H9uYusqmUaurlu37LlgO1Q7z2JoQU1yf57UKQaJWWmOvMthQ9GpVCNZRS7M_uXbf7-3FTuj6krv2ScQPxzA3dEXfUEmCFLGkGYrPJTjQ" alt=""><figcaption></figcaption></figure>

| <p>{<br>    "Version": "2012-10-17",<br>    "Statement": [<br>        {<br>            "Sid": "VisualEditor0",<br>            "Effect": "Allow",<br>            "Action": [<br>                "cloudwatch:*",<br>                "cloudwatch:List*",<br>                "cloudwatch:Get*",<br>                "cloudwatch:Describe*"<br>            ],<br>            "Resource": "*"<br>        }<br>    ]<br>}</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

태그

![](https://cdn.inflearn.com/public/files/courses/329624/units/129107/43eacfcb-b2dd-4437-b6d4-894ee63c0fe4/blob)

* 정책 이름 : **AWS-Chatbot-NotificationsOnly-Policy-prod**

<figure><img src="https://lh4.googleusercontent.com/6b2UaWgELJ2B_7eQI3gEqnPTQ_2G-XlbFzih1BDn7tSUBctV7sGbp_-fkizVz2ZUisdqUVW7OCUf5TLlFXRso-j5a2Y-VRIY2tw-neN7O64tH3_xbQC30CtJUNhuLbmVU31mWDpTP38XsIv7d6m0Rl2_aHSKHoHMKT3Zj5XMssMbSLtcJxosiGq_gQ" alt=""><figcaption></figcaption></figure>

&#x20;

**10-1-3)  AWS Chatbot**

(1) 새 클라이언트 구성 : Slack

<figure><img src="https://lh4.googleusercontent.com/uDvjSbvE5EdyvdDYE4wHOnYqNNOxC_KmmHrPWHbJtJeXEwhPMEMPIBIb7v2e2n8eMQ-XcaAVtvtT6f5o77hnnJdR2CH7I98nHecuH29tgs-BcfxAJpqQzU9DQS5pvcrFbPEYB17eZ4TnfROt-RZ5GrZUbxDNv8sUAlPgBCJoAWeKGW9NEiawlPxdHQ" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 구성 세부 정보&#x20;

* 구성 이름 : saju-alert-slack-prod

&#x20;

(3) Slack 채널

* 채널 유형 : 퍼블릭
* 퍼블릭 채널 이름 : saju-prod

&#x20;        \- slack에서 saju-prod 채널은 미리 생성되어 있어야 합니다.

&#x20;

<figure><img src="https://lh5.googleusercontent.com/S2pE6w2NUVPtWqS-xc5rWjznJuS4Op-2_ptpRYuj53WVN4v1LarrS4Cff7J6NDPD97KoP0Dz2BSe0-7DHboau8gDDseJ3ENq3EiVQXcJ7xg0Y11_pJziiEydo4qwsmG_uevSP9jclzeSHIywfGeIPPi0ULPhwW_GIsZoM1OEQdu7i7w1Zgb9p6qDAw" alt=""><figcaption></figcaption></figure>

&#x20;

(4) 권한

* 채널 IAM 역할 : 템플릿을 사용하여 IAM 역할 생성
* 역할 이름 : saju-alert-slack-role-prod
* 정책 템플릿 : 알림 권한
* 채널 가드레일 정책 : AWS-Chatbot-NotificationsOnly-Policy-prod

<figure><img src="https://lh5.googleusercontent.com/xM6j3h-K0Lb72tnDPfIybTaxClBJCzHwpl5I4VVGwOAaixdOjnpMHV1MXGaquVIs0aTyCgWdza0p4ShzruLwGgUvn9MoO9-qguFsqSAjYqE-DkXb5jjQPPu7tAsr1csmLkybNmQ46J3XMH3147BN8_WqLtBpxRzZMxuRfcWAuiCcbgCaScrk7ngamw" alt=""><figcaption></figcaption></figure>

&#x20;

(5) 알림&#x20;

* SNS 주제 : saju-alert-prod

<figure><img src="https://lh6.googleusercontent.com/TsHe_Fdk-UdrqkpkvbGaRvaoXXJGJexoFVW9rVmilSKoV0idbo2tEV5_Hfi43FER-crSRVYpPJ5G9TToSqs52T8FoUbZQE8YUczJVsAb82dvu0Tt3FMSAlnubLHIYjBeZ6EQxPBKasBtHuYECNmNz1aqkutzKcmTiLIxwJssrx3lc3aScuX_E4MeBQ" alt=""><figcaption></figcaption></figure>

&#x20;

**10-1-4) SNS**

* 위치 : SNS > 구성

saju-alert-prod에서 구독 정보가 생성된 것을 확인 할 수 있습니다.

<figure><img src="https://lh6.googleusercontent.com/qi9EW0A2hagdcR1qqn4l42n4WyLPOdXNWYDG-Szkc6fEuP6ckVlBmaTfe96m-jaxlDv7c33COVK1qyN8y0kA-zKZUPyPgFU6jnF8lPu8euPHjht94AeyQ5uXGNPC4cnK6SAmy5RWYKvx4za1bUI2H3g_HGV9gV8utBiGejhCKg3X9-S0seymXkovJg" alt=""><figcaption></figcaption></figure>

&#x20;

**10-1-5) CloudWatch 경보 및 알림**

* Alert (경보 상태) 일 때 알림 설정
* ECS의 CPU 사용률 관련 경보를 만듭니다.
* 조건은 테스트 용으로 CPU 사용률이 3%가 넘는 경우로 진행합니다. 실제 운영 서비스에서는 50% 정도로 진행합니다.&#x20;

(1) 경보 생성&#x20;

* CloudWatch의 경보(Alert)를 클릭 후 모든 경보를 클릭 합니다.

<figure><img src="https://lh6.googleusercontent.com/9EUpFDPUwSemT8OCuY5LvhEA-COc0RExF_TJdKQck1MV--RvkpTiJQhJGANTj5ti_S_U6C32zYmavNU1QBfL5yn68PSxNAeAi7j970_BaDrc5a0O9RrSetUtT1Nyytvj8X1SOoY7IROCTF3NKp0KXFmc2BuG69sGSHPIe6WuUPUoQVlb2stSmZkmYw" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 지표 및 조건 지정 : 지표선택

<figure><img src="https://lh5.googleusercontent.com/oqrnuHEfcvpNIm0Xidxwt9VC28A_xZoSSACZtI2iZ7OvTwTv__HU3MJDDsP5OfA-jvCkA1YvthS-g2beD8mr7Z5ZbeEe6bDcv8K7q0lddQpuxGNFj8HTzXS3W1tZmArhP9BdmMAuKvksxf3u2z2TYwaJIcniA6XsIYUdvXbPQ2BHycmvba0-1zC2nQ" alt=""><figcaption></figcaption></figure>

&#x20;

(3) 사용자 지정 네임스페이스 : ECS/ContainerInsights

<figure><img src="https://lh3.googleusercontent.com/L161MB-rhrW2jssP0GdWMVxUtV7z1zGjll6tJMtwyEv4QfPi31H0CnxRI8mFzCujX4MR7XFNANQM5WYwIu5gJCoIv8ClyxPwZtTzxfPbBTr54MLQ0tH9DW-fHupy7UXjrZbcRH7Z5aAs3HNmUZ8_x_FDWTJa-X7DURWDxguVP68ICU-8EaQzzqS-Ew" alt=""><figcaption></figcaption></figure>

&#x20;

(4) ECS/ContainerInsights : ClusterName, ServiceName

<figure><img src="https://lh4.googleusercontent.com/8UZmyvgsGVbIIAoU5JSTYTiZQtCmSuALGE2AthqwrEHu7DjUplSbGzxS9e4ijWjgjRFFntiBryV64o_UlgkAPJDk5D4FVF_s5gt2MCT2MhkoB_32Pa-qzPqwMkGa8rmA1GjyOWOyVJZC5UI1ZckiVSrDaBiLEhGFFkjlUWriv2mKDxJpOfHWoBhfdA" alt=""><figcaption></figcaption></figure>

&#x20;

(5) ClusterName, ServiceName

* ClusterName : saju-cluster-prod&#x20;
* ServiceName :  saju-service-prod&#x20;
* 지표 이름  : CpuUtilzed&#x20;

CPU 사용률을 기반으로 지표를 만듭니다. 특정 CPU 사용률을 초과하는 경우 스케일 아웃 합니다.

<figure><img src="https://lh4.googleusercontent.com/vOM_wAz1hE-R_1VN8fehSxbra-kxIXQLkDeOdvvKwlbRwCPEX2avMWbJKfqejz0GjAELxBFyKV02Ao-DLwu3cdayrEaRyPxqromgMwkoOF3JlrNUAjTUkebqNgFGx3jP6ww3XlZxlfqLOVA9zWum8BHf1pQJ3n1Rfad2XFQ1QTS9HjXtsJeLwuXnew" alt=""><figcaption></figcaption></figure>

&#x20;

(6) 지표

* 지표 이름 : CpuUtilzed
* ServiceName : saju-service-prod
* ClusterName : saju-cluster-prod
* 통계 : 평균
* 기간 : 1분

<figure><img src="https://lh3.googleusercontent.com/2XJ2KwGf_Vq0dyGT1mt42icjADnol0jiC5kuSOhfO0uLPO2qjcoTUFN4u1MQkBYPp_EXNKzW5v0J9-40LE6DsAnwVin6cbTBJHmtBNLn6eJ5_ak4bncCk80ZAQsXmIlx3LWL3CVh49XN5V8CUCOp2RAColqxuW8nqk-KBR12qzszwT1yTBHjbNIOKg" alt=""><figcaption></figcaption></figure>

&#x20;

(7) 조건&#x20;

* 임계값 유형 : 정적
* CpuUtilized : 보다 큼&#x20;
* 임계값 : 3      //CPU 사용률이 ㄷ% 보다 클 때
* 추가 구성

&#x20;         \- 경보를 알릴 데이터 포인트 : 1 / 1 (조건은 1분 동안 1번 경보가 울릴 때 입니다.)

<figure><img src="https://lh3.googleusercontent.com/uQiNIN7_nrRwIUmqwG-z6bmVNAKmgxv5h_wuxo2EgZBP7OG9QrcbwotxC-LCWggBNXdCHu3Qded6P7Mbp0GI0xBJbKdF9IFjf_ssAVYUqUHIG03__0aJaIddcX-kFUoCmX7tyqheoeiDdnpxiGQdbNlJcwfHB3utIXd_vwSnWE6A0QUF_ygczFVcZg" alt=""><figcaption></figcaption></figure>

&#x20;

(8) 알림

경보를 생성한 후 알림을 추가합니다.

* 기존 SNS 주제 선택 : saju-alert-prod

<figure><img src="https://lh3.googleusercontent.com/5fF7Rs5yyGI4F68TnQoZTNBtrXBL8DrTjD5pNVcqPtdX4XGg2kbjJmHLal4OOwZUJ9CQz0ylfRF47qHUqJZwLh9vVMxG95odGsFQBwgj1esFRF9rv_plGtMGKJ4nDPJYVprztpKu692enAugtDYuC9ThFDBLHxcmPTvxxJtiEtivK-_Tycc6J4m_BA" alt=""><figcaption></figcaption></figure>

* 이름 : ecs-cpu-alert-prod

<figure><img src="https://lh4.googleusercontent.com/d6lThghCYNhgsHFZCrO0m0ZKutZD2FEaXO7S7BekpnXV3fCCediO0OK4FmTVHNxhadU6ESgkNn1UtSaQYaesA2NLLX4nwiFR0qc7FHUIaJvtuAd-Ls3yuU2W-96LLrpI-USpouoErSYyH_24jRdE2m7MiIKp0-OlBjtvr4IXf9HlwYP-yHhLugFo7Q" alt=""><figcaption></figcaption></figure>

&#x20;

(9) 그래프

ecs-cpu-alert-prod 경보를 클릭하면 그래프를 볼 수 있습니다.&#x20;

Alert을 넘으면 slack 알림이 오는 것을 확인 할 수 있습니다.

* 위치 : CloudWatch > 경보 > ecs-cpu-alert-prod

<figure><img src="https://lh3.googleusercontent.com/6Agwsld_c1zncfBPNDwL7hfW1D-QHisHRsr-eDWfdQ0x9r0BJrdVGDcSGNvy1tclwLkxsdFLD5ZepdlvnQiQLu-Q3W5LoTS6RajObJtygyBoAd0wFBHtnSr1qTW_GT70IIO1OALzaXX63QascLSigh2rbk9J9o_J3lTFV4RWl32ktOzC68YGH9biBw" alt=""><figcaption></figcaption></figure>

&#x20;

(10) 슬랙 알림

![](https://lh3.googleusercontent.com/BUdYXH\_bI6gPzZx7IVEG5Y\_E62PCiMt26evW76Ey0ZQM7nuncLEByDFjVw0zKB0rRXCZ-nGOahkzTR4b8M1Dj911T7YZ1CGPgEjLTPyRDqvof0UoZmyEbl-NOptaYT-WH1LX2KrHiHNC\_huSUw0W2YW0elpOvLMW2qHKW24hrSYdYY\_Fd0IiQj5LDg)

&#x20;

