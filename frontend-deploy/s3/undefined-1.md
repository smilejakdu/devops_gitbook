# 로드밸런서

* 로드밸런서는 서버의 트래픽을 대상그룹으로 분산 시켜줍니다.
* 여기서는 백엔드에 HTTPS를 적용하는데 사용합니다.



**4-5) 프런트엔드 빌드**&#x20;

* 파일 위치  : <mark style="background-color:purple;">src/api/index.js</mark>

(1) production 환경에서 로드밸런서 주소를 설정

<figure><img src="https://lh5.googleusercontent.com/vbzULlT_-Lnq8qqTyOGYwwxEMtSHVz_fL2yjDN3CR0ef0Xxk05nQzzWo4szBa-a0pvstmEXjLgxRLp0cFzkax2j8FOMFAfl0VbIToy8EpF_lZ9dPWQQRvKLD5WB-Gry_05hRkTpqS_b0psgNOBrD-hFqiXKtdBbKNpkLdDQA3gGoIluVTvoPocE4ZQ" alt=""><figcaption></figcaption></figure>

```javascript
import axios from "axios";

export default process.env.NODE_ENV == "production"
  ? axios.create({
      //production 환경 (AWS ALB 주소)
      baseURL: "http://로드밸런서 주소",
    })
  : axios.create({
      //development 환경
      baseURL: "http://localhost:3000",
    });
```

&#x20;

(2) 빌드

* npm run build

npm run build 를 하면 dist 폴더에 css, js 폴더, index 파일이 생성됩니다.



**4-6) 프런트엔드 S3 배포**

* 위치 : S3 > 버킷 > saju-client-prod

&#x20;

(1) 객체에서 업로드 버튼을 클릭합니다.

(2) dist 폴더의 파일 4개를 드로그앤드랍으로 업로드 합니다.



**4-7) 프런트엔드 실행**

* S3 속성 - 정적 웹 사이트 호스팅에 버킷 웹 사이트 엔드포인트 주소로 접속
* http://saju-client-prod.s3-website.ap-northeast-2.amazonaws.com
* 크롬에서 F12 후 Network 탭을 클릭 후 Request URL를 보면 로드밸런서 주소로 프런트와 백엔드가 통신하는 것을 알 수 있습니다.\


<figure><img src="https://lh6.googleusercontent.com/Zs2P2vccfkXW7I0VuE1GzJylDzFfsgUxjusTnMr6IlCMAM3ZrHc7x1GmTt46CqQ4Gfl0oLlKzEsFusDHOGjChJig3_cLxgFQjVJSbhzqeCBisSP9HCihGJvejxdnUJHCsl01I1H1oh-AK8EXqjIeOL-9lyTYHBNVaMBPntCPVus_Yy1IfnoY1s1wRQ" alt=""><figcaption></figcaption></figure>
