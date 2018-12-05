
# Zasada działania


+++
### Kafka Logs
![](assets/img/how-it-works/log.png)



+++
### Kafka Logs
* Prosta abstrakcja składowania danych
* Logi to wiadomości klucz-wartość
* Sekwencja danych (zachowuje kolejność)
* Brak edycji (tylko append)
* Logi danych a nie aplikacji (!=log4j)



+++
### Producenci, konsumenci, topic
![](assets/img/how-it-works/kafka-architecture.png)



+++
### Producenci i konsumenci - niezależny odczyt i zapis
![](assets/img/how-it-works/log_subscription.png)



+++
### Consumer offset
<!-- .slide: class="imagecentersize50" -->
![](assets/img/how-it-works/log_consumer.png)



+++
### Partycje - wydajność i rozproszenie
![](assets/img/how-it-works/partitioned_log.png)



+++
### Partycje - gdzie zapisać?
![](assets/img/how-it-works/log_anatomy.png)



+++
### Partycje - replikacja
![](assets/img/how-it-works/replication.jpg)



+++
### Grupy konsumentów
![](assets/img/how-it-works/consumer-group.png)



+++
### Grupy konsumentów
![](assets/img/how-it-works/consumer-groups.png)



+++
### Kompaktowanie logów
![](assets/img/how-it-works/log_compaction_0.png)



+++
### Kompresja
* Możliwość kompresji wiadomości
* Przydatne przy dużych paczkach (batch) wiadomości
* Aktywacja za pomocą *compression.type*
* Możliwe opcje: gzip, snappy, lz4, uncompressed, **producer**
* Gdy kompresuje producent (zalecane)
    * brokerzy oszczędzają zasoby
    * mniej danych kopiowanych jest po sieci
* Zalecane dla danych które nie są binarne (xml, json, tekst)
