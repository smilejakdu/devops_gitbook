# 백엔드 실행 & 프론트엔드 설정



## :books: 백엔드 실행

**4-4) 백엔드 실행**

* 로드밸런서 주소 실행

`saju-alb-prod-1406545011.ap-northeast-2.elb.amazonaws.com`

* 로드밸런서를 브라우저 주소 입력창에서 실행하면 정상적으로 동작하는 경우 prod : working! 메시지를 확인 할 수 있습니다.
* 로드밸런서 주소가 503 에러 발생시 대상 그룹의 등록된 대상 확인 필요&#x20;
* 로드밸런서와 EC2의 AZ가 다른 경우 503이 발생합니다.

<figure><img src="https://lh6.googleusercontent.com/qB44Dtunmt5J4oXk4u-j2nA8chJElWekH9jO_cAaQCG8TxuiJVgEsYWnwS-_1z0AlU6rcZeeofYBoyk8iH7S_aB_uNoOrFjG-FfPSgW-pXF5PAWSc8zYtAEGnbQFBh6wULTkSSAd1S4trmALLSr_uMQLJjFocwa_7-9RpNagEZStoDh1IFJbNVeoVg" alt=""><figcaption></figcaption></figure>



## :books: 프론트엔드 빌드

백엔드 로드밸런싱 적용하게 되면 , 주소가 ip 주소에서 로드밸런싱 dns 주소로 변경이 됩니다.

그래서 프론트엔드에서 경로를 변경해줘야합니다.

**4-5) 프런트엔드 빌드**&#x20;

* 파일 위치  : src/api/index.js

(1) production 환경에서 로드밸런서 주소를 설정

<figure><img src="https://lh5.googleusercontent.com/vbzULlT_-Lnq8qqTyOGYwwxEMtSHVz_fL2yjDN3CR0ef0Xxk05nQzzWo4szBa-a0pvstmEXjLgxRLp0cFzkax2j8FOMFAfl0VbIToy8EpF_lZ9dPWQQRvKLD5WB-Gry_05hRkTpqS_b0psgNOBrD-hFqiXKtdBbKNpkLdDQA3gGoIluVTvoPocE4ZQ" alt=""><figcaption></figcaption></figure>

```javascript
import axios from 'axios';

export default process.env.NODE_ENV == 'production'
    ? axios.create({
        // production 환경 ( AWS ALB 주소 )
        baseURL: 'http://로드밸런서 주소',
    })
    : axios.create({
        // development 환경
        baseURL: 'http://localhost:3000',
    });
    
```

&#x20;

(2) 빌드

* npm run build

npm run build 를 하면 dist 폴더에 css, js 폴더, index 파일이 생성됩니다.



## :books: 프론트엔드 S3 배포

**4-6) 프런트엔드 S3 배포**

* 위치 : S3 > 버킷 > saju-client-prod

&#x20;

(1) 객체에서 업로드 버튼을 클릭합니다.

(2) dist 폴더의 파일 4개를 드로그앤드랍으로 업로드 합니다.



`aws cli` 를 통해서 배포를 진행해도 된다.

`aws s3 sync ./dist s3://saju-client-prod`

이 명령어는 현재 디렉토리의 dist 폴더 내 모든 파일을 saju-client-prod 라는 이름의 s3 버킷에 동기화 합니다.





## :books: 프론트엔드 실행

**4-7) 프런트엔드 실행**

* S3 속성 - 정적 웹 사이트 호스팅에 버킷 웹 사이트 엔드포인트 주소로 접속
* http://saju-client-prod.s3-website.ap-northeast-2.amazonaws.com
* 크롬에서 F12 후 Network 탭을 클릭 후 Request URL를 보면 로드밸런서 주소로 프런트와 백엔드가 통신하는 것을 알 수 있습니다.

<figure><img src="https://lh6.googleusercontent.com/Zs2P2vccfkXW7I0VuE1GzJylDzFfsgUxjusTnMr6IlCMAM3ZrHc7x1GmTt46CqQ4Gfl0oLlKzEsFusDHOGjChJig3_cLxgFQjVJSbhzqeCBisSP9HCihGJvejxdnUJHCsl01I1H1oh-AK8EXqjIeOL-9lyTYHBNVaMBPntCPVus_Yy1IfnoY1s1wRQ" alt=""><figcaption></figcaption></figure>

&#x20;
