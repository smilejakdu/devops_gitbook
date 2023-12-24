# S3 를 이용한 배포

## CSR

S3(simple storage service)는 파일 저장소이지만, 프런트엔드를 정적 웹호스팅을 배포하는데 사용할 수 있습니다.

프런트엔드 중 CSR (Client Sider Rendering)를 배포하는데 사용합니다.

**3-1) S3 생성**

* 위치 : S3 > 버킷

(1) 버킷 생성

* 버킷 이름 : saju-front-prod (<mark style="background-color:purple;">버킷 이름은 고유해야 합니다</mark>. 예: saju-front-prod-0723)
* AWS 리전 : ap-northeast-2 서울

![](https://cdn.inflearn.com/public/files/courses/329624/units/128987/012b8015-ba46-4ddb-9383-505416e73e63/blob)

(2) 모든 퍼블릭 엑세스 차단 해제

웹 페이지 (프런트)를 배포하는 것이기 때문에 모든 퍼블릭 엑세스 차단 해제 후 사용자가 접근할 수 있도록 합니다.

* 경고 문구에 체크

현재 설정으로 인해 이 버킷과 그 안에 포함된 객체가 퍼블릭 상태가 될 수 있음을 알고 있습니다.

<figure><img src="https://lh5.googleusercontent.com/XpV8jrLkTkPDkX96EtdKhVhUmFXAxguYxWzdIbFovO01GOtZ4rx--sBHctTz_FBpfPvA8AlvANayVa1-VhF-LGFg_uU6eM517Y7ShB0hvO0Dm1b0GJOw3FtU_KAzif_FtZjDiBj0fkxZO8G0cGxiKx0z3ZGcoS91Y0CwNfNnsskfq9TwaWh2rXBgTA" alt=""><figcaption></figcaption></figure>

(3) 태그 추가

![](https://cdn.inflearn.com/public/files/courses/329624/units/128987/87ee9963-709b-45f8-b243-c5a175bd955d/blob)

## 정적 웹 호스팅

**3-2) 정적 웹 호스팅**

(1) 정적 웹 사이트 호스팅 편집 이동

* 속성 탭 클릭
* 정적 웹 사이트 호스팅 편집 버튼 클릭

![](https://cdn.inflearn.com/public/files/courses/329624/units/128988/23fc1ad6-9205-4dfe-80f1-74c7a33794c0/blob)

![](https://lh5.googleusercontent.com/Z7vHjcMuo85Xr3PRrPqSauESzsizEkziOfjb3LJseTUlMls9MSVan9BpFd78t\_lFbo5aOgsfya27uY1hfHubVZ4xicgtP62nrxKaGIXZ0fqGehN3ws80dRmXcfUxg2tsu6ETUOOitsUMy01jBSAlgCY5koYTON1KYNYfUtE2igRlpzEdJ9xgNqXnuw)

&#x20;

(2) 정적 웹 호스팅 편집

* 정적웹호스팅 : 활성화
* 호스팅 유형 : 정적 웹 사이트 호스팅
* 인덱스 문서 :  index.html&#x20;
* 오류 문서 : **index.html**

![](https://cdn.inflearn.com/public/files/courses/329624/units/128988/a47b9be9-b1fb-4f80-b0e7-082f6677f67d/blob)

(3) 버킷 웹 사이트 엔드포인트 주소 확인

* http://saju-front-prod.s3-website.ap-northeast-2.amazonaws.com

![](https://cdn.inflearn.com/public/files/courses/329624/units/128988/adadd366-21f6-419a-8faf-8e613844b59a/blob)

(4) 버킷 정책 편집

* 권한 탭 클릭
* statement의 resource에 버킷 명 saju-front-prod 으로 수정

```markdown
{
 "Version": "2012-10-17",
 "Id": "Policy1546621853468",
 "Statement": [
  {
   "Sid": "Stmt1546621828605",
   "Effect": "Allow",
   "Principal": "*",
   "Action": "s3:GetObject",
   "Resource": "arn:aws:s3:::saju-front-prod/*"
  }
 ]
}
```

&#x20;

![](https://cdn.inflearn.com/public/files/courses/329624/units/128988/f5688e53-5052-4dae-8126-ca32c2f4c0d2/blob)

## 프런트엔드 빌드

**3-3) 프런트엔드 빌드**

(1) 소스코드 다운로드

* https://github.com/vipick/saju-frontend-vuejs

(2) production 환경에서 EC2 퍼블릭 IP 주소와 3000포트를 설정

* 파일 위치 : <mark style="background-color:purple;">/src/api/index.js</mark>

<figure><img src="https://lh3.googleusercontent.com/CpDDvxf7Ch4YyHtydt8GSKuBeJNE7YBV6___0quX8HHUL82xvsIcmXisZSVATEhHQ65-T4qAWmKn5x9rY95XlIYTDLH7sUSYmqWSbIFsOT5kqvAli4d2pSkNmwPlXgYdY8feC5338dAXzW4jh7t-mDeroaJD62dM-I2j1U5bh2IrdnuJmPJt5c9SQw" alt=""><figcaption></figcaption></figure>

```javascript
import axios from "axios";

export default process.env.NODE_ENV == "production"
  ? axios.create({
      //production 환경 (AWS EC2)
      baseURL: "http://EC2 퍼블릭 IP 주소:3000",
    })
  : axios.create({
      //development 환경
      baseURL: "http://localhost:3000",
    });
```

(3) npm 설치

* npm install

(4) 빌드

* npm run build

npm run build 를 하면 dist 파일에 css, js 폴더, index 파일이 생성됩니다.

## Frontend S3 배포

**3-4) 프런트엔드 S3 배포**

* 위치 : S3 > 버킷 > saju-client-prod (앞에서 생성한 버킷 명을 사용합니다)

(1) 객체에서 업로드 버튼을 클릭합니다.

<figure><img src="https://lh4.googleusercontent.com/AO7bSAU2fOkEkrTGSwY93jLHtkVKRhiDyYil4w5EGaljDYZzAFb0K6IGT23vsJSLboayiZciQsNS8UvXPSImLR7ZWtf3PTFUWdk8VuHRWS65P6b77ER38A3oKqGYzdCRBP-8ZtuT7fYlXuTeTrpqQ7r58832M_VRMgyo9LjRCfwWRxxQU9qtQsEh_Q" alt=""><figcaption></figcaption></figure>

(2) dist 폴더의 파일을 4개를 드로그앤드랍으로 업로드 합니다.

<figure><img src="https://lh3.googleusercontent.com/X6G_hX5wZz4GpcfQd8Jf2JEln5SP0NRpW7hZgsnCuIA8b1a5AxkSYWc8oRv0aig5J9cyVrMMAx6zrztXcWXTr571PpFZ3uCPaEz_0IhH1K8WEbsE5mkURCh7sj74OCuR8RgiWCclsKrS8YB9FRHJBAnfJ3i3Qjl4S80dqdYTHLZ78D_VRs6_3pGMFA" alt=""><figcaption></figcaption></figure>

(3) 업로드 파일 및 폴더 확인

<figure><img src="https://lh3.googleusercontent.com/uAxF6Tq8qN4S7tQE7MEC3Od3kfE_s6NPN2DADe69oq6FQ3-szBaQLCmDJXgAXPrtHpG_4WLDauLuRzO7b1mD1wZCOzv997SHYFIDxJzb2rY61XUaWGXoPbJGZAenH6WgVMtihA4ykLnDhoQmv_T5e65O2Yl6gB_98Z9pOKceOB3VQMngURXMNTaxuw" alt=""><figcaption></figcaption></figure>

## Frontend 실행

**3-5) 프런트엔드 실행**

* S3 속성 - 정적 웹 사이트 호스팅에 버킷 웹 사이트 엔드포인트 주소로 접속
* http://saju-client-prod.s3-website.ap-northeast-2.amazonaws.com
* 크롬에서 F12 후 Network 탭을 클릭 후 Request URL를 보면 퍼블릭 ip 주소로 프런트와 백엔드가 통신하는 것을 알 수 있습니다.

<figure><img src="https://lh6.googleusercontent.com/IMX8PMpZzMC8eitTZnuSySFCSKXBdwMOl9l-U8pVjqkX3WkhHgowuGWA0JJ8Rwyz6ykboYGI-ILYbwDMLyDemzI5m_9H3KtOd0F_Sz5JMQC9o7j89PAahEGISSDLiPVLwNHC1H6K_HB3HUNBYBWLP68KYs6IYIElxXMn79NfrX388PjZDIVtKxI-KA" alt=""><figcaption></figcaption></figure>

## Frontend 버전 관리 (롤백)

![](https://cdn.inflearn.com/public/files/courses/329624/units/174876/5f184e46-c2d5-4798-a6dd-3d97ffe817d0/blob)

* 프런트엔드 배포를 했는데, 이전 버전으로 돌리고 싶은 경우 <mark style="background-color:purple;">index.html 파일</mark> 만 삭제하면 됩니다.
* 삭제를 하는 경우 <mark style="background-color:purple;">가장 최신 index.html 버전</mark>으로 돌립니다.&#x20;

![](https://cdn.inflearn.com/public/files/courses/329624/units/174876/80821802-f0b1-4e77-98d2-b96357dc94bf/blob)

* 속성에서 버킷 버전 관리를 활성화로 바꿉니다.\
  \


