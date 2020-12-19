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
> `mongo --username root --password example`

### DB
> * database list 보기: > `show dbs`
> * database 사용: > `use <database>`
> * 종료: > `exit`
> * connection url: `mongodb://<id>:<password>@<ip>:<port>/<dbname>?authSource=admin`   
> * 예시: `mongodb://root:example@localhost:27017/nodepractice?authSource=admin`

## query
### find
> 데이터베이스가 `dev` 이며 테이블이 `user` 의 모든 데이터 조회 
> ```shell
> use dev
> db.user.find()
> ```
