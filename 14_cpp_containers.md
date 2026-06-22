# 14. Omów własności kontenerów asocjacyjnych i adapterów kontenerów z biblioteki STL w C++. Pokaż różnice funkcjonalności.

## Definicja

Kontenery asocjacyjne to kontenery w których wartości są ze sobą w jakiś sposób
powiązane w celu określenia ich unikalności lub mapowania:
* set - kontener zawierający tylko unikalne elementy
* multiset - kontener pozwalający na powtórzenia elementów, który jednocześnie
zlicza ilość powtórzeń dla każdego z elementów
* map - kontener wiążący przechowywane wartości z jakimś kluczem (key-value),
gdzie klucze nie mogą się powtarzać, a do jednego klucza jest przypisana jedna
wartość
* multimap - kontener wiążący przechowywane wartości z jakimś kluczem (key-value),
gdzie klucze nie mogą się powtarzać, a do jednego klucza może być przypisanych
więcej niż jedna wartość

Adaptery kontenerów oznaczają jakieś rozwinięcie bazowego kontenera i
udostępnienie jego funkcjonalności w określony sposób. Przykładami są:
* stack - stos oparty o std::list, std::vector lub std::deque
* queue - kolejka oparta o std::list lub std::deque
* priority_queue - kolejka priorytetowa również oparta o std::vector lub std::deque
Adaptery domyślnie tworzone są na bazie predefiniowanych kontenerów opisanych
w standardzie języka, jednak użytkownik może zmienić typ kontenera bazowego
adaptera na jeden ze wspieranych typów podczas tworzenia adaptera.

Różnice wynikają z definicji.