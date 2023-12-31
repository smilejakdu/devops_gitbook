# docker 삭제



## 모든 docker container 검색

```bash
docker ps -a
```

## docker 모든 container 삭제

```bash
docker rm $(docker ps -aq)
```

모든 container 를 삭제한다.

## docker image 삭제

Docker에서 모든 이미지를 삭제하려면 Docker CLI의 명령어를 사용할 수 있습니다. 다만, 모든 이미지를 삭제하기 전에 중요한 이미지가 없는지, 혹은 백업이 필요한 이미지는 없는지 확인하는 것이 중요합니다. 이미지를 한 번 삭제하면 복구가 불가능할 수 있으므로 주의가 필요합니다.

모든 Docker 이미지를 삭제하는 방법은 다음과 같습니다:

1.  **모든 이미지 목록 보기**:

    ```bash
    docker images -a
    ```

    이 명령은 시스템에 있는 모든 Docker 이미지의 목록을 표시합니다.
2.  **모든 이미지 삭제**:

    ```bash
    docker rmi $(docker images -a -q) -f
    ```

    * `docker images -a -q`는 모든 이미지의 ID를 나열합니다.
    * `docker rmi`는 이미지를 삭제하는 명령입니다.
    * `-f` 플래그는 강제 삭제를 의미합니다.

#### 주의사항:

* 이미지를 삭제하기 전에 해당 이미지들이 더 이상 필요하지 않은지 확인하세요.
* 사용 중인 컨테이너에 의존하는 이미지는 삭제할 수 없습니다. 먼저 해당 컨테이너를 삭제하거나 정지해야 합니다.
* 이미지를 삭제하면, 나중에 다시 사용하려면 재다운로드해야 합니다. 따라서 삭제하기 전에 해당 이미지가 정말로 필요하지 않은지 확인하는 것이 중요합니다.

이러한 명령을 통해 Docker 시스템 내의 모든 이미지를 삭제할 수 있지만, 이 과정은 되돌릴 수 없으므로 신중하게 수행해야 합니다.





## docker container 삭제

삭제 하기 전에 먼저 stop 이 돼있는지 확인해야한다.



