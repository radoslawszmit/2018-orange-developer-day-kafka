
# Connect API

+++
### Co to takiego?
* Narzędzie do integracji z popularnymi źródłami danych
* Wykorzystywane jako wejście lub wyjście z topicu
* Używanie tego samego kodu (zwykle czyjegoś)
* Dostępnych wiele konektorów
* Bazuje na frameworku
* Odporność na awarie
* Wprowadzono w Kafka 0.9.x (Listopad 2015 r.)



+++
![](assets/img/kafka/connect/kafka-connect.png)



+++
### Architektura
* Wymagana instalacja komponentów (workers)
* Obsługa trybu Standalone (dev) i Distributed Mode (prod)
* Source i Sink Connectors
* Connector to Java jar
* Connector + Configuration = Task
* "Taski" uruchamiane są na "workerach"


+++
![](assets/img/kafka/connect/kafka-connect-sources-and-sinks.png)