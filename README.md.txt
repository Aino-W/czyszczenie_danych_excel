# Portfolio: Czyszczenie danych w Excelu

W tym repozytorium znajdują się pliki z wyczyszczonymi danymi. Poniżej znajdują się opisy przeprowadzonych działań dla poszczególnych baz.

---

## 📁 20260319 inventory

1. **Utworzenie tabeli:** Przygotowanie podstawowej struktury danych.
2. Kolumna `warehouse_country`:
   * Ujednolicenie nazewnictwa krajów.
   * Dostosowanie danych do jednego, spójnego języka.
3. Kolumna `last_stock_update`:
   * Sprawdzenie poprawności i ujednolicenie formatu dat.
   * Usunięcie pustych komórek (braków danych).
   * Usunięcie komórek zawierających błędy (np. `"not_a_date"`).
   * Usunięcie nierealnych dat (np. `"2024-13-40"`).
   * Uznanie dat w formacie "RRRR-MM" za pierwszy dzień miesiąca.

---

## 📁 20260320 products

**Wielkość danych:** ok. 2500 rekordów

Poniżej znajdują się kroki podjęte w celu oczyszczenia bazy:

1. **Utworzenie tabeli:** Przygotowanie podstawowej struktury danych.
2. **Rozdzielenie danych** na kolumny.
3. **Utworzenie tabeli** ułatwiającej dalszą analizę.
4. **Formatowanie cen:** Zmiana kropki na przecinek oraz dodanie odpowiedniej waluty.
5. **Czyszczenie dat:** Usunięcie nieprawidłowych dat typu `"2024-13-40"` lub niepełnych dat `"2017-05"` (łącznie **7 sztuk**).
6. **Usuwanie braków i błędów:** Usunięcie pustych komórek i wpisów `"not_a_date"` (łącznie **97 sztuk**).