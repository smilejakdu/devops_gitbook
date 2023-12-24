# RDS 생성

**1-2) RDS 생성**

* 위치 : RDS > 데이터베이스

(1) 데이터베이스 생성 버튼 클릭

<figure><img src="https://lh4.googleusercontent.com/Oua0NsUZltgHVw3IQxlfhXKgPcI2FGihfHhYNeDwnf7Jfg0J7-MzLwC-uVHe61-EzKGf74CrPb8a510Unly--BvihdWneeGvqPH4VFKhSV4Gho-XV6tWVDhldS1-2xKd-chZvXsqM48NHEb-RCtiChikw-xmktkvva7VbGNL67ViiTh6_65wzVurzQ" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 데이터베이스 생성 방식 선택 : 표준 생성&#x20;

<figure><img src="https://lh4.googleusercontent.com/NKrXTz3k-yc2GtyYtU7-gLRyXMOEObULf7wh_XecpDSuEwNkFQ5pTbSS6YfROIQbNcBYCLsTd-N8B6MxNa75t96IzszghziB52KbwCSMdwrpGSbJZHUXEoLt0ToVlyYSRKGvRH-ocAQEX_OL4XJzkJ4hr6Gv43uMV-A3dvVi7Uz992ivOX3SJJFQLQ" alt=""><figcaption></figcaption></figure>

&#x20;

(3) 엔진 옵션 : MySQL 8.0.28

