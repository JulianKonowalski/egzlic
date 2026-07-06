# 25. Na czym polegają więzy klucza głównego oraz spójności referencyjnej (klucza obcego) i jak się je definiuje?
Więzy te tworzą relację pomiędzy tabelami. Dla przykładu, jeśli mamy tabelę
zawierającą sale lekcyjne oraz tabelę zawierającą budynki na kampusie uczelni,
to możemy stworzyć relację pomiędzy dwoma tabelami, zapisując klucz główny
budynku uczelni w każdym rekordzie należącym do tabeli z salami. W ten sposób
tworząc salę, przypisujemy ją do jakiegoś budynku. Ważne jest to, aby klucze
używane do tworzenia więzów były unikalne w swoich tabelach.

Aby stworzyć takie powiązanie należy w jednej z tabel umieścić kolumnę odnoszącą
się do klucza głównego innej tabeli. Załóżmy, że w tabeli ROOMS przypisujemy
wartość kolumny id z tabeli BUILDINGS do kolumny building_id:

```
CREATE TABLE IF NOT EXISTS 'ROOMS' (
    ...
    'building_id' int unsigned NOT NULL,
    FOREIGN KEY (building_id) REFERENCES 'BUILDINGS'('id'),
    ...
);
```

Oczywiście aby polecenie się wykonało poprawnie, tabela BUILDINGS musi już
istnieć. Dodatkowo rząd building_id w tabeli ROOMS musi być tego samego typu
danych, co rząd id w tabeli BUILDINGS (typy danych czasem mogą być castowane,
np. ze stringa na inta, ale to jest proszenie się o kłopoty).