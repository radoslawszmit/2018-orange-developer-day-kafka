
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
producerConfig.put(BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
producerConfig.put(CLIENT_ID_CONFIG, "");
producerConfig.put(KEY_SERIALIZER_CLASS_CONFIG, 
    StringSerializer.class.getName());
producerConfig.put(VALUE_SERIALIZER_CLASS_CONFIG, 
    StringSerializer.class.getName());
producerConfig.put(ACKS_CONFIG, "all");
producerConfig.put(RETRIES_CONFIG, 1);

Producer<String, String> producer 
    = new KafkaProducer<>(producerConfig);

ProducerRecord<String, String> data 
    = new ProducerRecord<>(TOPIC, MESSAGE_ID, "Message...");
producer.send(data);

producer.flush();
producer.close();
~~~
@[1-9](Konfiguracja)
@[11-12](Kafka producent)
@[14-15](Rekord wiadomośći (klucz - wartość))
@[16](Wysłanie wiadomości (do bufora))
@[18-19](Wysłanie bufora, zamknięcie producenta)



+++
### Consumer API
~~~java
Properties consumerConfig = new Properties();
consumerConfig.put(BOOTSTRAP_SERVERS_CONFIG, KAFKA_SERVER);
consumerConfig.put(GROUP_ID_CONFIG, CONSUMER_GROUP);
consumerConfig.put(VALUE_DESERIALIZER_CLASS_CONFIG, 
    StringDeserializer.class.getName());
consumerConfig.put(KEY_DESERIALIZER_CLASS_CONFIG, 
    StringDeserializer.class.getName());
consumerConfig.put(AUTO_OFFSET_RESET_CONFIG, "earliest");
consumerConfig.put(ENABLE_AUTO_COMMIT_CONFIG, true);

KafkaConsumer<String, String> consumer 
    = new KafkaConsumer<>(consumerConfig);
consumer.subscribe(Collections.singletonList(TOPIC));

ConsumerRecords<String, String> records
    = consumer.poll(TIMEOUT);

if (records.count() > 0) {
    LOGGER.info("Poll records: " + records.count());

    for (ConsumerRecord<String, String> record : records) {
        // Consume message
    }
}

consumer.commitAsync();
consumer.close();
~~~
@[1-9](Konfiguracja)
@[11-12](Kafka konsument)
@[13](Subskrybcja do kolejki)
@[14-15](Pobranie wiadomości z topicu)
@[17-23](Obsługa wiadomości z topicu)
@[25](Offsets commit)
@[26](Zamykamy odbiorcę)
