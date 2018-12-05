
# Gwarancje dostarczenia


+++
There are only two hard things in Computer Science: 
* cache invalidation and
* naming things.
<br/>
<br/>
-- Phil Karlton


+++
There are 2 hard problems in computer science:
* cache invalidation, 
* naming things, 
* and off-by-1 errors.
<br/>
<br/>
-- Leon Bambrick @secretGeek
Jan 1, 2010



+++
There are only two hard problems in distributed systems: 
* 2 Exactly-once delivery 
* 1 Guaranteed order of messages 
* 2 Exactly-once delivery
<br/>
<br/>
-- Mathias Verraes @mathiasverraes
Aug 14, 2015



+++
### Gwarancja dostarczenia
* At most once — Co najwyżej raz
* At least once — Przynajmniej raz
* Exactly once — Dokładnie raz



+++
### Gwarancja dostarczenia
* Kafka Streams API wspiera **exactly-once delivery** 
* Pozostałe API domyślnie wspierają **at-least-once delivery**
* Exactly-once delivery wymaga współpracy z systemem docelowym, dodatkowa implementacja