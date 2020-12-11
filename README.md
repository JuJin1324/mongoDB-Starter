# mongoDB-Starter
mongoDB 사용을 위한 시작 안내

## 설치
### Docker
> docker-compose.yml
> ```yml
> version: '3'
> services:
>  mongo:
>    container_name: mongo-local
>    image: mongo:4.0.21
>    ports: 
>      - 27017:27017
>    environment:
>      MONGO_INITDB_ROOT_USERNAME: root
>      MONGO_INITDB_ROOT_PASSWORD: example
>    volumes:
>      - 
>  
>  mongo-express:
>    container_name: mongo-express-local
>    image: mongo-express
>    restart: always
>    ports:
>      - 8081:8081
>    environment:
>      ME_CONFIG_MONGODB_ADMINUSERNAME: root
>      ME_CONFIG_MONGODB_ADMINPASSWORD: example
> ```