![](https://cdn.inflearn.com/public/files/courses/329624/units/128939/49212992-a039-45bc-95fb-18c047dd3758/blob)

&#x20;

(4) 템플릿 : 프리티어

<figure><img src="https://lh5.googleusercontent.com/3U3c45yvfuo9JiZcSaR6ZVMib3dCYezxBe67qEOzkbljgUsG386csZsB9k8hCs-LW6fnmA-fzAI0IxpQV36NondgGWSoXL65pcOcuNjBmnMNu3xlnC_5TtzZZ_RNZ_p7gqRvUlFpZ4XFgkQXmkeoUt6nf4TovVBlufsTsTsFwEuhDr9Vv75wciuW5g" alt=""><figcaption></figcaption></figure>

&#x20;

(5) 가용성 및 내구성

![](https://cdn.inflearn.com/public/files/courses/329624/units/128939/06d21cff-4a37-40c1-aa09-ada0a6809c9a/blob)

&#x20;

(6) 설정

* DB 인스턴스 식별자 : saju-db-prod    //엔드포인트 주소와 관련이 있습니다.
* 마스터 사용자 이름 : admin                 &#x20;
* 암호 자동생성 선택   &#x20;

<figure><img src="https://lh6.googleusercontent.com/J6I2pAdTs8BLx1hGr9ecewxW5vvqc1net1kWiKo_tKqrTUqRUAbVdpMvlQwKIAdmn7r23E0Lk3BtFAxYv-l8NBh0fb_UkfU3LyrPdPr8--22K00jHxudzA-wHnCZPxQMh6DIY0529bKsHNEzLyN95-cBofKBwhoXUfRYuzcUS-4WJwaDGuk-tN34Qw" alt=""><figcaption></figcaption></figure>

&#x20;

(7) 인스턴스 구성

* DB 인스턴스 클래스 : db.t2.micro&#x20;

<figure><img src="https://lh3.googleusercontent.com/Yh7P7_EvKkg7_OeIig6BUfIbPXlyhqB2zyix7Tv3g1gxXW2um-W2JFWTv92s7cEYP1sVc6p2HXFCCwVgZwBXVQ2_5xk8vTvDEMlVYPmeaKrEo9s0Psj49TpPnUhlqCG-NqRBE5XvsSJ3YvLYEJeBd4nVNOQzCHoQb6rbYbyxqDbWjQ83krPbRPGkJQ" alt=""><figcaption></figcaption></figure>

&#x20;

(8) 스토리지 : 변경 사항 없음

<figure><img src="https://lh6.googleusercontent.com/tH6jcCpaS7vkVBlpQs-ijsZgO8mFqGh5uzqqq9JJHVY4hPUlGdyAZ13KH0970xIRA6N6-TcsCVixYsRRxxFJyf75vL990Dws0tju2H7DanjfSy3lQDOemK2KKXYXOGV7bWh_63MX7v-0YKk3Pg6NhJMbKnJBSAOHfOmwKJvhAmmhonv8g5Ku7VlHSw" alt=""><figcaption></figcaption></figure>

&#x20;

(9) 연결

* Virtual Private Cloud(VPC) : Default VPC
* DB 서브넷 그룹 : default
* 퍼블릭 액세스 : 예        //DB서버에 원격 접속을 위해 필요
  * 하지만 퍼블릭에 두면 보안에 좋지 않다. 그러므로 private 으로 데이터베이스를 두고 bation 으로 두거나 open vpn, SSM 으로 접속을 하는것이 좋다.
* VPC 보안그룹 (방화벽) : 기존 항목 선택
* 기본 VPC 보안 그룹 : saju-db-sg-prod
* 가용 영역 : ap-northeast-2a
* 데이터베이스 포트 : 3306

<figure><img src="https://lh3.googleusercontent.com/NiWXrsXg0osA-uxSkPGIK_7KCDSSUCONJb67WuGtFsHML1EcCzbsNtx3KE9BURengp3Bty9tAQt7uXAmaTxYNp4vC9r7kIFrEXR_wPi9WgQuq0lYF8RyNsl5uABDuNwAFh6eHiqgpzFRKGz2pBfTcQ2sMvteAhLSJo-h66aXMIhFd07Qk7Cc-brawA" alt="" width="563"><figcaption></figcaption></figure>

<figure><img src="https://lh6.googleusercontent.com/azrV_edRE_rWtLuIrF8pMrwWFH5Xca26ATw3gj26ZT8R2_sDMQhRb2prNT222legmkVlRqoJTz7Qz5Gxf5tpvzLYqP25krMFfSIq0AQzSnfz2C78PaXhVnlDFM6JSZHPU48jEQjXD6hYV-QX3zByROsSM2uo8sXXdCNKgnJ-QGT3T6R31GeU_9p8YQ" alt=""><figcaption></figcaption></figure>

&#x20;

(10) 데이터베이스 인증 : 암호 인증

<figure><img src="https://lh6.googleusercontent.com/ta7oiydiW4LM_eFHXK5skI8ign5LzYwI_20H_p2u4HMldKFYb0Vw4Wv3VYQWmnYDKaBXwM553r_Y6vF3oyKE-aXlGTrvj6BSPKxLixMpMOMiWzAVoArp0g-75WVog8ChI86JS8vhQSwEJxJgJy2hKGrxQKSGLqCtUijZQrOd_G761A1-RXYM730gfA" alt=""><figcaption></figcaption></figure>

&#x20;

(11) 모니터링 및 추가 구성 : 변경 사항 없음

<figure><img src="https://lh3.googleusercontent.com/2EIafUac14GcaNtR1Q4p1ruNiQJ82W3-gVJCB1Ip6J6jt1pWW6vSxBiUJmAUw3qrQgKimGj22kaA4K9C6hqGsLfR_MKjrnDGQ_R5u5zvXxpQQ9_dCT0IWJkHVTVeiFkypUmXK-twbcv1c3u7rSktnBq_Jvfka3agiZuRezNnusic9se_ylh6d3wUOg" alt=""><figcaption></figcaption></figure>

![](https://cdn.inflearn.com/public/files/courses/329624/units/128939/d5ec62f7-899a-46a9-a266-c54b5f127c18/blob)

\
(12) 데이터베이스 생성 버튼 클릭   //약 10분 소요

<figure><img src="https://lh5.googleusercontent.com/F4A-tGUFten-dLIXfB9TBzJIG05pKZwjn4rRum-1I6bVyctrsAtS_D21ggTORcjqN5boqQevOM2oKH2AdgWqc2gdX5TvFbvcvrsY8TpoTGEEkk9UFwpH1zg-fndJ6vR-q9PN6txjlEydrNJXaVajrPrv2AJ_nOmImdYdAyI_WgITqR4zWxTSY4fzDA" alt=""><figcaption></figcaption></figure>

&#x20;

(13) 연결 세부정보 보기  <mark style="color:yellow;">//마스터 암호는 Copy해서 보관해야 합니다.</mark>

<figure><img src="https://lh4.googleusercontent.com/6Q1lv2fzPRnCbBemMnvRE9fuSyrLcDJa8ANaLZYD4sQTIXyF7_1omaablIXlYpsleyWwkEeBcUphs0_BO7tJmoWOtTNBv1hEG7owG-PjUSrRnDrRy9uqa9I0fPGMsthrF0apJKKkJmMZTmbtoJgw97_zgEFG5XhRzLKqE3hm-bo4iG2S7F6Q9pbzVQ" alt=""><figcaption></figcaption></figure>

&#x20;

(14) DB 생성 완료 후 3가지 정보 확인

* 마스터 사용자 이름 (PROD\_DB\_USERNAME) admin
* 마스터 암호 (PROD\_DB\_PASSWORD) Y4KieiWb71KbGqNlH14y
* 엔드포인트 (PROD\_DB\_HOST) saju-db-prod.cbfdf2pmg9gq.ap-northeast-2.rds.amazonaws.com

&#x20;

(15) 태그

RDS 는 생성이 완료된 이후에 태그를 추가 할 수 있습니다.

Name : saju-db-prod

Service : saju-prod

![](https://cdn.inflearn.com/public/files/courses/329624/units/129027/c81927bc-0b97-4c2b-b14a-0c4082539d3c/blob)
