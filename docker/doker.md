# doker 중단

1. **모든 컨테이너 중지**:
   *   먼저, 모든 실행 중인 컨테이너를 중지합니다. 이를 위해 다음 명령어를 사용합니다:

       ```bash
       docker stop $(docker ps -aq)
       ```
   * `docker ps -aq` 명령어는 모든 컨테이너의 ID를 나열하며, `docker stop` 명령어는 이러한 ID를 사용하여 모든 컨테이너를 중지합니다.
2. **모든 컨테이너 삭제**:
   *   모든 컨테이너를 삭제하려면 다음 명령어를 사용합니다:

       ```bash
       docker rm $(docker ps -aq)
       ```
   * 이 명령어는 중지된 모든 컨테이너를 삭제합니다.

