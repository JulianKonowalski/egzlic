# 17. Definicja binarnego drzewa poszukiwań (BST) i podstawowe operacje: wstawianie, wyszukiwanie, usuwanie.

## Definicja

Binarne drzewo poszukiwań to dynamiczna struktura danych będąca drzewem binarnym,
w którym lewe poddrzewo każdego węzła zawiera wyłącznie elementy o kluczach
mniejszych niż klucz węzła. Węzły, oprócz klucza, przechowują wskaźniki na
swojego lewego i prawego syna oraz na swojego ojca [Wikipedia].

Tak naprawdę to węzły nie muszą i często nie przechowują wskaźników na rodziców,
ale kim jestem by kłócić się z wikipedią.

## Operacje

Wstawianie, wyszukiwanie oraz usuwanie opierają się o przechodzenie drzewa według
pewnej zasady - Jeśli wartość szukana jest mniejsza od przechowywanej w obecnie
odwiedzanym węźle, to idziemy do jego lewego dziecka. W przeciwnym wypadku idziemy
do jego prawego dziecka.

W przypadku wstawiania, gdy dojdziemy do pierwszego pustego miejsca to wstawiamy
tam nową wartość (przy założeniu, że wartości w drzewie się nie powtarzają).

Kiedy szukamy to przechodzimy przez drzewo do momentu natknięcia się na węzeł z
szukanym kluczem. Wtedy, w zależności od konwencji, zwracamy węzeł lub jakieś dane,
które przechowuje.

Gdy usuwamy, to najpierw musimy znaleźć węzeł z szukanym kluczem. Następnie
przechodząc drzewo in-order znajdujemy następcę usuwanego węzła. Najprościej
mówiąc idziemy jeden krok w prawo, a następnie cały czas w lewo, aż do liścia,
lub też jeden krok w lewo, a później cały czas w prawo aż do liścia. To
gwarantuje znalezienie nowego korzenia poddrzewa, które będzie spełniało
wszystkie założenia BST.

## Implementacja

```
// C
typedef struct Node {
    int key;
    struct Node* p_left;
    struct Node* p_right;
} Node;

void insert(Node** pp_root, int key) {
    Node* p_new     = (Node*)malloc(sizeof(Node));
    p_new->key      = key;
    p_new->p_left   = (void*)0;
    p_new->p_right  = (void*)0;

    if (!*pp_root) {
        *pp_root = p_new;
        return;
    }

    Node* tmp = *pp_root;
    while(tmp) {
        if (key < tmp->key) {
            if (!tmp->p_left) {
                tmp->p_left = p_new;
                break;
            }
            tmp = tmp->p_left;
        } else {
            if (!tmp->p_right) {
                tmp->p_right = p_new;
                break;
            }
            tmp = tmp->p_right;
        }
    }
}

Node* search(const Node* p_root, int key) {
    if (!p_root) { return (void*)0; }
    Node* p_tmp = p_root;
    while(p_tmp) {
        if (p_tmp->key == key) { return p_tmp; }
        p_tmp = key < p_tmp->key ? p_tmp->p_left : p_tmp->p_right;
    }
}

void delete(Node** pp_root, int key) {
    if (!*pp_root) { return; }

    if ((*pp_root)->key == key) {
        if (!(*pp_root)->p_right) {
            Node* p_tmp = *pp_root;
            *pp_root = (*pp_root)->p_left;
            free(p_tmp);
        } else {
            Node*p_tmp = (*pp_root)->p_right;
            while(p_tmp->p_left) { p_tmp = p_tmp->p_left; }
            (*pp_root)->key = p_tmp->key;
            free(p_tmp);    /**
                             * Dangling pointer on the parent of p_tmp, but it'd
                             * take a lot more code to do it "right"
                             */
        }
        return;
    }

    Node* p_tmp = *pp_root;
    while(p_tmp) {
        if (p_tmp->key == key) { break; }
        p_tmp = key < p_tmp->key ? p_tmp->p_left : p_tmp->p_right;
    }
    if (!p_tmp) { return; }

    // do the same as above, just treat p_tmp as *pp_root
}
```