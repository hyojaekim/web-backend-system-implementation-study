# 구성요소
- 브로커: 카프카
- 프로듀서: 브로커에게 데이터를 **기록한다.**
- 컨슈머: 브로커에게 데이터를 **읽는다.**
- 모든 것은 분산

# 데이터
- 데이터는 **토픽**에 저장
- 토픽은 **파티션**에 **분할(Partitions)**, **복제(Replicated)**되어 있다.
- 파티션 단위로 분산처리 된다.
- 파티션은 순차적이고, 불변적인 일련의 메시지이다. (어느 부분을 삭제하고 끼워넣을 수 없다. 즉, 커밋되면 변경될 수 없음)

# 컨슈머는 어디까지 메시지를 읽었는지 어떻게 알 수 있을까?
- **offset 포인터(메시지 아이디)**로 어디까지 읽었는지 기록한다.
- 컨슈머들은 **offset, partition, topic**으로 메시지를 추적한다.

# 컨슈머와 컨슈머 그룹
- 컨슈머 그룹 개념을 통해 **큐 모델과 발행-구독 모델 모두 지원**한다.
- 파티션은 **컨슈머 그룹당 오로지 하나의 컨슈머 접근만을 허용**하며, 해당 컨슈머를 **파티션 오너**라고 부른다.
- 파티션 내에 **메시지 순서에 대해 보장**하고, 토픽의 **다른 파티션의 순서는 보장하지 않는다.**

### 파티션은 하나의 컨슈머 밖에 접근하지 못하나?
- 아니다. 같은 그룹 내의 컨슈머들은 같이 접근하지 못하지만, 다른 그룹의 컨슈머는 동시에 접근 가능하다. (브로드 캐스트 가능)

### 파티션이 3개이고, 컨슈머 그룹 내의 컨슈머가 3개인데 만약 해당 그룹에 새로운 컨슈머가 들어온다면?
- 해당 컨슈머는 파티션을 읽지 못하고, 멍청하게(?) 가만히 있는다. 하나가 죽어야 읽을 수 있다.
- 컨슈머 그룹 전략을 잘 짜야한다.

# Replicas: 파티션의 백업
- 데이터 손실을 막기 위함.
- 복제는 절대로 읽지도 쓰지도 않는다.
- 데이터 손실 전, numReplicas - 1 만큼 죽는 브로커를 허용

# 렉(lag)
- 컨슈머 문제에 의해 발생
- 메시지 소비 속도가 너무 느리거나, 주키퍼 또는 카프카 연결이 끊어지는 등 이러한 이유로 인해 렉이 발생

# Kafka Cluster
- ex) logs 토픽 정보: partition 3, replication-factor 2
- kafka broker 1
  - **Partition 0 / Replica 1**
  - Partition 2 / Replica 1
- kafka broker 2
  - Partition 0 / Replica 2
  - **Partition 1 / Replica 2**
- kafka broker 3
  - Partition 1 / Replica 3
  - **Partition 2 / Replica 3**

# 명령어
- zookeeper 실행 `./bin/zookeeper.server.start.sh ./config/zookeeper.properties`
- kafka server 실행 `./bin/kafka-server-start.sh ./config/server.properties`
- topic 생성 `./bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic event.join`
- topic 목록 조회 `./bin/kafka-topics.sh --list --zookeeper localhost:2181
- 메시지 전송 및 읽기
  - 브로커 리스트 목록에 대해 메시지 전송 `./bin/kafka-console.producer.sh --broker-list localhost:9092 --topic event.join`
  - producer(메시지 전송) `./bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic test`
  - consumer(메시지 읽기) `./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test`
    - 이전 메시지까지 읽어오기 `./bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic test --from-beginning`
- [topic 삭제](https://hyojaedev.tistory.com/38)

# 고민
- 어떻게 파티셔닝을 할 것인가?
- 프로듀서, 컨슈머들을 어떻게 분산처리 할 것인가?
- 특별한 조건들을 두고 어떻게 하면 빠르게 하기 위해 토픽이랑 파티션을 둘 것인가?
- kafka broker가 죽으면 복제는 어떻게 할 것인가?
