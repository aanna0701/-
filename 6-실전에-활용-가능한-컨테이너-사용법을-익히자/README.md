# 실전에 활용 가능한 컨테이너 사용법을 익히자

## 컨테이너와 호스트 간에 파일 복사하기

### 파일 복사

- 서버와 로컬 컴퓨터 간에 파일을 주고받아야 할 때가 있다.

- 파일 복사는 컨테이너 -> 호스트, 호스트 -> 컨테이너로 양방향 모두 가능하다.

- 파일 복사 커맨드

    ```bash
    # 컨테이너로 파일을 복사하는 커맨드
    docker cp $HOST_PATH $CONTAINER_NAME:$CONTAINER_PATH

    # 호스트로 파일을 복사하는 커맨드
    docker cp $CONTAINER_NAME:$CONTAINER_PATH $HOST_PATH
    ```

<br />


