# 여러 개의 컨테이너를 연동해 실행해보자

## 워드프레스 구축

### 도커 네트워크 생성/삭제

- 워드프레스는 웹 사이트 작성자가 작성한 내용을 데이터베이스에 저장하고, 웹 사이트 열람자의 요청에 따라 웹 페이지를 보여준다.

- 워드프레스가 MySQL에 저장된 데이터를 읽고 쓸 수 있어야 하기 떄문에 <strong>두 컨테이너가 연결</strong>돼 있어야 한다.

- 가상 네트워크를 만들고 이 네트워크에 두 개의 컨테이너를 소속시켜 두 컨테이너를 연결한다.

- 도커 네트워크를 생성/삭제하는 커맨드
    ```bash
    # 생성
    docker network create $NETWORK_NAME

    # 삭제
    docker network rm $NETWORK_NAME
    ```

- 도커 네트워크 관련 커맨드

    | 커맨드 | 내용 |
    | --- | --- |
    | connect | 네트워크에 컨테이너를 새로이 접속 |
    | disconnect | 네트워크에서 컨테이너의 접속을 끊음 |
    | create | 네트워크를 생성 |
    | inspect | 네트워크의 상세 정보를 확인 |
    | ls | 네트워크의 목록을 확인 |
    | prune | 현재 아무 컨테이너도 접속하지 않은 네트워크를 모두 삭제 |
    | rm | 지정한 네트워크를 삭제 |

<br />

## 워드프레스 및 MySQL 컨테이너 생성과 연동

### 실습

- 네트워크 생성
    ```bash
    docker network create $NETWORK_NAME
    ```

- MySQL 컨테이너 생성 및 실행
    ```bash
    docker container run --name $CONTAINER_NAME -dit --net=$NETWORK_NAME -e MYSQL_ROOT_PASSWORD=$MYSQL_ROOT_PASSWORD -e MYSQL_DATABASE=$DATABASE_NAME -e MYSQL_USER=$MYSQL_USER_NAME -e MYSQL_PASSWORD=$$MYSQL_PASSWORD mysql --character-set-server=$CHARACTER_ENCODING --collation-server=$SORTING_ORDER --default-authentication-plugin=$CERTIFICATION_METHOD
    ```

- 워드프레스 컨테이너 생성 및 실행
    ```bash
    docker run --name $CONTAINER_NAME -dit --net=$NETWORK_NAME -p $PORT_SET -e WORDPRESS_DB_HOST=$DATABASE_CONTAINER_NAME -e WORDPRESS_DB_NAME=$DATABASE_NAME -e WORDPRESS_DB_USER=$DATABASE_USER_NAME -e WORDPRESS_DB_PASSWORD=$DATABASE_PASSWORD wordpress
    ```