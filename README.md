 Czyszczenie danych w Excelu

W tym repozytorium znajdują się pliki z wyczyszczonymi danymi. Poniżej znajdują się opisy przeprowadzonych działań dla poszczególnych baz.

---

📁 20260319 inventory

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

📁 20260320 products

**Wielkość danych:** ~2500 wierszy

1. **Utworzenie tabeli:** Przygotowanie podstawowej struktury danych.
2. **Rozdzielenie danych** na kolumny.
3. **Utworzenie tabeli** ułatwiającej dalszą analizę.
4. **Formatowanie cen:** Zmiana kropki na przecinek oraz dodanie odpowiedniej waluty.
5. **Czyszczenie dat:** Usunięcie nieprawidłowych dat typu `"2024-13-40"` lub niepełnych dat `"2017-05"` (łącznie **7 sztuk**).
6. **Usuwanie braków i błędów:** Usunięcie pustych komórek i wpisów `"not_a_date"` (łącznie **97 sztuk**).

---

📁 20260508 sales_orders

Narzędzie: Excel Power Query
Zakres danych: ~260,000 wierszy

### 1. Kolumna order_id
* Typ danych: Zmieniono na Tekst
* Czyszczenie tekstu: Zastosowano operację Przytnij (Trim), usuwając ukryte spacje.
* Filtrowanie: Usunięto puste wiersze (null).

### 2. Kolumna customer_id
* Zmieniono na Tekst 
* Czyszczenie tekstu: Zastosowano operację Przytnij (Trim).

### 3. Kolumna order_date
* Skonwertowano na Datę.
* Czyszczenie błędów: Zastosowano funkcję Usuń błędy (Remove Errors), aby wyeliminować wiersze z uszkodzonymi lub nielogicznymi wpisami dat, które nie poddały się transformacji.

### 4. Kolumna country
* Zastosowano operację Przytnij (Trim).
* Wymuszono format wielkich liter / każdego wyrazu od wielkiej litery, ujednolicając zapis.
* Ujednolicenie nazw państw np. PL -> POLAND

### 5. Kolumna product_id
* Zmieniono na Tekst.
* Zastosowano operację Przytnij (Trim).
* Wykluczono wartości puste (null), usuwając błędy systemowe (zamówienia bez przypisanego towaru).

### 6. Kolumna quantity
* Ustawiono na Liczba całkowita.
* Odznaczono wartość 0, pozostawiając wyłącznie poprawne transakcje (eliminacja błędów i zwrotów).
* Usunięcie nienaturalnych zamówień: Zidentyfikowano kilka transakcji na dokładnie 608 sztuk produktu. Po przyjrzeniu się tym wierszom uznano to za błąd (tzw. śmieciowe dane). Ta konkretna liczba została odfiltrowana, by nie zawyżać sztucznie naszych wyników sprzedaży.

### 7. Kolumna unit_price
* Zamieniono kropki (.) na przecinki (,), aby dostosować dane do polskich ustawień regionalnych i uniknąć błędów konwersji.
* Skonwertowano na Liczbę dziesiętną.
* Usunięto rekordy z ceną 0.

### 8. Kolumna discount
* Zamieniono kropki na przecinki.
* Skonwertowano na Liczbę dziesiętną.
* Puste komórki (null) zastąpiono wartością 0. Przyjęto biznesowe założenie, że brak wpisu oznacza brak naliczonego rabatu, co przygotowało kolumnę do bezpiecznych operacji matematycznych.

### 9. Kolumna status
* Zastosowano operację Przytnij (Trim).
* Użyto opcji Każdy wyraz od wielkiej litery (Capitalize Each Word), ujednolicając zapis (np. "completed" i "Completed").
* Zredukowano 6 wariantów nazewnictwa do 3 ustandaryzowanych statusów za pomocą funkcji Zamień wartości: Complete oraz Done -> Completed, Ship -> Shipped.
* Zunifikowano synonimy dla statusu Cancelled.
