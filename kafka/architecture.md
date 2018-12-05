
# Architektura


+++
### Architektura
![](assets/img/architecture/Kafka-Broker-Diagram.png)



+++
### Brokerzy
![](assets/img/architecture/broker-on-disk.png)



+++
### Wiadomości
![](assets/img/architecture/messages.jpg)



+++
### Segmenty
![](assets/img/architecture/segments.png)


+++
### Zero-copy
"Zero-copy" describes computer operations in which the CPU does not perform the task of copying data from one memory area to another. This is frequently used to save CPU cycles and memory bandwidth when transmitting a file over a network. Wikipedia



+++
### Data copying

@div[left-50 fragment]
![](assets/img/kafka/architecture/traditional-data-copying.gif)
@divend

@div[right-50 fragment]
![](assets/img/kafka/architecture/zero-copy-data-copying.gif)
@divend



+++
### Context switching

@div[left-50 fragment]
![](assets/img/kafka/architecture/traditional-context-switching.gif)
@divend

@div[right-50 fragment]
![](assets/img/kafka/architecture/zero-copy-context-switching.gif)
@divend