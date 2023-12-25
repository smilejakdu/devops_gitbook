# 백엔드 실행



**4-4) 백엔드 실행**

* 로드밸런서 주소 실행

saju-alb-prod-1406545011.ap-northeast-2.elb.amazonaws.com

* 로드밸런서를 브라우저 주소 입력창에서 실행하면 정상적으로 동작하는 경우 prod : working! 메시지를 확인 할 수 있습니다.
* 로드밸런서 주소가 503 에러 발생시 대상 그룹의 등록된 대상 확인 필요&#x20;
* 로드밸런서와 EC2의 AZ가 다른 경우 503이 발생합니다.

<figure><img src="https://lh6.googleusercontent.com/qB44Dtunmt5J4oXk4u-j2nA8chJElWekH9jO_cAaQCG8TxuiJVgEsYWnwS-_1z0AlU6rcZeeofYBoyk8iH7S_aB_uNoOrFjG-FfPSgW-pXF5PAWSc8zYtAEGnbQFBh6wULTkSSAd1S4trmALLSr_uMQLJjFocwa_7-9RpNagEZStoDh1IFJbNVeoVg" alt=""><figcaption></figcaption></figure>
