
# Producer API
# Consumer API

+++
### Producer / Consumer API
* API stworzone dla języka Java
* Służy do wysyłania i odczytywania wiadomości z Kafki
* Łatwość integracji z naszymi systemami (prosty kod)
* Jest bazą dla wszystkich innych API
* Wiadomości wysyłane są jako "paczki" (latency versus throughput)
* Wiadomości to ciąg bajtów i metadane
* Implementuje Kafka protocol




+++
### Producer API
~~~java
Properties producerConfig = new Properties();
producerConfig.put(ProducerConfig.BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
producerConfig.put(ProducerConfig.CLIENT_ID_CONFIG, "");
producerConfig.put(ProducerConfig.KEY_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());
producerConfig.put(ProducerConfig.VALUE_SERIALIZER_CLASS_CONFIG, StringSerializer.class.getName());

Producer<String, String> producer = new KafkaProducer<>(producerConfig);

ProducerRecord<String, String> data = new ProducerRecord<>(TOPIC, MESSAGE_ID, "Message text...");
producer.send(data);

producer.flush();
producer.close();
~~~
@[1-5](Konfiguracja)
@[7](Kafka producent)
@[9](Rekord wiadomośći (klucz - wartość))
@[10](Wysłanie wiadomości (do bufora))
@[12-13](Wysłanie bufora, zamknięcie producenta)



+++
### Consumer API
~~~java
Properties consumerConfig = new Properties();
consumerConfig.put(ConsumerConfig.BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
consumerConfig.put(ConsumerConfig.GROUP_ID_CONFIG, "group-name");
consumerConfig.put(ConsumerConfig.VALUE_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getCanonicalName());
consumerConfig.put(ConsumerConfig.KEY_DESERIALIZER_CLASS_CONFIG, StringDeserializer.class.getCanonicalName());

KafkaConsumer<String, String> consumer = new KafkaConsumer<>(consumerConfig);
consumer.subscribe(Collections.singletonList(TOPIC));

ConsumerRecords<String, String> records = consumer.poll(TIMEOUT);

if (records.count() > 0) {
    LOGGER.info("Poll records: " + records.count());

    for (ConsumerRecord<String, String> record : records) {
        // Consume message
    }
}

consumer.commitAsync();
consumer.close();
~~~
@[1-5](Konfiguracja)
@[7](Kafka konsument)
@[8](Subskrybcja do kolejki)
@[10](Pobranie wiadomości z topicu)
@[12-18](Pobranie wiadomości z topicu)
@[20](Offsets commit)
@[21](Zamykamy odbiorcę)
