# MySQL 접속 연결



## 디비를 public 에 뒀을때&#x20;

**1-3) MySQL Workbench 접속**

(1) 연결 설정

<figure><img src="https://lh6.googleusercontent.com/A19WMK87g38nnT5q2wf906cFsSnUoUl_qgEThxy2Cwc0eSR9aAr27g_WHV7jWpdWvfaBmSP1YwU5yPgTmbuDTGRcTNmWhaeumVZunpj747fw7UpV83_WCXPDtM3k0vlHoNcDMw3ad4z_UaKasd1VBFSKCFCROmP8W6x2cipNisaQJPbV5dUs8f48rg" alt=""><figcaption></figcaption></figure>

* Test Connection으로 연결이 성공했는지 확인

<figure><img src="https://lh5.googleusercontent.com/jq6oCfj8B_JdkJjpm2K6DDAltVNO6W96vocs09SOmWGahkRO3oRtUOrZ5W_fTz6j24u3_R117wOsOVA1w1eg04GTRpd2e1hrk2AS_HNbNN3NVoCrw60LqGsPampDTu1GSnvuy2MfF6p0mhcibxAA_hFof8SJ6RiFQ0OZuAy0t32AXF2f8dcWImVg7w" alt=""><figcaption></figcaption></figure>

&#x20;

(2) 데이터베이스 스키마 생성

* &#x20;saju\_db\_prod  (PROD\_DB\_DATABASE)&#x20;

<figure><img src="https://lh5.googleusercontent.com/CcUAxp8To4Zakejr2ecy5792lzrd8OaLmtDVLOFc74Iu9WR3KETKU67K4tpvZ_Gmvo5r3lLKF2vwPAr2Ik0e5f0yBl7UyjF377c9GKs2qtzPVD_l7x905pILQQLYc4J-0P8qSZCz7J0ZUGSqkNlQp38mQHuROaJ5uvaIhTk2ooX1K-6Wcp7JDD_mcA" alt=""><figcaption></figcaption></figure>

&#x20;

(3) 사주 DB 덤프

* NodeJS : https://github.com/vipick/saju-backend-nodejs
* MySQL Workbench 접속&#x20;
* Administartor 클릭
* Data Import 클릭
* Import from Self-Containered File 선택
* NodeJS 소스코드 폴더에서 mysql/sqls/saju-db-prod.sql 를 선택&#x20;
* 데이터베이스(saju\_db\_prod)를 선택&#x20;
* start import

<figure><img src="https://lh3.googleusercontent.com/AfELQyXBeWZgImwhcHwQf4g9BApCOgdgP5rSB_c3QAU7augBF5fKolz4JO0txdcIgGps_IWVorY0N8_X7eFITXBYnOX8KxxqPX9sMsfaOEQg42Vy0FFuKUCExDq9j0_sPSNOEXARGFT3FJg1zUfGuqofAYJHyaASUiuYLBOHeEE8z64SAdBpBQrekw" alt=""><figcaption></figcaption></figure>



위는 public 을 뒀을때 접근이 가능하다.&#x20;



## 디비를 private 에 뒀을때&#x20;



디비의 보안성을 고려하면 private subnet 에 둘때가 많다.

private subnet 에 존재하는 디비는 host , user , password 를 알고있다고해서 곧바로 접근이 불 가능하다.

bation 을 통해서 접근을 하거나 open vpn 이나 SSM 으로 접근하게 된다.

#### Bation 으로 활용할 경우

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-23 오후 1.07.56.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-23 오후 1.09.13.png" alt=""><figcaption></figcaption></figure>

public 으로 접근 가능한 인스턴스를 하나 생성한다.

이후 pem 키를 활용해서 위의 인스턴스에 접속을 한다.&#x20;

`chmod 600 test.pem`

권한 설정을 해주고 `ssh dev-bation-instacne`

접속하게 되면 bation 으로 보안그룹설정했던 녀석들은 접속을 할 수 있다.

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-23 오후 1.14.29.png" alt=""><figcaption></figcaption></figure>

