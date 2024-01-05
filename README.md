→ open up Docker Desktop
→ run CheckoutApplication

IntelliJ → kafka → Open in: Terminal → docker compose up
http://localhost:9000/

IntelliJ → Terminal → docker ps -a → copy kafka container ID

→ get a Bash shell prompt inside the specified Docker container:
cmd Terminal → docker exec -it 5432bdf8309c /bin/bash

cd /opt/kafka_2.13-2.8.1

→ create a topic:
/opt/kafka_2.13-2.8.1# bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic order --partitions 1 --replication-factor 1

→ produce a message as a producer:
bin/kafka-console-producer.sh --broker-list localhost:9092 --topic order

→ open up a new Terminal
→ create a consumer of these messages:
/opt/kafka_2.13-2.8.1# bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic order

→ create a new consumer, with --from-beginning
/opt/kafka_2.13-2.8.1# bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic order --from-beginning

→ Postman → POST localhost://8080/checkout
(8080 because in application.yml service:port:8080)
{
"cardNumber":"1234123412341234",
"amount":234,
"item":"Xbox"
}

→ run OrderApplication
→ when you publish a message (Postman), you can also see in IntelliJ
