# mongoDB-Starter

> mongoDB 사용을 위한 시작 안내

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

---

## MongoDB 학습 로드맵
### MongoDB의 기본 이해 및 RDBMS와의 비교 (기반 다지기)

> * 핵심 개념: 왜 NoSQL이 등장했는지, NoSQL 중에서도 MongoDB(문서 지향 NoSQL)가 어떤 특징을 갖는지 이해합니다.
>
> **주요 내용**
> * 정형/비정형/준정형 데이터 개념 복습 (방금 하신 것!)
> * CAP 이론 (Consistency, Availability, Partition Tolerance) 간단히 이해
> * RDBMS vs MongoDB:
> * 스키마 vs. 스키마리스(유연한 스키마)
> * 테이블 vs. 컬렉션
> * 행 vs. 문서(Document)
> * 조인 vs. 임베딩(Embedding) & 참조(Referencing)
> * SQL vs. MongoDB 쿼리 언어
>
> * MongoDB의 장점과 단점, 어떤 경우에 MongoDB가 적합한가?

### MongoDB 설치 및 기본 환경 설정 (실습 준비)

> * 핵심 개념: 로컬 환경에 MongoDB를 설치하고 기본적인 관리 도구를 사용해봅니다.
>
> **주요 내용**
> * MongoDB Community Edition 다운로드 및 설치 (운영체제에 맞게)
> * MongoDB 서버 실행 및 중지
> * mongosh (또는 이전 버전 mongo) 쉘 사용법 익히기
> * 데이터베이스(Database) 생성, 확인, 삭제
> * 컬렉션(Collection) 생성, 확인, 삭제

### Step 3: CRUD (Create, Read, Update, Delete) 기본 작업 (가장 중요!)

> * 핵심 개념: 데이터를 MongoDB에 저장하고, 읽고, 수정하고, 삭제하는 가장 기본적인 방법을 익힙니다. RDBMS의 INSERT, SELECT, UPDATE, DELETE에 해당합니다.
>
> **주요 내용**
> * Create: insertOne(), insertMany()
> * Read: find() (조건 없는 전체 조회), findOne() (하나 조회)
> * Update: updateOne(), updateMany(), replaceOne() (업데이트 연산자 $set, $inc, $push 등 사용법)
> * Delete: deleteOne(), deleteMany()
> * 데이터 타입: BSON 타입 (String, Integer, Double, Boolean, Array, Object, Date, ObjectID 등) 이해

### 데이터 모델링 (MongoDB스러운 설계)

> * 핵심 개념: RDBMS와는 다른 MongoDB의 문서 모델링 방식을 이해하고 적용합니다. 관계형 모델 사고방식에서 벗어나 문서 중심으로 생각하는 연습이 필요합니다.
>
> **주요 내용**
> * 문서 구조 설계 (Nested Document, Array of Documents)
> * 임베딩(Embedding) vs. 참조(Referencing): 각각의 장단점 및 사용 사례 분석 (언제 임베딩하고 언제 참조할까?)
> * 단방향/양방향 참조 구현 방법
> * 데이터 정규화(Normalization) vs. 비정규화(Denormalization) 관점에서 바라보기

### 쿼리 및 필터링 심화 (데이터 조회 마스터)

> * 핵심 개념: 원하는 데이터를 효율적으로 조회하기 위한 다양한 쿼리 연산자와 기법을 익힙니다.

> **주요 내용**
> * 쿼리 연산자 상세 학습 ($eq, $ne, $gt, $lt, $gte, $lte, $in, $nin, $and, $or, $not, $nor, $exists, $type, $regex, $size, $
> * elemMatch 등)
> * 정렬 (sort())
> * 결과 제한 (limit()) 및 건너뛰기 (skip()) (페이징 처리)
> * 필드 선택 (projection, 특정 필드만 가져오기)
> * 커서(Cursor) 개념 이해

### 인덱싱 (성능 최적화의 핵심)

핵심 개념: 쿼리 성능을 향상시키기 위해 인덱스를 사용하는 방법을 익힙니다. RDBMS의 인덱스와 개념은 유사하나, MongoDB만의 특징이 있습니다.
주요 내용:
인덱스의 필요성 및 동작 원리
인덱스 생성 및 삭제 (createIndex(), dropIndex())
다양한 인덱스 타입: 단일 필드, 복합(Compound), 멀티키(Multikey - 배열 필드 인덱싱), 텍스트(Text), 지리 공간(Geospatial), TTL(Time To Live) 인덱스
쿼리 플랜 분석 (explain())을 통해 인덱스 사용 확인 및 성능 튜닝

### Aggregation Framework (복잡한 데이터 집계 및 변환)

> * 핵심 개념: 여러 문서를 그룹화하고 집계하며 데이터를 변환하는 고급 쿼리 기법입니다. RDBMS의 GROUP BY, 조인, 서브쿼리 등과 유사한 기능을 파이프라인 형태로 제공합니다.
>
> **주요 내용**
> * Aggregation Pipeline 개념 이해
> * 주요 Stage 학습:
> * $match (필터링)
> * $project (필드 선택/변환)
> * $group (그룹화 및 집계 연산자 $sum, $avg, $count 등)
> * $sort (정렬)
> * $limit, $skip (페이징)
> * $lookup (컬렉션 조인)
> * $unwind (배열 분해)
> * Aggregation 사용 예제 실습

### 고급 개념 및 관리 (운영 지식)

> * 핵심 개념: 실제 서비스 운영에 필요한 고가용성, 확장성, 일관성 등의 개념을 이해합니다.
>
> **주요 내용**
> * Replica Set: 고가용성 및 데이터 이중화 (Master-Slave 개념과 유사하지만 더 발전된 형태)
> * Sharding: 수평적 확장성 (대규모 데이터 분산 저장 및 처리)
> * 읽기/쓰기 Preference (어떤 노드에서 읽고 쓸지 설정)
> * Write Concern & Read Concern (쓰기/읽기 일관성 수준 설정)
> * 트랜잭션 (Multi-document Transaction - 최근에 추가됨, 중요 개념)
> * 데이터 검증 (Schema Validation)
> * 보안 (인증, 권한 부여)
> * 백업 및 복구

### Java/Spring Framework 연동 (실제 개발 적용)

> * 핵심 개념: 배운 MongoDB 지식을 자바 스프링 환경에서 활용합니다.
>
> **주요 내용**
> * MongoDB Java Driver 사용법 (로우 레벨 접근)
> * Spring Data MongoDB 사용법 (추천!)
> * 설정 및 의존성 추가
> * MongoTemplate을 이용한 저수준 CRUD/쿼리
> * Repository 인터페이스를 이용한 고수준 CRUD/쿼리 (JPA와 유사)
> * @Document, @Id, @Field 등 애노테이션 사용법
> * 쿼리 메소드, @Query 애노테이션
> * Aggregation 파이프라인 구현

---

