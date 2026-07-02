# 21. Omów strategię przeszukiwania lokalnego. Podaj przykłady algorytmów używających tej strategii.

## Definicja 

Przeszukiwanie lokalne polega na ewaluacji sąsiedztwa rozwiązań w celu
znalezienia najbardziej optymalnego rozwiązania problemu w oparciu o jakieś
kryteria oceny. Strategia ta porusza się po przestrzeni rozwiązań, kolejno je
ewaluując, często wybierając następne rozwiązania do ewaluacji na podstawie tego
czy obrana droga po sąsiedztwie rozwiązań zbliża nas do optymalnego rozwiązania.

W skrócie:
1. Rozwiązanie jest ewaluowane - spełnia kryteria? super, jak nie to idziemy do pkt 2
2. W algorytmie wprowadzane są drobne zmiany parametrów wejściowych, wróć do pkt 1

## Zastosowania

Głównie uczenie maszynowe oraz SAT solvery i pokrewne.

## Przykłady algorytmów

Hill climb, symulowane wyżarzanie, Gradient descent