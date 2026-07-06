# 22. Przedstaw podstawowe architektury współczesnych komputerów.

## Architektura Von Neumanna

Architektura Von Neumanna jest bazą dla większości współczesnych komputerów.
Opiera się ona na trzech kluczowych koncepcjach:
* Dane i instrukcje są przechowywane w pojedynczej pamięci do odczytu i zapisu
* Zawartość tej pamięci jest adresowalna według lokalizacji, bez względu na
rodzaj zawartych tam danych
* Wykonanie następuje w sposób sekwencyjny od jednej instrukcji do nastepnej

## Architektura harvardzka
Została opracowana w latach 40. XX wieku przez Howarda Aikena, który wraz z
grupą badawczą na uniwersytecie Harvarda stworzył komputer Harvard Mark I.
Później została ona wykorzystana chociażby w komputerze IBM czy UNIVAC I.
Obecnie stosowana jest w systemach wbudowanych, mikrokontrolerach i procesorach
sygnałowych. Opiera się ona na założeniu, że dane i instrukcje są przechowywane
w osobnych pamięciach, z osobnymi kanałami komunikacji pomiędzy nimi (oddzielne
szyny adresowe i danych dla każdej z pamięci, co pozwala na równoczesny odczyt
instrukcji i danych).

## Zmodyfikowana architektura harvardzka (hybrydowa architektura Von Neumanna/Harvarda)
Jest to połączenie elementów architektury Von Neumanna oraz architektury
harvardzkiej. Architekturę harvardzką można zmodyfikować na kilka sposobów:

### Oddzielne pamięci cache
Instrukcje oraz dane są przechowywane w tej samej pamięci (architektura Von
Neumanna), ale pamięć jest podzielona na rejon instrukcji oraz danych, które
mają swoje dedykowane pamięci cache (architektura Harvardzka).

### Pamięć instrukcji jako dane
Instrukcje oraz dane są przechowywane w tej samej pamięci (architektura Von
Neumanna), ale pamięć ta jest inaczej adresowana dla instrukcji oraz danych
(architektura Harvardzka)

### Pamięć danych jako instrukcje
Instrukcje oraz dane są przechowywane w tej samej pamięci (architektura Von
Neumanna), a dowolny rejon danych może zostać przeczytany, zinterpretowany i
wykonany jako instrukcje procesora.