# 10. Wskaźniki - definicja, operacje, zjawiska zwisających odwołań i śmieci (wyciekającej pamięci)

## Definicja 

W językach programowania pozwalających na bezpośredni dostęp do pamięci pamięć
jest reprezentowana jako jednowymiarowa tablica bajtów. Wskaźnik jest indeksem
do tej tablicy [Wikipedia].

Wskaźnik przechowuje wartość całkowitą oznaczającą adres pamięci pod którym
zapisane są jakieś dane. Wskaźnik może wskazywać na dane umieszczone zarówno na 
stosie jak i na stercie. Może on również wskazywać na region pamięci mapowany na
urządzenia I/O (to akurat w sterownikach itd). 

```
{ // C
    int x;                                  // zmienna na stosie
    int* px = &x;                           // wskaźnik na zmienną na stosie
    int* py = (int*)malloc(sizeof(int));    // wskaźnik na zmienną na stercie
}
```

## Operacje

```
{ // C
    int* px = (int*)malloc(sizeof(int) * 10); // 10-cio elementowa tablica intów na stercie

    // dereferencja
    int y = *px; // zerowy element
    y = px[0];   // zerowy element
    y = 0[px];   // tak też się da - zerowy element

    // arytmetyka
    for (int i = 0; i < 10; ++i) { y = px[i]; } // iteracja po tablicy

    for (int i = 0; i < 10; ++i) { y = *(px + i); } /**
                                                     * To samo co w pierwszej
                                                     * pętli, wartość wskaźnika
                                                     * się nie zmienia.
                                                     */

    int* pxref = px;
    for (int i = 0; i < 10; ++i) { y = pxref++; }   /**
                                                     * To samo co w pierwszej
                                                     * pętli, wartość kopii
                                                     * wskaźnika się zmienia.
                                                     */
    
    /**
     * Podczas dodawania, odejmowania, mnożenia oraz dzielenia wskaźników,
     * ich wartości adresów skalują się według typu danej jaką przechowują.
     * Gwarantuje to, że jeśli do adresu wskaźnika na inta dodamy 1, to jego
     * wartość przeskaluje się o rozmiar jednego inta (typowo 4 bajty, ale
     * standard tego nie definiuje). Pozwala to uniknąć sytuacji, gdzie zaczniemy
     * czytać niezalignowane dane, co prowadziłoby do źle interpretowanych wartości
     * lub w niektórych przypadkach segfaultów.
     */

    // zwalnianie pamięci
    free(px); // nie wołamy free na pxref, ponieważ to była kopia tego wskaźnika
}
```

## Zwisające odwołanie

```
{ // C
    int* px = (int*)malloc(sizeof(int));
    int* pxref = px;
    free(px);
    /**
     * Tutaj pxref jest zwisającym odwołaniem, ponieważ wskazuje na zwolnioną
     * pamięć i może doprowadzić do use after free. Tak naprawdę w C px też jest
     * zwisającym odwołaniem, ponieważ standard nie wymaga zmiany wartości px na 
     * NULL po wywołaniu na niej free(); W C++ delete gwarantuje zmianę wartości
     * wskaźnika na nullptr.
     */
}
```

## Śmieci

```
{ // C
    int* px = (int*)malloc(sizeof(int));
    *px = 10;
    px = (int*)malloc(sizeof(int)); /**
                                     * W tym momencie tworzymy śmieć w postaci
                                     * zmiennej na stercie do której przypisaliśmy
                                     * wartość 10 po czym nadpisaliśmy wartość
                                     * wskaźnika, który na nią wskazywał bez
                                     * zwalniania tej pamięci. Teraz w pamięci
                                     * programu żyje sobie incik do którego nie
                                     * możemy się dostać ani w celach modyfikacji
                                     * ani jego zwolnienia.
                                     */
}
```