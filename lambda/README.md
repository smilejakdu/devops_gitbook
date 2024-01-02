# Lambda

{% embed url="https://www.serverless.com/framework/docs/getting-started/" %}

글이 되게 많지만 무엇이든 공식문서가 최고인것 같다.

서버리스 책을 구입해도 되지만 우선 제일 먼저 공식문서를 먼저 보고 나서&#x20;

다른 사람들은 어떻게 사용하고 있는지 궁금해 질때 , 그때 책을 사서 구입하는게 좋다.



## 배포

* 전체 배포 : sls deploy
* 특정 function 만 배포 : sls deploy function -f my-api
  * `-f [function name in serverless.yml]`



## 테스트

배포 하고나서 lambda serverless 에서 TEST 진행 가능합니다

그 전에 로컬에서 테스트를 우선 하는것을 권장합니다.

<mark style="background-color:blue;">sls invoke local -f app</mark>

위의 명령어로 로컬에서 테스트를 진행할 수 있다.

