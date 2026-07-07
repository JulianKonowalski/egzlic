# 28. Sposoby zapewnienia jakości wytwawrzanego oprogramowania.

Sposoby dzielą się na kilka kategorii:
* zarządzanie projektem
* testowanie oprogramowania
* dostosowanie oprogramowania do norm i wymogów obowiązujących w danej
dziedzinie

## Zarządzanie projektem

Mamy dwie, najbardziej charakterystyczne metodyki zarządzania projektem:

* waterfall - kroki oraz wymogi dotyczące wytwarzanego oprogramowania są jasno
określone na początku i nie ulegają zmianie w czasie projektu
* agile - kroki oraz wymogi nie są jasno określone, zespół wybiera i wykonuje
drobne zadania w zależności od bieżących potrzeb projektu

Tutaj pojawiają się określenia takie jak scrum, kanban oraz narzędzia w postaci
Trello, Jiry itp. Są to rzeczy powiązane z metodyką zwinną (agile) pozwalające
lepiej planować krótkie okresy prac (sprinty) i mierzyć postęp zespołu.
Narzędzia wykorzystywane w metodyce zwinnej w większości mogą zostać
wykorzystane w metodyce waterfall.

## Testowanie oprogramowania

Sposobem na twarde określenie jakości oprogramowania (poprawnego działania,
odpowiedniej wydajności, odporności na obciążenie systemu) są różnego rodzaju
testy oprogramowania. Zazwyczaj wyróżnia się poniższe typy testów:

* testy jednostkowe - weryfikacja poprawności logiki działania małych fragmentów
kodu, takich jak funkcje, klasy czy moduły. Testom zazwyczaj podlega tylko i
wyłącznie publiczny interfejs danej jednostki (zwłaszcza w OOP).
* testy integracyjne - weryfikacja poprawności logiki działania zestawu
jednostek w celu sprawdzenia, czy oddzielne klasy oraz moduły współpracują ze
sobą w zamierzony sposób
* testy systemowe - weryfikacja poprawności logiki działania całego systemu w
celu sprawdzenia czy wymagane funkcjonalności systemu zostały spełnione
* testy obciążeniowe - weryfikacja odporności systemu na obciążenie, na przykład
testowanie serwera pod kątem jego zdolności do obsłużenia określonej ilości
zapytań w ciągu jakiegoś okresu

## Dostosowanie oprogramowania do norm i wymogów obowiązujących w danej dziedzinie

Ten punkt można po części zaliczyć do testowania oprogramowania, jednakże
spełnienie jakiejś funkcjonalności nie jest jednoznaczne ze spełnieniem norm
obowiązujących w prawie. Dla przykładu - jeśli użytkownik wykonuje jakąś
transakcję internetową, która się nie powiedzie, to pieniądze z jego konta nie
zostaną ściągnięte, ale połączenie pomiędzy użytkownikiem, a usługą nie było
szyfrowane. Z punktu widzenia użytkownika system działa poprawnie, ale nie
spełnia szeregu norm, będąc skrajnie podatnym na ataki z zewnątrz.