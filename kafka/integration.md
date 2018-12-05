
# Integracja



+++
### Kafka API

@div[left-50]
![](assets/img/integration/kafka-apis.png)
@divend

@div[right-50]
@ul[white]
- Producer API
- Consumer API
- Streams API
- Connect API
- AdminClient API
- Legacy API (old)
@ulend
@divend



+++
### Które API wybrać?
Wymaganie | Rozwiązanie
------------    | -------------
App -> Kafka    | Producer API
Kafka -> App    | Consumer API
Source -> Kafka | Connect API (lub Producer API)
Kafka -> Sink   | Connect API (lub Consumer API)
Kafka -> Kafka  | Streams API (lub Prod/Con API)



+++
### Klienci Kafka
* Stworzona w oparciu o język **Scala**
* Zespół Apache Kafka utrzymuje i rozwija bibliotekę kliencką dla języka **Java**
* Dostępne są klienci "community" dla innych języków programowania (niekiedy kilka możliwości)



