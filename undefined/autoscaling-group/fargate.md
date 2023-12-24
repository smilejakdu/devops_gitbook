# Fargate 오토스케일링

EC2 에 비해 비교적 간단합니다.

* CloudWatch 경보(Alert)와 연동해서 특정 CPU 사용률 기준을 넘으면 스케일 아웃, 스케일 인이 되도록 동작합니다.
* ECS 서비스에서 설정 가능하며 배포 방식은 롤링 배포 방식을 따릅니다.



CloudWatch 에 경보 추가를 해줍니다.



* CloudWatch -> 경보 -> 경보생성
* 스케일 아웃에 대한 경보를 생성해줍니다.
  * 스케일 아웃에 대한 경보를 생성합니다. 스케일 업이 CPU나 메모리 성능을 올리는 반면에 스케일 아웃은 인스턴스의 갯수를 증가 시킵니다.
*   경보 생성

    * CloudWatch 의 경보에 경보 상태로 이동 후 경보 생성 버튼을 클릭합니다.
    *

        <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.45.03.png" alt=""><figcaption></figcaption></figure>

        생성을 클릭하면 지표 및 조건지정 -> 지표지정 선택
    *   &#x20;

        <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.45.38.png" alt=""><figcaption></figcaption></figure>

        <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.46.43.png" alt=""><figcaption></figcaption></figure>

        지표를 선택할때 ,
    *   &#x20;

        <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.47.32.png" alt=""><figcaption></figcaption></figure>

        지표이름이 CpuUtilized 를 선택한다.

    <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.49.16.png" alt=""><figcaption></figcaption></figure>

    <figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.49.59.png" alt=""><figcaption></figcaption></figure>

    작업구성 넘어가면 알림을 제거합니다. -> 제거하는 이유는 ?



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.51.32.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.52.13.png" alt=""><figcaption></figcaption></figure>

스케일 인에 대한 경보를 생성합니다.

스케일 아웃은 인스턴스의 갯수를 증가시키며, 스케일 인은 인스턴스의 갯수를 감소시킵니다.

트래픽이 줄어서 특정 스케일 인 조건을 만족하면 인스턴스의 갯수가 줄어듭니다.

이후 경보 생성 미리보기가 나오는데 경보 생성을 클릭해줍니다.



생성된 상태를 보려면 모든 경보에 들어가줍니다.

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.54.50.png" alt=""><figcaption></figcaption></figure>





scale-out, scale-in 모두 생성을 하게 되면

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 6.58.04.png" alt=""><figcaption></figcaption></figure>

이렇게 보이게 됩니다.



## ECS 클러스터





<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오후 1.24.19.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 7.13.49.png" alt=""><figcaption></figcaption></figure>

조정정책을 수정해줍니다.



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 7.15.12.png" alt=""><figcaption></figcaption></figure>

스케일 아웃을 작성했으면, 밑에 `더 많은 조정 정책 추가` 버튼을 클릭합니다.

<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 7.17.40.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 7.23.11.png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/스크린샷 2023-12-22 오전 7.19.24.png" alt=""><figcaption></figcaption></figure>



