# Czyszczenie danych w Excelu

Poniższy projekt — czyszczenie danych — jest jednym z etapów większego projektu analitycznego. To jeden z ważniejszych kroków w całym procesie, bo jeśli dane są brudne, to żadna analiza nie ma sensu — wyniki sprzedaży, cen czy sezonowości byłyby po prostu nieprawdziwe.
Projekt zawierał wiele błędów m.in.: nieistniejące daty (`2024-13-40`), wpisy `"not_a_date"`, puste komórki, nazwy krajów w różnych językach i formatach, błędny separator w cenach, zamówienia z ilością 0 lub bez produktu, sześć wariantów tych samych statusów oraz podejrzane powtarzające się wartości w kolumnie quantity.
Poniżej opisuję szczegółowo, co i jak poprawiłam w każdym pliku.

---

## 📁 20260319 inventory

1. **Utworzyłam tabelę** — najpierw zamieniłam zakres danych na tabelę, żeby łatwiej się na nim pracowało.

2. **Kolumna `warehouse_country`** — nazwy krajów były wpisane na różne sposoby (różne języki, różna pisownia). Ujednoliciłam je wszystkie do jednego, spójnego formatu.

3. **Kolumna `last_stock_update`** — ta kolumna sprawiała najwięcej problemów:
   - Daty były zapisane w różnych formatach, więc je ustandaryzowałam.
   - Usunęłam puste komórki.
   - Usunęłam wpisy takie jak `"not_a_date"`, które w ogóle nie były datami.
   - Usunęłam daty, które fizycznie nie mogą istnieć, np. `"2024-13-40"`.
   - Daty zapisane tylko jako rok i miesiąc (np. `"2024-05"`) potraktowałam jako pierwszy dzień danego miesiąca.

---

## 📁 20260320 products

* około 2500 wierszy

1. **Utworzyłam tabelę** — tak samo jak wyżej, dla wygody pracy.

2. **Rozdzieliłam dane na kolumny** — część danych była "sklejona" w jednej komórce i trzeba było je rozdzielić.

3. **Poprawiłam formatowanie cen** — zamieniłam kropki na przecinki i dodałam oznaczenie waluty.

4. **Wyczyściłam daty** — usunęłam daty niemożliwe (np. `"2024-13-40"`) oraz niepełne (np. `"2017-05"`). Takich przypadków było łącznie **7**.

5. **Usunęłam braki i błędy** — puste komórki oraz wpisy `"not_a_date"` — łącznie **97 przypadków**.

---

## 📁 20260508 sales_orders

**Narzędzie:** Excel Power Query  
**Rozmiar pliku:** około 260 000 wierszy

To był zdecydowanie największy i najbardziej wymagający zestaw danych.

---

### Kolumna `order_id`
- Zmieniłam typ danych na Tekst.
- Użyłam funkcji Przytnij, żeby usunąć ukryte spacje, które mogłyby powodować problemy przy wyszukiwaniu.
- Usunęłam puste wiersze.

---

### Kolumna `customer_id`
- Zmieniłam typ na Tekst.
- Zastosowałam Trim, tak samo jak wyżej.

---

### Kolumna `order_date`
- Przekonwertowałam wartości na typ Data.
- Usunęłam błędy — niektóre daty były uszkodzone lub nie miały sensu i nie dały się przekonwertować. Takie wiersze po prostu wyrzuciłam.

---

### Kolumna `country`
- Użyłam Trim, żeby pozbyć się zbędnych spacji.
- Ujednoliciłam wielkość liter — każde słowo zaczyna się od wielkiej litery.
- Ustandaryzowałam nazwy krajów, np. `"PL"` zamieniłam na `"Poland"`.

---

### Kolumna `product_id`
- Zmieniłam typ na Tekst.
- Zastosowałam Trim.
- Usunęłam puste wiersze — zamówienie bez przypisanego produktu nie ma sensu.

---

### Kolumna `quantity`
- Ustawiłam typ na Liczba całkowita.
- Usunęłam wiersze z wartością 0 — zerowa ilość to albo błąd, albo zwrot.
- Znalazłam kilka zamówień na dokładnie **608 sztuk** tego samego produktu. Po sprawdzeniu uznałam, że to śmieciowe dane — taka liczba pojawiała się podejrzanie regularnie i nie wyglądała na prawdziwe zamówienie. Odfiltrowałam te wiersze, żeby nie zawyżały wyników.

---

### Kolumna `unit_price`
- Zamieniłam kropki na przecinki (wymagane przez polskie ustawienia regionalne).
- Przekonwertowałam na Liczbę dziesiętną.
- Usunęłam rekordy z ceną równą 0 — produkt bez ceny to błąd w danych.

---

### Kolumna `discount`
- Zamieniłam kropki na przecinki.
- Przekonwertowałam na Liczbę dziesiętną.
- Puste komórki uzupełniłam wartością `0` — jeśli rabat nie był wpisany, przyjęłam założenie, że po prostu nie był naliczony. Dzięki temu kolumna nadaje się do obliczeń.

---

### Kolumna `status`
- Zastosowałam Trim.
- Ujednoliciłam wielkość liter (każde słowo od wielkiej litery).
- Oryginalnie status miał **6 różnych wariantów nazewnictwa** — zredukowałam je do **3 ustandaryzowanych**:
  - `"Complete"` i `"Done"` → `"Completed"`
  - `"Ship"` → `"Shipped"`
  - Synonimy `"Cancelled"` → `"Cancelled"`
