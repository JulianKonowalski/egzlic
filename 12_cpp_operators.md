# 12. Omów dla języka C++ metody tworzenia przeciążonych operatorów oraz uzasadnij potrzebę ich stosowania.

## Tworzenie

Metoda jest jedna - napisanie przeciążonego operatora. Możemy go umieścić w
kilku miejscach lub napisać kilka jego wersji, ale zachowanie operatora zależy
od nas.

```
class Vec3 {
public:
    // constructor, destructor, yadda yadda 

    Vec3 operator+(const Vec3& other) {
        return Vec3(
            m_vals[0] + other.m_vals[0],
            m_vals[1] + other.m_vals[1],
            m_vals[2] + other.m_vals[2]
        );
    }

    const Vec3& operator=(const Vec3& other) {
        for (int i = 0; i < 3; ++i) { m_vals[i] = other.m_vals[i]; }
        return *this;
    }

    Vec3 operator+(const int& v) {
        return Vec3(
            m_vals[0] + static_cast<float>(v),
            m_vals[1] + static_cast<float>(v),
            m_vals[2] + static_cast<float>(v)
        );
    }
private:
    float m_vals[3];
}

{
    Vec3 v1(1.0, 2.0, 3.0);
    Vec3 v2(4.0, 5.0, 6.0);
    Vec3 v3 = v1 + v2;
    v3 = v3 + 1;
}
```

## Potrzeba zastosowania

Potrzeba ich zastosowania? Żadna. To samo, a do tego w jaśniejszy sposób byśmy
osiągnęli pisząc to nieobiektowo:
```
// C
typedef struct vec3 { float v[3]; } vec3;

void vec3_add(const vec3* p_lhs, const vec3* p_rhs, vec3* p_out) {
    p_out->v[0] = p_lhs->v[0] + p_rhs->v[0];
    p_out->v[1] = p_lhs->v[1] + p_rhs->v[1];
    p_out->v[2] = p_lhs->v[2] + p_rhs->v[2];
}
```

O ile na vec3 to się fajnie sprawdza, tak przy obiektach niezwiązanych z algebrą
liniową czy ogólną matematyką niesie to coraz mniejsze korzyści. Jeśli np byśmy
mieli obiekty typu słuchawki to jak zdefiniujemy ich dodawanie? Impedancja się
zwiększa czy zostaje ta sama? Zakres odpowiedzi częstotliwościowej jest szerszy?
Poza tym już na wektorze widać dziury w tej logice - operator mnożenia oznaczałby
iloczyn skalarny czy wektorowy dwóch wektorów? Nie musimy przechodzić przez takie
rozterki kiedy nazwa funkcji mówi nam bardzo jasno o wyniku operacji.

Addendum (Sławek Brzózka): Poza algebrą liniową i operatorami porównania, 
które są względnie mało kontrowersyjne, przydatne potrafią być operatory indeksowania
(`[]`, `()`) przy implementacji własnych kontenerów. Z kolei operatory `*` i `->` są
sensowne w kontekście iteratorów lub smart pointerów, ponieważ jedynie odtwarzają
zachowanie wskaźników dobrze znane z C. Poza tym dołączam się do krytyki; przez
dziwaczne pomysły z `<<` C++ miał najbardziej składniowo przekombinowane "Hello World"
ze wszystkich rozsądnych języków programowania. Na szczęście ktoś poszedł 
po rozum do głowy i dodali `<print>` w C++23.