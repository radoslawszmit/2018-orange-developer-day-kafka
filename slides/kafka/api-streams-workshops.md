
# Streams API
# Warsztat



+++
### Streams API
~~~java
Properties config = new Properties();
config.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
config.put(StreamsConfig.APPLICATION_ID_CONFIG, "wordcount");
config.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());
config.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass().getName());

StreamsBuilder builder = new StreamsBuilder();
KStream<String, String> textLines = builder.stream(TOPIC);
KTable<String, Long> wordCounts = textLines
    .flatMapValues(textLine -> Arrays.asList(textLine.toLowerCase().split("\\W+")))
    .groupBy((key, word) -> word)
    .count(Materialized.as("counts-store"));

wordCounts.toStream().to(TOPIC_OUT, Produced.with(Serdes.String(), Serdes.Long()));

KafkaStreams streams = new KafkaStreams(builder.build(), config);
streams.start();
~~~
@[1-5](Konfiguracja)
@[6-12](Kafka Streams)
@[14](Zapis wyniku do Kafki)
@[16-17](Wysłanie wiadomości (do bufora))



+++
### Wynik z Kafka Streams
~~~bash
bin/kafka-console-consumer.sh --bootstrap-server $KAFKA_BROKER --topic $TOPIC --from-beginning

bin/kafka-console-consumer.sh --bootstrap-server $KAFKA_BROKER --topic $TOPIC_OUT --from-beginning

bin/kafka-console-consumer.sh --bootstrap-server $KAFKA_BROKER \
    --topic $TOPIC_OUT \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
~~~