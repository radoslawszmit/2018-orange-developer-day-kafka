
# Zasada działania


+++
### Kafka Logs
![](assets/img/kafka/how-it-works/log.png)
<br/><span class="footer">https://www.confluent.io/blog/okay-store-data-apache-kafka</span>



+++
### Kafka Logs
* Prosta abstrakcja składowania danych
* Logi to wiadomości klucz-wartość
* Sekwencja danych (zachowuje kolejność)
* Brak edycji (tylko append)
* Logi danych a nie aplikacji (!=log4j)



+++
### Producenci, konsumenci, topic
![](assets/img/kafka/how-it-works/kafka-architecture.png)
<br/><span class="footer">https://www.cloudera.com/documentation/kafka/1-2-x/topics/kafka.html</span>



+++
### Producenci i konsumenci - niezależny odczyt i zapis
![](assets/img/kafka/how-it-works/log_subscription.png)



+++
### Consumer offset
<!-- .slide: class="imagecentersize50" -->
![](assets/img/kafka/how-it-works/log_consumer.png)



+++
### Partycje - wydajność i rozproszenie
![](assets/img/kafka/how-it-works/partitioned_log.png)



+++
### Partycje - gdzie zapisać?
![](assets/img/kafka/how-it-works/log_anatomy.png)



+++
<!-- .slide: class="imagecentersize80" -->
### Partycje - replikacja
![](assets/img/kafka/how-it-works/replication.jpg)
<br/><span class="footer">https://www.confluent.io/blog/hands-free-kafka-replication-a-lesson-in-operational-simplicity/</span>


+++
### Partycje - replikacja
<!-- .slide: class="imagecentersize80" -->
![](assets/img/kafka/how-it-works/replication-lagging.jpg)
<br/><span class="footer">https://www.confluent.io/blog/hands-free-kafka-replication-a-lesson-in-operational-simplicity/</span>



+++
<!-- .slide: class="font90" -->
### Consumer offset
* Każdy offset to maksymalnie Long.MAX_VALUE (nie można zresetować)
* Offset jest oddzielny dla każdej partycji
* Zakładając sto wiadomości na sekundę (na partycję) limit spotkamy za 3 miliardy lat
* Nasza planeta będzie nadawała się do życia prawdopodobnie tylko przez miliard lat
* Zakładając milion wiadomości na sekundę (na partycję) limit spotkamy za 300 tysięcy lat


+++
<!-- .slide: class="font90" -->
### Topiki
* Nie ma teoretycznego limitu liczby topików
* Ze względów wydajnościowych nie zaleca się przekraczanie 4000 partycji na brokera i 200 000 partycji w klastrze
* Wiadomości trzymane są domyślnie 168 godzin (7 dni)
* Można także ograniczyć maksymalną wielkość logu (domyślnie brak limitu)
<br/><span class="footer">https://www.confluent.io/blog/apache-kafka-supports-200k-partitions-per-cluster</span>


+++
<!-- .slide: class="font90" -->
### Wiadomości
* Kafka potrafi przetwarzać duże zbiory danych (sumarycznie)
* Jednak pracuje najlepiej z małymi wiadomościami (domyślnie 1MB limit)
* Jeśli chcemy obsługiwać wiadomości z dużymi załącznikami to najlepiej podzielić je na mniejsze fragmenty lub użyć zewnętrznego dodatkowego narzędzia do ich składowania


+++
### Wiadomości
* Każda wiadomość to klucz, wartość i metadane
* Kafkę nie interesuje format danych (używamy dowolnej serializacji)
* Warto korzystać z formatów typu Avro (schemat)
* Możliwość kompresji wiadomości



+++
### Grupy konsumentów
![](assets/img/kafka/how-it-works/consumer-group.png)



+++
### Grupy konsumentów
![](assets/img/kafka/how-it-works/consumer-groups.png)



+++
### Kompaktowanie logów
![](assets/img/kafka/how-it-works/log_compaction_0.png)

