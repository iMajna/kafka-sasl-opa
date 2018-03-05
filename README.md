SSL/SASL Kafka in Docker with OPA authorization
===

Create certificates for SSL/SASL/Kerberos

    cd secrets
    ./create-certs.sh

Start OPA, Kerberos, Zookeeper, Kafka broker, a producer and a consumer.

    cd ..
    docker-compose up -d
    docker logs producer
    docker logs consumer

OPA policy stops producer and consumer from creating the topic "X" so they keep failing.

Create the topic from the broker box (as user kafka).

    docker exec -it broker bash -c "kafka-topics --zookeeper zookeeper --create --topic X --partitions 1 --replication-factor 1"

Soon after the topic is created the producer and the consumer can access it.

    docker logs producer
    docker logs consumer

    docker-compose down
