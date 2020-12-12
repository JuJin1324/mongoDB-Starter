# mongoDB-Starter
mongoDB 사용을 위한 시작 안내

## 설치
### Docker
> docker-compose.yml  
> * mongo: mongoDB 서버
> * mongo-express: mongoDB 서버 상태 체크를 웹에서 할 수 있도록 해주는 클라이언트: http://localhost:8081 로 접속해서 상태 확인 가능 
> ```yml
> version: '3'
> services:
>  mongo:
>    container_name: mongo-27017
>    image: mongo:4.0.21
>    ports: 
>      - 27017:27017
>    environment:
>      MONGO_INITDB_ROOT_USERNAME: root
>      MONGO_INITDB_ROOT_PASSWORD: example
>      MONGO_INITDB_DATABASE: nodepractice
>    volumes:
>      - ./docker-volumes/mongodb-data:/data/db
>  
>  mongo-express:
>    container_name: mongo-express-8081
>    image: mongo-express
>    restart: always
>    ports:
>      - 8081:8081
>    environment:
>      ME_CONFIG_MONGODB_ADMINUSERNAME: root
>      ME_CONFIG_MONGODB_ADMINPASSWORD: example
> ```

### mongo CLI(Command Line Interface) client
> * macOS  
> ```
> brew tap mongodb/brew
> brew install mongodb-community-shell
> ```

### 접속
> `mongo`

### DB
> * database list 보기: > `db`
> * database 사용: > `use <database>`
> * 종료: > `exit`
