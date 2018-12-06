
# Streams API

+++
### Co to takiego?
* Narzędzie do przetwarzania strumieniowego
* Wejściem i wyjściem jest topic
* Integralna część Apache Kafka
* Jest to zwykła aplikacja (Java) bez potrzeby dodatkowej instalacji "workerów"
* Skalowalność, elastyczność, odporność na awarie
* Exactly Once Delivery (pod pewnymi warunkami)
* Wprowadzono w Kafka 0.10.x (Maj 2016 r.)



+++
### Konkurencja do:
* Spark Streaming
* Akka Streams
* Samza
* Flink
* Custom Code



+++
### Flow Managment & ETL
* NiFi
* Flume
* Logstash
* Fluent
* Pentaho Data Integration (Kettle)



+++
### Streams API
~~~java
Properties config = new Properties();
config.put(BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
config.put(APPLICATION_ID_CONFIG, "wordcount");
config.put(DEFAULT_KEY_SERDE_CLASS_CONFIG, 
    Serdes.String().getClass().getName());
config.put(DEFAULT_VALUE_SERDE_CLASS_CONFIG, 
    Serdes.String().getClass().getName());

StreamsBuilder builder = new StreamsBuilder();

KStream<String, String> textLines = builder.stream(TOPIC);

KTable<String, Long> wordCounts = textLines
    .flatMapValues(textLine -> 
        Arrays.asList(textLine.toLowerCase().split("\\W+")))
    .groupBy((key, word) -> word)
    .count(Materialized.as("counts-store"));

wordCounts.toStream().to(TOPIC_OUT, 
    Produced.with(Serdes.String(), Serdes.Long()));

KafkaStreams streams = new KafkaStreams(builder.build(), config);
streams.start();

Runtime.getRuntime().addShutdownHook(new Thread(streams::close));
~~~
@[1-7](Konfiguracja)
@[9](Kafka Stream Builder)
@[11](Strumień)
@[13-17](Kafka Streams)
@[19-20](Zapis wyniku do topicu Kafki)
@[22-23](Uruchomienie)
@[25](Eleganckie wyjście)




+++
### Który wybrać?
* Micro batch lub single data streaming
* Praca w klastrze lub zwykła aplikacja
* Skalowalność (rozbudowa czy włączenie nowego procesu/aplikacji)
* Wsparcie dla "Exactly Once Delivery"
* Biblioteka, platforma czy narzędzie drag & drop