# 20. Omów algorytmy minimax i alfa-beta.

## Minimax

Minimax jest algorytmem minimalizowania maksymalnych strat/maksymalizowania
minimalnych zysków. Polega na zbudowaniu drzewa decyzyjnego, w którym każdy z
węzłów reprezentuje decyzję danego gracza. Zadaniem pierwszego gracza jest
wybieranie najwyżej (tzn korzystnie dla niego) punktowanych decyzji, natomiast
zadaniem drugiego jest wybieranie najniżej (tzn niekorzystnie dla pierwszego)
punktowanych decyzji. Algorytm jest wykonywany rekurencyjnie - wywoływany jest
na korzeniu drzewa, który wywołuje go na swoich dzieciach, które wywołują go
na swoich dzieciach itd, aż do momentu dotarcia do liści drzewa. Wtedy algorytm
ewaluuje wartości liści i zaczyna cofać się w górę drzewa, przypisując rodzicom
na zmianę najwyższą, a później najniższą wartość spośród pary dzieci. Ostateczna
droga znana jest po całkowitym wyjściu ze stosu wywołań.

## Alfa-beta

Alfa-beta jest wzbogaceniem algorytmu minimax pozwalającym na określenie czy
dalsze ewaluacje drzewa są konieczne, a tym samym zaoszczędzenie czasu, który
inaczej zostałby zmarnowany na wykonywanie obliczeń, które i tak by nic nie
wniosły. Do rekurencyjnych wywołań dodawane są wartości alfa oraz beta, które
inicjalizowane są kolejno na -inf oraz inf przy pierwszym wywołaniu algorytmu na
korzeniu drzewa. Przekazywane są one w dół drzewa, aż do momentu dojścia do
pierwszego liścia. Następnie wartość alfa rodzica tego liścia jest ustawiana na
największą wartość spośród wartości przechowywanych przez jego dzieci. Algorytm
wychodzi poziom wyżej i zamienia wartości alfa oraz beta, przekazując je do
drugiego dziecka. W przypadku kiedy wartość beta jest mniejsza od wartości alfa,
oznacza to, że możemy nie ewaluować drugiego dziecka i wyjść z rekurencyjnego
wywołania o jeden poziom wyżej ("uciąć" nieznaczącą gałąź).