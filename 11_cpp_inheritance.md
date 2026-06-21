# 11. Omów dla wybranego języka obiektowego mechanizm dziedziczenia ze zszczególnym uwzględnieniem polimorfizmu.

## Definicja
Oczywiście omówię dla C++. Dziedziczenie polega na transferze funkcjonalności z
klasy bazowej (rodzica) na klasę dziedziczącą (dziecko). W wyniku dziedziczenia
dziecko przejmuje zarówno interfejs (metody) jak i dane (pola) rodzica:

```
// C++
class Base {
public:

    Base(void) : m_int(0), m_float(0.0f) {}
    ~Base(void) = default;
    int get_int(void) { return m_int; }
    
protected:

    float set_float(const float v) { m_float = v; }

private:

    int m_int;
    float m_float;

};

class Child : public Base {
public:
    using Base::Base;
};
```

C++ posiada kilka trybów dziedziczenia, których nie będę omawiał, bo komisji to
nie obchodzi.

C++ również umożliwia oznaczanie klas specjalnymi keywordami, aby użytkownik nie
mógł po nich dziedziczyć, ale nie będę tego omawiał bo komisji to nie obchodzi.

C++ również umożliwia przekazywanie klas bazowych jako template do klas
dziedziczących oraz sprawdzanie czy klasa będąca argumentem spełnia pewne wymogi
za pomocą conceptów, czego też nie będę omawiał bo komisji to nie obchodzi.

C++ również umożliwia sprawdzanie czy klasa może dziedziczyć po danej klasie,
również za pomocą conceptów ale nie będę tego omawiał, bo komisji to nie obchodzi.

C++ również umożliwia wielodziedziczenie i tworzenie error traceów wykraczających
poza najśmielsze oczekiwania twórców języka, czego też nie będę omawiał bo komisji
to nie obchodzi.

## Polimorfizm

Polimorfizm pozwala na określenie wymaganej funkcjonalności klasy dziedziczącej
poprzez stworzenie interfejsu klasy w klasie bazowej. Podczas dziedziczenia po
klasie bazowej, użytkownik musi zaimplementować wymagany interfejs aby program
mógł się skompilować:

```
// C++

class Base {
public:
    Base(void) = default;
    ~Base(void) = default;
    virtual void do_something(void) = 0;    /**
                                             * Oznaczenie braku implementacji
                                             * tej metody, utworzenie instancji
                                             * klasy Base będzie niemożliwe.
                                             */
};

class BetterChild : public Base {
public:
    using Base::Base;
    void do_something(void) override {
        std::cout << "I'm the better child, parents love me more" << std::endl;
    }   /* Implementacja wymaganej funkcjonalności w klasie dziedziczącej. */
};

class WorseChild : public Base {
public:
    using Base::Base;
    void do_something(void) override {
        std::cout << "I'm the worse child, I'll hang myself eventually" << std::endl;
    }   /* Implementacja wymaganej funkcjonalności w klasie dziedziczącej. */
};
```

Aby polimorfizm zadziałał, musimy zrzutować instancje klasy do klasy bazowej.
Oznacza to, że pamięć musi być przekazywana przez wskaźniki lub referencje do
zmiennej o bazowym typie `Base`.

```
{ // C++
    BetterChild child1;
    WorseChild child2;

    std::vector<Base*> children;
    children.push_back(&child1);
    children.push_back(&child2);

    for(const auto* child : children) { child->do_something(); }
}
```

Wymóg posługiwania się wskaźnikami utrudnia wykorzystywanie tej funkcjonalności
w środowiskach o ograniczonych zasobach lub uniemożliwiających dynamiczną
alokację pamięci bez implementacji własnego alokatora. Z tego powodu odchodzi
się od tego typu polimorfizmu na rzecz compile-time polimorfizmu z wykorzystaniem
conceptów.