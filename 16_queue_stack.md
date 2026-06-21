# 16. Omów struktury kolejki oraz stosu, ich zastosowania oraz implementację opartą o listę.

## Definicja

Kolejka jest strukturą do której dane są dołączane oraz z której są czyta w
określony sposób (FIFO/FILO). Tradycyjną kolejką jest kolejka FIFO, natomiast
stos jest szczególnym przypadkiem kolejki - kolejką FILO.

FIFO jest skrótem od angielskiej nazwy First In, First Out. Oznacza to, że
elementy znajdujące się w kolejce są czytane w kolejności w jakiej zostały do
niej dodane.

FILO jest skrótem od angielskiej nazwy First In, Last Out. Oznacza to, że
elementy znajdujące się w kolejce są czytane w kolejności odwrotnej niż ta, w
której je dodano do kolejki.

## Zastosowania

Zastosowania kolejki FIFO obejmują wszystkie sytuacje, gdzie potrzebne jest
sekwencyjne przetworzenie jakichś danych, a zwłaszcza kiedy kolejka tych danych
może zwiększać swoją długość (tak naprawdę o tablicy jednowymiarowej można myśleć
jak o kolejce, o tablicy dwuwymiarowej jak o kolejce kolejek itd). Konkretne
przykłady to przeszukiwanie grafów czy kolejkowanie wydarzeń do obsłużenia w
systemie wydarzeń aplikacji.

Zastosowania stosu są równie rozległe, jednakże tutaj problem zazwyczaj wymaga
utworzenia lokalnego kontekstu działania. Dobrym zastosowaniem stosu jest stos
wywołań lub rozwijanie rekurencyjnych algorytmów do nierekurencyjnych
implementacji z wykorzystaniem statycznego stosu (algorytmy przeszukiwań). Z
rozwiązań obecnych w architekturze aplikacji może to również być stos warstw
aplikacji lub elementów graficznych w hierarchii GUI.

## Implementacja

Kolejkę FIFO można zaimplementować za pomocą listy jednokierunkowej:
```
// C
typedef struct QueueElement {
    void* p_data;
    struct QueueElement* p_next;
} QueueElement;

void enqueue(QueueElement** pp_head, void* p_data) {
    if (!*pp_head) {
        *pp_head = (QueueElement*)malloc(sizeof(QueueElement));
        (*pp_head)->p_data = p_data;
        (*pp_head)->p_next = (void*)0;
        return;
    }
    QueueElement* p_tmp = pp_head;
    while(p_tmp->p_next) { p_tmp = p_tmp->p_next; }
    p_tmp->p_next = (QueueElement*)malloc(sizeof(QueueElement));
    p_tmp->p_next->p_data = p_data;
    p_tmp->p_next->p_next = (void*)0;
}

void* dequeue(QueueElement** pp_head) {
    if (!*pp_head) { return (void*)0; }
    QueueElement* p_tmp = *pp_head;
    *pp_head = p_tmp->p_next;
    void* p_data = p_tmp->p_data;
    free(p_tmp);
    return p_data;
}
```

Implementacja stosu wygląda bardzo podobnie:
```
// C
typedef struct StackElement {
    void* p_data;
    struct StackElement* p_prev;
} StackElement;

void push(StackElement** pp_top, void* p_data) {
    StackElement p_tmp = *pp_top; // assuming the *pp_top is valid or NULL
    *pp_top = (StackElement*)malloc(sizeof(StackElement));
    (*pp_top)->p_data = p_data;
    (*pp_top)->p_prev = p_tmp;
}

void* pop(StackElement** pp_top) {
    if (!*pp_top) { return (void*)0; }
    StackElement* p_tmp = *pp_top;
    void* p_data = p_tmp->p_data;
    *pp_top = p_tmp->p_prev;
    free(p_tmp);
    return p_data;
}
```