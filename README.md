RedisWrapper - Project Documentation
===================================
Overview
--------
RedisWrapper is a Spring Boot based lightweight Redis utility layer designed to provide simple
abstractions for key-value operations, caching, and distributed locking. It uses the Lettuce Redis
client and provides modular structure for integration into any microservice.
Architecture
------------
src/
├── main/java/com/redisWrapper/
│ ├── RedisWrapperApplication.java
│ ├── config/RedisConfig.java
│ ├── kv/
│ │ ├── RedisKV.java
│ │ ├── LettuceRedisKV.java
│ ├── cache/
│ │ ├── CacheHelper.java
│ │ ├── DefaultCacheHelper.java
│ ├── lock/
│ │ ├── LockClient.java
│ │ ├── SimpleLockClient.java
│ ├── web/
│ │ ├── SmokeController.java
│ │ ├── CacheController.java
└── resources/
 └── application.properties
Key Components
--------------
1. RedisConfig.java
 - Sets up Lettuce Redis connection and provides a StatefulRedisConnection bean.
2. RedisKV.java & LettuceRedisKV.java
 - Provides abstraction and implementation for key-value operations with optional TTL.
3. CacheHelper.java & DefaultCacheHelper.java
 - Implements caching with fallback loading and expiration support.
4. LockClient.java & SimpleLockClient.java
 - Distributed locking mechanism using Redis SETNX.
5. CacheController.java
 - REST API endpoints for testing cache operations:
 - POST /cache/set?key=KEY&value=VALUE&ttl=SECONDS
 - GET /cache/get?key=KEY
 - GET /cache/getOrLoad?key=KEY&fallback=VAL
Testing
-------
- CacheControllerTest.java: Tests REST endpoints using MockMvc.
- LettuceRedisKVTest.java: Unit tests for Redis key-value operations using Mockito.
Run tests:
 mvn clean test
JaCoCo Coverage
---------------
Add JaCoCo plugin to pom.xml and run:
 mvn clean test
View coverage report at:
 target/site/jacoco/index.html
Running the Application
-----------------------
1. Start Redis server:
 sudo service redis-server start
2. Verify Redis:
 redis-cli ping -> PONG
3. Run Spring Boot app:
 mvn spring-boot:run
4. Test API:
 POST http://localhost:8081/cache/set?key=k1&value=hello
 GET http://localhost:8081/cache/get?key=k1
Environment Variables
---------------------
spring.redis.host = localhost
spring.redis.port = 6379
server.port = 8081
Tech Stack
-----------
- Spring Boot 3.5
- Lettuce Redis Client
- JUnit 5, Mockito, MockMvc
- Maven
- JaCoCo
- Jackson JSON
Future Enhancements
-------------------
- Add Redis Cluster support
- Reactive Redis client
- Prometheus metrics
- Docker Compose integration
