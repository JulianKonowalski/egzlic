# 15. Mechanizm wyjątków w C++ - typy, sposób przechwytywania, obsługa, zalecenia dotyczące rzucania wyjątków w konstruktorach i destruktorach

## Typy

Typ wyjątku może być dowolny. Biblioteka standardowa C++ dostarcza podstawowe
typy wyjątków, np.
* exception - typ bazowy dla wszystkich wyjątków
* logic_error
* runtime_error
* invalid_argument
* domain_error
* length_error
* out_of_range
* range_error
* overflow_error
* underflow_error

Po każdym z tych typów można dziedziczyć i tworzyć własne, bardziej specyficzne
typy wyjątków.

## Przechwytywanie i obsługa

Wyjątek można przechwycić w bloku try-catch:

```
{
    try {
        possibly_throw();
    } catch (ErrorType& error) {
        // handle error
    }
}
```

W razie gdyby w bloku try mogło się pojawić kilka typów wyjątków, można
przygotować handlery dla każdego z nich:

```
{
    try {
        possibly_throw();
    } catch (ErrorType1& error) {
        // handle error of type ErrorType1
    } catch (ErrorType2& error) {
        // handle error of type ErrorType2
    }
}
```

Można również złapać cokolwiek, ale to już brzmi jak desperacja:

```
{
    try {
        possibly_throw();
    } catch (...) {
        // handle something (?)
    }
}
```

Z bloku catch również można rzucić wyjątek, ale nie będę tego nawet komentował:

```
{
    try {
        possibly_throw();
    } catch (std::runtime_error& error) {
        // handle error
        throw std::runtime_error("Have fun up there!");
    }
}
```

## Zalecenia dotyczące rzucania wyjątków w konstruktorach i destruktorach

W konstruktorach można, a kierując się RAII nawet trzeba rzucać wyjątki, jeśli
coś pójdzie nie tak podczas tworzenia obiektu. Nie dopuści to do sytuacji
stworzenia niepoprawnej instancji, której możnaby nieświadomie używać, generując
trudne do wykrycia błędy.

```
class OpenGLWindow {
    // implementation
};

{
    try {
        OpenGLWindow window(800, 600, "My first OpenGL triangle");
    } catch (std::runtime_error& e) {
        // haha you're using Apple, aren't you?
    }
}
```

Z destruktorów nie należy rzucać wyjątków. W sytuacji gdzie rzucamy jakiś
wyjątek, to stos przypisany do wywołania funkcji/metody, która ten wyjątek rzuca
jest zwalniany. Jeśli w tym czasie którykolwiek zasób zaalokowany na tym stosie
rzuci kolejny wyjątek, to nie zdołamy go przechwycić, a program wyjdzie dwa
poziomy wyżej lub w najgorszym wypadku się zatrzyma, nawet jeśli funkcjonalność
rzucająca oba wyjątki została owinięta w blok try-catch. Wrócenie się o kilka
poziomów wywołań lub zatrzymanie programu w ten sposób byłoby kompletnie bez
sensu, biorąc pod uwagę, że byliśmy w stanie obsłużyć oryginalny wyjątek i
poprawnie wyjść z błędnego stanu programu.