# 19. Definicja grafu oraz metody jego reprezentacji (macierz asocjacji, tablica list krawędzi). Metody przeglądania grafu: w głąb (DFS) i wszerz (BFS).

## Definicja

Graf to podstawowy obiekt rozważań teorii grafów, struktura matematyczna służąca
do przedstawiania i badania relacji między obiektami. W uproszczeniu graf to
zbiór wierzchołków, które mogą być połączone krawędziami w taki sposób, że każda
krawędź kończy się i zaczyna w którymś z wierzchołków. [Wikipedia]

Grafy mogą być skierowane lub nieskierowane. Mówi o tym wzajemność połączeń -
jeśli każde połączenie jest obustronne, tzn dla każdego wierzchołka A oraz
każdego jego sąsiada B istnieje połączenie z A do B oraz z B do A, to mówimy, że
mamy do czynienia z grafem nieskierowanym. Możemy o tym myśleć jak o drodze jedno
lub dwukierunkowej. W grafie nieskierowanym każde połączenie jest drogą
dwukierunkową. Wystarczy jednak jedna droga jednokierunkowa, aby graf był grafem
skierowanym.

Dodatkowo możemy mówić o grafach ważonych. Ważenie grafu wynika z "kosztu"
przejścia którąś z krawędzi. Oczywiście nie zawsze musi to oznaczać koszt,
jednakże grafy ważone najczęściej występują w sytuacjach, gdzie graf reprezentuje
mapę, a krawędzie przedstawiają drogi pomiędzy kluczowymi punktami tej mapy. 

## Macierz asocjacji

Macierz asocjacji to kwadratowa macierz N x N, gdzie N to jest liczba
wierzchołków w grafie. Za pomocą 0 i 1 przedstawia ona połączenia pomiędzy
wszystkimi wierzchołkami grafu, gdzie 1 oznacza istniejące połączenie pomiędzy
wierzchołkami, natomiast 0 sygnalizuje jego brak.
```
| -------------------|
| \ | A | B | C | D  |
| -------------------|
| A | x   1   0   1  |
| ---                |
| B | 1   x   1   1  |
| ---                |
| C | 0   1   x   0  |
| ---                |
| D | 1   1   0   x  |
| -------------------|
```

## Tablica list krawędzi

Tablica list krawędzi jest bardziej intuicyjną reprezentacją grafu. Krótko mówiąc
jest to zbiór wszystkich krawędzi przedstawionych za pomocą węzła startowego oraz
węzła końcowego, np. (A, B). Możemy o tej reprezentacji myśleć, jak o zestawie
danych w formie klucz-wartość, gdzie kluczem jest węzeł startowy, a wartością
węzeł końcowy.

Alternatywną wersją tej reprezentacji, jest reprezentacja z wartością jako listą
węzłów docelowych, co często ma miejsce w implementacjach programów:

```
// C
typedef struct GraphNode {
    void* p_data;
    struct GraphNode* p_neighbours; // array of as many neighbours as you want
} GraphNode;
```

## DFS

Przeszukiwanie w głąb charakteryzuje się priorytetyzacją przechodzenia grafu w
głąb. Oznacza to, że wchodząc do wierzchołka grafu, od razu idziemy do jego
pierwszego dziecka, aż do momentu kiedy nie natrafimy na wierzchołek bez dzieci.
Wtedy po jego przeszukaniu wychodzimy poziom wyżej i przeszukujemy kolejne dzieci
jego rodzica itd. Wszystkie odwiedzone wierzchołki należy oznaczać jako odwiedzone, 
aby zapobiec niechcianym cyklom (nieskończonym pętlom).
```
1 - 2 - 3
|       |
4 - 5 - 6
|        
7 - 8 - 9
```
Powyższy graf zostanie przeszukany w kolejności 9-8-7-2-3-6-5-4-1.

## BFS

Przeszukiwanie wszerz charakteryzuje się priorytetyzacją pola przeszukanej
powierzchni wokół wierzchołka startowego. Najpierw dodajemy do kolejki wszystkie
dzieci startowego wierzchołka, następnie odwiedzamy jego pierwsze dziecko i
dołączamy na koniec kolejki wszystkie jego dzieci. Kolejkę przechodzimy zgodnie
z kolejnością kolejkowania wierzchołków. Podobnie jak w DFS, wszystkie odwiedzone
wierzchołki należy oznaczać jako odwiedzone aby nie doprowadzić do powstania
nieskończonej pętli.
```
1 - 2 - 3
|       |
4 - 5 - 6
|        
7 - 8 - 9
```
Powyższy graf zostanie przeszukany w kolejności 1-4-2-7-5-3-8-6-9.