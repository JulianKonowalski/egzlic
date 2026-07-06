# 24. Omów podstawowe części kwerendy SQL oraz kolejność ich wykonywania. Uwzględnij funkcje grupujące.

Pytanie jest sformułowane w sposób sugerujący, że chodzi o zapytanie typu SELECT,
zatem to omówię:

# Wybranie rzędu tabeli
Pierwszą częścią kwerendy jest zaznaczenie co i skąd chcemy wybrać. Powiedzmy,
że interesują nas użytkownicy z tabeli USERS i jesteśmy już zalogowani do bazy
danych na konto posiadające odpowiednie uprawnienia itd.

```
SELECT * FROM USERS u;
```

Zapytanie to zwróci wszystkich użytkowników znajdujących się w bazie danych.
Następnie, jeśli chcemy przefiltrować wpisy, to możemy dodać kontynuację
zapytania. Załóżmy, że interesują nas użytkownicy z wartością identyfikatora
mniejszą od 100:

```
SELECT * FROM USERS u WHERE u.id < 100;
```

Teraz zapytanie zwróci użytkowników, których identyfikator jest mniejszy niż 100.
Następnie, jeśli chcemy jakoś posortować otrzymane elementy, należy wybrać klucz
oraz typ sortowania. Posortujmy użytkowników malejąco względem ich
identyfikatora:

```
SELECT * FROM USERS u WHERE u.id < 100 ORDER BY u.id DESC;
```

Ostatnią operacją jaką możemy wykonać to ogarniczenie liczby wyników do
określonej wartości. Wybierzmy tylko 10 pierwszych użytkowników, którzy
spełniają warunki kwerendy:

```
SELECT * FROM USERS u WHERE u.id < 100 ORDER BY u.id DECS LIMIT 10;
```