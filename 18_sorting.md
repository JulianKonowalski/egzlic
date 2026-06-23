# 18. Dolne ograniczenie na szybkość sortowania przy pomocy porównań i przestawiń. Sortowanie szybkie (quick sort) i przez scalanie (merge sort) oraz ich złożoności czasowe i pamięciowe.

## Dolne ograniczenie

N(logn)

## Quick sort

Algorytm polega na wybraniu "pivotu", czyli wartości relatywnie do której
będziemy sortować. Zazwyczaj jest to pierszy, środkowy lub ostatni element
sortowanego fragmentu tablicy. Może to także być mediana lub cokolwiek innego.
Następnie elementy mniejsze od wybranej wartości są umieszczane po lewej stronie
tej wartości, a wartości większe po prawej stronie (lub na odwrót, zależy jak
sortujemy). Wartości nie muszą być umieszczone w żadnej konkretnej kolejności,
ważne jest tylko zachowanie zależności: po jednej stronie pivotu są wartości
mniejsze, a po drugiej większe. Ostatnim krokiem jest rekurencyjne wywołanie 
quick sortu dla lewej i prawej strony tablicy do momentu aż algortym podzieli
całą tablicę na jednoelementowe fragmenty. Jako, że jednoelementowa tablica nie
wymaga sortowania, to jest to wartunkiem przerwania algorytmu.

Złożoność czasowa algorytmu to N(logn), natomiast pamięciowa to N(n), ponieważ
jest to algorytm wykonywany in-place.

```
[4, 2, 3, 1]    // 3 will be the pivot, just because I say so
[2, 1, 3, 4]    // smaller elements go to the left, larger to the right
[2, 1] [3] [4]  // split, on the left 1 will be the pivot, the rest doesn't need sorting
[1, 2] [3] [4]  /**
                 * sorted, because the algorithm works in-place, it's still a
                 * contiguous block of memory
                 */
```

## Merge sort

Merge sort polega na dzieleniu tablicy na coraz mniejsze podtablice, do momentu
dojścia do tablic jednoelementowych. Następnie algorytm wychodzi z wywołań
rekurencyjnych scalając powstałe tablice w coraz większe, posortowane kawałki.

Złożoność czasowa algorytmu to N(logn), natomiast pamięciowa to N(n) przy
założeniu, że algorytm jest wykonywany in-place lub przy użyciu dodatkowej
tablicy, bez żadnych dynamicznych alokacji pamięci podczas samego sortowania.

```
       [4, 2, 3, 1]         // first split the array into subarrays
      /            \
   [4, 2]         [3, 1]
  /      \       /      \
[4]      [2]   [3]      [1] // begin merging
  \      /       \      /
   [2, 4]         [1, 3]    // values are being sorted while merging
      \            /
       [1, 2, 3, 4]         // sorted array
```