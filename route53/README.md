# Route53

Route53 은 무엇인가요?&#x20;

Domain Name System (DNS) 웹 서비스입니다. 이 서비스는 인터넷 트래픽을 사용자의 인프라에 효율적으로 라우팅하는 데 사용됩니다.&#x20;



AWS Route 53에서 사용되는 DNS 레코드 유형인 A, NS, SOA, CNAME에 대해 설명해드리겠습니다:

#### 1. A 레코드 (Address Record)

* **목적**: 도메인 이름을 해당하는 IP 주소로 매핑합니다. 즉, 웹 브라우저나 다른 클라이언트가 도메인 이름을 입력할 때, A 레코드가 해당하는 IP 주소로 사용자를 안내합니다.
*   **예시**: `example.com` → `192.0.2.123`\
    \
    `로드밸런싱에 연결 할 수도 있다.`\


    <figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오전 10.55.50 (1).png" alt=""><figcaption></figcaption></figure>

    이렇게 연결 하면 된다.\
    생성하고 나서 \
    ![](<../.gitbook/assets/스크린샷 2023-12-21 오전 10.59.54.png>)\
    \
    복사해서 https 를 적용하기위해 https://dev.example.com 으로 들어가게 되면 \
    ![](<../.gitbook/assets/스크린샷 2023-12-21 오전 11.02.25.png>)\
    \
    이렇게 에러가 발생한다. -> 로드밸런서 -> 리스너 -> 리스너 추가 버튼 클릭 \
    \
    \


    <figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오전 11.28.49.png" alt="" width="281"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오전 11.04.16.png" alt="" width="375"><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/스크린샷 2023-12-21 오전 11.04.44.png" alt="" width="375"><figcaption></figcaption></figure>

적용하고 나서 다시 새로고침하면 됩니다. !&#x20;

#### 2. NS 레코드 (Name Server Record)

* **목적**: 특정 도메인에 대한 이름 서버(Name Server)의 정보를 제공합니다. 이 레코드는 도메인의 DNS 쿼리를 처리할 서버를 지정합니다.
* **예시**: `example.com`의 DNS 쿼리를 처리할 이름 서버는 `ns-123.awsdns-45.com`, `ns-678.awsdns-90.net` 등입니다.

#### 3. SOA 레코드 (Start of Authority Record)

* **목적**: DNS 존(Zone)의 권한 있는 시작점을 나타냅니다. SOA 레코드는 해당 DNS 존의 기본 설정을 포함하며, 존의 기본 이름 서버, 도메인 관리자의 연락처, 존 파일의 새로 고침 및 재시도 간격 등의 정보를 제공합니다.
* **예시**: `example.com`에 대한 SOA 레코드는 존의 권한 있는 이름 서버, 관리자의 이메일, 시리얼 번호 등의 정보를 포함합니다.

#### 4. CNAME 레코드 (Canonical Name Record)

* **목적**: CNAME(Canonical Name) 레코드는 하나의 도메인 이름을 다른 도메인 이름으로 매핑합니다. 즉, 사용자가 한 도메인 이름을 요청했을 때, 다른 도메인 이름으로 리다이렉트하도록 설정합니다.
* **예시**: `www.example.com`을 `example.com`으로 매핑할 수 있습니다.\
  레코드 이름이 test.example.com 이고, 값이 test.example.co.kr 로 설정된 CNAME 레코드는 다음을 의미합니다:\
  \
  test.example.co.kr 은 대상 도메인 또는 실제 도메인 입니다. \
  test.example.com 을 통해 접근할 때 실제로 연결 되는 주소이다.\
  \
  사용자가 웹 브라우저에 test.example.com 을 입력하면, DNS 시스템은 CNAME 레코드를 조회합니다. \
  DNS 는 test.example.com 이 test.example.co.kr 로 매핑되어 있음을 확인하고, 사용자를 test.example.co.kr 로 리다이렉트 합니다.\
  \
  결과적으로 사용자는 test.example.com 을 요청했지만, test.example.co.kr 의 컨텐츠를 받게됩니다.\
  \
  A 레코드와 CNAME 레코드는 주로 웹 트래픽을 관리하는데 사용되며, NS 와 SOA 레코드는 도메인의 DNS 관리에 필수적입니다. 이러한 레코드들은 서로 다른 목적과 기능을 가지며, 함께 작동하며 인터넷의 도메인 이름 시스템을 원활하게 유지합니다.
