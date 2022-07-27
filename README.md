# kafka-cluster-manager
Shell Scripts for managing Kafka clusters

---

### Kafka 2.13-3.1.0 기준 자주 사용하는 명령어

- 토픽 리스트
```shell script
bin/kafka-topics.sh --bootstrap-server kafka01:9092 --list
```


- 토픽 생성
```shell
bin/kafka-topics.sh --bootstrap-server kafka01:9092 --create --topic igkim-mm --partitions 3 --replication-factor 2
bin/kafka-topics.sh --bootstrap-server kafka01:9092 --create --topic igkim-mm-second --partitions 2 --replication-factor 2
```
       
    
- 토픽 삭제

    bin/kafka-topics.sh --bootstrap-server kafka01:9092 --delete --topic B.*

- 토픽 상세 정보

    bin/kafka-topics.sh --bootstrap-server kafka01:9092 --describe --topic igkim-mm

- 토픽 삭제 주기 변경

    bin/kafka-configs.sh --bootstrap-server kafka01:9092 --entity-type topics --entity-name igkim-mm --alter --add-config retention.ms=1000

    bin/kafka-configs.sh --bootstrap-server kafka01:9092 --entity-type topics --entity-name igkim-mm --alter --add-config retention.ms=36000000

    bin/kafka-configs.sh --bootstrap-server kafka01:9092 --entity-type topics --entity-name igkim-mm-second --alter --add-config retention.ms=1000

    bin/kafka-configs.sh --bootstrap-server kafka01:9092 --entity-type topics --entity-name igkim-mm-second --alter --add-config retention.ms=36000000

- 샘플 Producer 실행

    bin/kafka-producer-perf-test.sh --topic igkim-mm --num-records 3000 --throughput -1 --producer-props bootstrap.servers=kafka01:9092,kafka02:9092,kafka03:9092 \
 --print-metric --record-size 10485760 --producer.config config/producer.properties

    bin/kafka-producer-perf-test.sh --topic igkim-mm-second --num-records 1000 --throughput -1 --producer-props bootstrap.servers=kafka01:9092,kafka02:9092,kafka03:9092 \
 --print-metric --record-size 10485760 --producer.config config/producer.properties

    bin/kafka-producer-perf-test.sh --topic igkim --num-records 300 --throughput -1 \
 --print-metric --record-size 10485760 --producer.config config/producer.properties

- 샘플 Consumer 실행

    bin/kafka-console-consumer.sh --bootstrap-server kafka01:9092 --topic igkim --from-beginning

- MirrorMaker2 실행

    bin/connect-mirror-maker.sh config/igkim/s-to-t.prop
