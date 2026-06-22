# 13. Jak tworzyć manipulatory argumentowe i bezargumentowe w strumieniach: omów budowę i działanie.

## Definicja

Manipulatory to funkcje lub obiekty funkcyjne wywoływane poprzez podanie ich nazw
jako elementów wstawianych do lub wyjmowanych ze strumienia. Ich działanie może,
ale nie musi, polegać na modyfikacji flagi stanu formatowania strumienia.
[Programowanie Obiektowe, wyk15 s 405]

## Tworzenie

Tworzenie manipulatora polega na przeciążeniu operatora <<. Aby stworzyć
manipulator bezargumentowy, wystarczy stworzyć funkcję:

```
inline std::ostream& hello(std::ostream& ostream) {
	return ostream << "hello";
}

{
    std::cout << hello << " user!\n";
}
```

Podczas wywołania jej "w strumieniu", operator wykonuje swoje zadanie, w tym
przypadku wstawiając napis "hello".

W przypadku manipulatora argumentowego musi to już być klasa, aby przekazany
argument mógł zostać gdzieś przechowany:

```
class Messenger {
public:
	Messenger(const std::string& message) : m_message(message) {}
	friend std::ostream& operator<<(std::ostream& ostream, const Messenger& messenger) {
		return ostream << messenger.m_message;
	}
private:
	const std::string m_message;

};

{
    std::cout << Messenger("custom message") << "\n";
}
```

Tym razem to użytkownik decyduje co zostanie wypisane do konsoli za pomocą
manipulatora. Manipulatory mogą być bardziej złożone, umożliwiając "owijanie"
fragmentów strumienia w nawiasy, cudzysłowy etc lub operacje takie jak
wielokrotne wypisywanie tego, co znajdą na wejściu. Mogą także ustawiać flagi
strumienia, aby np kolorować czy formatować tekst, a także robić różne inne
dziwne rzeczy.