# Typy danych – ćwiczenia

**Projektowanie oprogramowania | Technik programista | Klasa II**
Dział I: Typy danych w projektowaniu aplikacji
Efekty kształcenia: **INF.04.3.1**, **INF.04.3.2**
Opracował: **Bartosz Bryniarski**

---

## Jak korzystać z tego materiału

Ćwiczenia są przypisane do sześciu lekcji działu. Zadania oznaczone **[K]** można wykonać na komputerze (Python w konsoli, dowolne IDE), pozostałe rozwiązuje się na kartce.

Klucz odpowiedzi znajduje się na końcu pliku.

| Lekcja | Temat | Ćwiczenia |
|---|---|---|
| 1 | Rola typów danych. Typowanie statyczne i dynamiczne | 1.1 – 1.5 |
| 2 | Typy liczbowe stałoprzecinkowe | 2.1 – 2.6 |
| 3 | Typy zmiennoprzecinkowe | 3.1 – 3.6 |
| 4 | Typ logiczny i znakowy. Kodowanie znaków | 4.1 – 4.7 |
| 5 | Typ łańcuchowy | 5.1 – 5.6 |
| 6 | Dobór typu prostego do problemu programistycznego | 6.1 – 6.5 |

---

# Lekcja 1. Rola typów danych. Typowanie statyczne i dynamiczne

### Ćwiczenie 1.1 – Trzy cechy typu

Dla każdego typu wypełnij tabelę.

| Typ | Przykładowe wartości | Dozwolone operacje | Rozmiar w pamięci |
|---|---|---|---|
| `bool` | 	true, false | Logiczne | 1 bajt |
| `int32` | -2147483648, 0, 42 | Arytmetyczne, porównania, bitowe | 4 bajty |
| `char` | 'a', 'Z', '9', '\n' | Porównania, przypisanie, inkrementacja | 1 lub 2 bajty |

### Ćwiczenie 1.2 – Statyczne czy dynamiczne

Przy każdym fragmencie napisz, czy język stosuje typowanie **statyczne** czy **dynamiczne**, i uzasadnij jednym zdaniem.

```
a)  int x = 5;  x = "tekst";      → błąd przy kompilacji   Statyczne - ponieważ typ zmiennej jest sprawdzany w trakcie kompilacji i nie można przypisać wartości tekstowej do zmiennej liczbowej
b)  x = 5;      x = "tekst"       → działa poprawnie       Dynamiczne - ponieważ zmienna nie ma sztywnego typu i może swobodnie zmieniać go w trakcie działania programu.
c)  auto y = 3.14;                → y jest typu double     Statyczne - ponieważ kompilator automatycznie dopasowuje stały typ na podstawie przypisanej wartości przed uruchomieniem programu.
d)  let z = 10; z = "dziesięć";   → działa w JavaScripcie  Dynamiczne - ponieważ JavaScript określa typy wartości w czasie wykonywania kodu, co pozwala na zmianę typu zmiennej z.
```

### Ćwiczenie 1.3 – Silne czy słabe

Rozstrzygnij, co zwróci każde wyrażenie. Jeśli będzie to błąd – napisz „błąd".

| Wyrażenie | Python | JavaScript |
|---|---|---|
| `"5" + 3` | błąd | "53" |
| `"5" * 2` | "55" | 10 |
| `"10" - 5` | błąd | 5 |
| `True + 1` | 2 | 2 |

### Ćwiczenie 1.4 – Konwersje

Podaj wynik każdej konwersji.

```
a)  (int) 7.99            = 7
b)  (int) -7.99           = -7
c)  (double) 5            = 5.0
d)  (int) 3.5 + (int) 3.5 = 6
e)  (int)(3.5 + 3.5)      = 7
```

Wyjaśnij, dlaczego wyniki `d` i `e` się różnią.

D - W przykładzie d rzutowanie wykonuje się przed dodawaniem: liczby 3.5 są skracane do 3, co daje wynik 3 + 3 = 6.
E - W przykładzie e nawias wymusza najpierw dodawanie: 3.5 + 3.5 daje 7.0, co po rzutowaniu na typ całkowity daje 7.

### Ćwiczenie 1.5 [K] – Sprawdź w konsoli

W konsoli Pythona wykonaj:

```python
print(type(5), type(5.0), type("5"), type(True))
print(int("42") + 8)
print(int("42abc"))
```

Zapisz, jaki wyjątek zwraca ostatnia linia i co on oznacza.

Wyjątek ValueError oznacza, że funkcja otrzymała argument o właściwym typie (w tym przypadku napis/string), ale o niepoprawnej wartości, której nie da się przekształcić na liczbę całkowitą. Funkcja int() potrafi przetłumaczyć na system dziesiętny tylko te teksty, które składają się wyłącznie z cyfr (i opcjonalnie znaku plus/minus). Litery "abc" uniemożliwiają wykonanie tej konwersji.

---

# Lekcja 2. Typy liczbowe stałoprzecinkowe

### Ćwiczenie 2.1 – Zakresy

Uzupełnij tabelę. Wartości zapisz w postaci liczbowej, nie wzorem.

| Liczba bitów | Liczba wartości | Zakres bez znaku | Zakres ze znakiem |
|---|---|---|---|
| 4 | 16 | od 0 do 15| 0d -8 do 7 |
| 8 | 256 | od 0 do 255 | od -128 do 127 |
| 16 | 65536 | od 0 do 65535 | od -32768 do 32767 |

### Ćwiczenie 2.2 – Konwersja dwójkowo-dziesiętna

Zamień na system dziesiętny (liczby bez znaku):

```
a)  0000 1111  = 15
b)  1000 0000  = 128
c)  1111 1111  = 255
```

A teraz te same bajty odczytane jako liczby **ze znakiem** w kodzie U2:

```
a)  0000 1111  = 15
b)  1000 0000  = -128
c)  1111 1111  = -1
```

### Ćwiczenie 2.3 – Przepełnienie

Zmienna typu `int8` (zakres −128 … 127) ma wartość 120. Program dodaje do niej 10 w pętli. Wypisz kolejne wartości:

```
120 → 130 (błąd przepełnienia, czyli -126) → -116 → -106
```

Po ilu krokach wartość stanie się ujemna?

Wartość stanie się ujemna już po 1 kroku.

### Ćwiczenie 2.4 – Dzielenie całkowite

Podaj wyniki:

```
a)  17 / 5    (liczby całkowite)  = 17 / 5 = 3
b)  17 % 5                        = 17 % 5 = 2
c)  -17 / 5   (liczby całkowite)  = -17 / 5 = -3
d)  Ile stron po 20 rekordów potrzeba na 143 rekordy?  = 8
```

Zapisz wzór ogólny na liczbę stron przy `n` rekordach i `k` rekordach na stronie.

### Ćwiczenie 2.5 – Dobór typu

Dla każdej danej dobierz najmniejszy wystarczający typ całkowity i uzasadnij.

| Dana | Typ | Uzasadnienie |
|---|---|---|
| Wiek człowieka | uint8 / byte | Wiek jest zawsze dodatni i nie przekracza 255 lat, więc idealnie mieści się w 1 bajcie bez znaku. |
| Rok kalendarzowy | uint16 / ushort | Lata bieżące i przewidywalna przyszłość (ponad 65 tysięcy lat) bez problemu zmieszczą się w 2 bajtach bez znaku. |
| Liczba mieszkańców Polski | uint32 / uint | Populacja Polski (ok. 38 mln) przekracza zakres 2 bajtów (65 535), ale mieści się w 4 bajtach bez znaku (do ok. 4,29 mld). |
| Liczba mieszkańców Ziemi | uint64 / ulong | Ludzkość liczy obecnie ponad 8 miliardów ludzi, co przekracza limit 4 bajtów bez znaku. Wymagane jest użycie 8 bajtów bez znaku. |
| Liczba bajtów pliku wideo | uint64 / ulong | Współczesne pliki wideo mogą ważyć wiele gigabajtów (miliardów bajtów), co szybko przepełniłoby typ 32-bitowy. Bezpieczny jest typ 8-bajtowy. |
| Temperatura w °C (całkowita) | int8 / sbyte | Temperatura na Ziemi może być ujemna i mieści się w przedziale od ok. -90°C do +60°C, co idealnie pokrywa zakres 1 bajtu ze znakiem (-128 do 127). |

### Ćwiczenie 2.6 [K] – Przepełnienie na własne oczy

W Pythonie zainstalowany jest moduł `numpy`, który używa typów o stałym rozmiarze:

```python
import numpy as np
x = np.int8(127)
print(x + np.int8(1))
```

Zapisz wynik i wyjaśnij go w dwóch zdaniach.

Moduł NumPy stosuje stały, 8-bitowy rozmiar typów (np.int8) o zakresie od -128 do 127. Dodanie jedynki do maksymalnej wartości 127 wywołuje przepełnienie (overflow), przez co licznik automatycznie przewija się do najmniejszej wartości, czyli -128.

---

# Lekcja 3. Typy zmiennoprzecinkowe

### Ćwiczenie 3.1 – float czy double

| Zastosowanie | float czy double | Dlaczego |
|---|---|---|
| Współrzędne GPS z dokładnością do metra | double | Typ float zapewnia tylko ok. 7 cyfr znaczących, co na poziomie równika daje dokładność rzędu kilkunastu metrów; double (15-17 cyfr znaczących) gwarantuje precyzję do pojedynczych milimetrów. |
| Kolor piksela (0.0 – 1.0) | float | W grafice komputerowej miliony pikseli przetwarzane są jednocześnie; float w zupełności wystarcza do zapisu składowych RGB, oszczędzając połowę pamięci i pasma pamięci GPU. |
| Obliczenia naukowe, całkowanie numeryczne | double | Wielokrotne operacje matematyczne kumulują błędy zaokrągleń; double minimalizuje ten efekt (błąd numeryczny), zapewniającej stabilność długich symulacji. |
| Saldo konta bankowego | żaden z nich | Liczby zmiennoprzecinkowe nie potrafią dokładnie reprezentować ułamków dziesiętnych (np. 0.1), co prowadzi do utraty groszy; w bankowości używa się typów stałopozycyjnych (np. decimal) lub przechowuje grosze jako int. |

### Ćwiczenie 3.2 – Zapisywalne czy nie

Zaznacz, które liczby da się zapisać **dokładnie** w systemie dwójkowym:

```
0,5     0,1     0,25     0,3     0,75     0,125     0,2     1,5
```

Podaj regułę, według której rozstrzygasz.

Ułamek dziesiętny można zapisać dokładnie w systemie dwójkowym wtedy i tylko wtedy, gdy po sprowadzeniu go do postaci ułamka zwykłego nieskracalnego, jego mianownik jest potęgą dwójki (np. \(2, 4, 8, 16\dots\)). Mówiąc prościej: część ułamkowa musi dawać się zapisać jako suma skończonej liczby ułamków typu \(\frac{1}{2}\), \(\frac{1}{4}\), \(\frac{1}{8}\), \(\frac{1}{16}\) itd.

### Ćwiczenie 3.3 [K] – Klasyczny przykład

Wykonaj w konsoli:

```python
print(0.1 + 0.2)
print(0.1 + 0.2 == 0.3)
print(f"{0.1:.20f}")
print(0.1 + 0.7)
```

Zapisz wyniki. Który z nich Cię zaskoczył?

print(0.1 + 0.2)  -  0.30000000000000004
print(0.1 + 0.2 == 0.3)  -  False
print(f"{0.1:.20f}")  -  0.10000000000000000555
print(0.1 + 0.7)  -  0.7999999999999999

Zaskoczył mnie wynik 2.

### Ćwiczenie 3.4 – Poprawa kodu

Poniższa funkcja czasem zwraca błędny wynik. Znajdź przyczynę i popraw kod.

```python
def czy_zaplacono(kwota_wplacona, kwota_do_zaplaty):
    if kwota_wplacona == kwota_do_zaplaty:
        return True
    return False
```

Przyczyną błędnego działania funkcji jest użycie operatora dokładnego porównania (==) dla liczb zmiennoprzecinkowych. Ze względu na ograniczenia zapisu binarnego, operacje na ułamkach (takich jak np. 0.1 czy 0.2) generują minimalne błędy zaokrągleń, przez co sumy pozornie równe (np. 0.1 + 0.2) nie są idealnie równe wartości oczekiwanej (0.3).

def czy_zaplacono(kwota_wplacona_grosze, kwota_do_zaplaty_grosze):
    return kwota_wplacona_grosze == kwota_do_zaplaty_grosze

### Ćwiczenie 3.5 – Wartości specjalne

Podaj wynik każdego wyrażenia: liczba, `inf`, `-inf`, `nan` albo błąd.

```
a)  1.0 / 0.0        = inf
b)  -1.0 / 0.0       = inf
c)  0.0 / 0.0        = nan
d)  1 / 0            = błąd   (liczby całkowite)
e)  float('inf') - float('inf')  = nan
f)  float('nan') == float('nan') = false
```

### Ćwiczenie 3.6 – Kwoty pieniężne

Sklep internetowy przechowuje ceny jako `float`. Klient kupuje 3 sztuki towaru po 19,99 zł.

**a)** Jaka kwota może pojawić się w systemie zamiast 59,97?
**b)** Zaproponuj dwa różne poprawne rozwiązania.
**c)** Jaki typ kolumny wybierzesz w bazie danych dla ceny? Podaj pełny zapis.

a) W systemie zamiast oczekiwanej wartości 59,97 zł może pojawić się kwota 59.96999999999999 (przy podwójnej precyzji double/float64) lub 59.97000122 (przy pojedynczej precyzji float/float32). Wynika to z faktu, że ułamki dziesiętne (takie jak 0,99) nie mają dokładnego rozwinięcia w binarnym systemie zmiennoprzecinkowym.
b) Dwa różne poprawne rozwiązania tego problemu to:
1. Użycie dedykowanego typu dziesiętnego (stałoprzecinkowego): W kodzie aplikacji należy użyć typu przeznaczonego do obliczeń finansowych, który operuje na bazie dziesiętnej (np. BigDecimal w Javie, Decimal w Pythonie/C#).
2. Przeliczenie kwot na jednostki całkowite (grosze): Przechowywanie i przetwarzanie cen jako liczb całkowitych (int / integer). Zamiast 19,99 zł system operuje na wartości 1999 groszy (\(1999 \times 3 = 5997\) groszy), a formatowanie na złote następuje dopiero na etapie wyświetlania danych użytkownikowi.
c) W bazie danych dla ceny należy wybrać typ DECIMAL(10, 2) (lub zamiennie NUMERIC(10, 2)).
Zapis ten oznacza, że kolumna może pomieścić maksymalnie 10 cyfr (precyzja), z czego dokładnie 2 cyfry są przeznaczone na miejsca po przecinku (skala) – co pozwala na zapisanie kwot do 99 999 999,99 zł.

---

# Lekcja 4. Typ logiczny i znakowy. Kodowanie znaków

### Ćwiczenie 4.1 – Tablica prawdy

Wypełnij:

| a | b | `a AND b` | `a OR b` | `NOT a` | `a XOR b` | `NOT (a AND b)` |
|---|---|---|---|---|---|---|
| F | F | F | F | T | F | T |
| F | T | F | T | T | T | T |
| T | F | F | T | F | T | T |
| T | T | T | T | F | F | F |

### Ćwiczenie 4.2 – Skrócone obliczanie

```java
if (lista != null && lista.size() > 0) { ... }
```

**a)** Co się stanie, gdy `lista` jest pusta (`null`)?
**b)** Co się stanie po zamianie warunków miejscami?
**c)** Zapisz analogiczny warunek z operatorem `||`.

**a)** Zadziała poprawnie.
**b)** Wystąpi błąd.
**c)** if (lista == null || lista.size() == 0)

### Ćwiczenie 4.3 – Kody znaków

Uzupełnij, korzystając z tego, że `'A'` = 65, `'a'` = 97, `'0'` = 48:

```
a)  kod znaku 'D'          = 68
b)  kod znaku 'z'          = 122
c)  znak o kodzie 74       = 'J'
d)  '7' - '0'              = -7
e)  (char)('a' - 32)       = 'A'
```

### Ćwiczenie 4.4 – Zamiana wielkości liter

Napisz w pseudokodzie funkcję, która zamienia wielką literę na małą, korzystając wyłącznie z arytmetyki na kodach znaków. Uwzględnij sprawdzenie, czy znak faktycznie jest wielką literą.

### Ćwiczenie 4.5 – ASCII a Unicode

Rozstrzygnij, czy zdanie jest prawdziwe (P) czy fałszywe (F):

```
a)  ASCII koduje znaki na 8 bitach.                 F   ASCII koduje znaki na 7 bitach.
b)  Unicode to sposób zapisu znaków w bajtach.      F   Unicode to zestaw znaków przypisujący im numery, a sposobem ich zapisu w bajtach jest kodowanie (np. UTF-8).
c)  UTF-8 jest zgodne wstecz z ASCII.               P
d)  W UTF-8 każdy znak zajmuje dokładnie 2 bajty.   F   W UTF-8 znaki zajmują zmienną liczbę bajtów (od 1 do 4 bajtów, w zależności od znaku).
e)  U+0041 to punkt kodowy litery A.                P
f)  Emoji nie da się zapisać w UTF-8.               F   Emoji da się zapisać w UTF-8 (zajmują wtedy zazwyczaj 4 bajty).
```

Popraw zdania fałszywe.

### Ćwiczenie 4.6 – Mojibake

Uczeń zapisał plik w kodowaniu Windows-1250, a otworzył go w edytorze ustawionym na UTF-8.

**a)** Jak nazywa się to zjawisko?
**b)** Czy dane w pliku zostały uszkodzone? Uzasadnij.
**c)** Wymień trzy miejsca w projekcie webowym, w których trzeba ustawić kodowanie.

**a)** To zjawisko nazywa się mojibake.
**b)** Nie, dane w pliku nie zostały uszkodzone.
**c)** Kod źródłowy plików, Nagłówek sekcji <head> w dokumencie HTML, Baza danych.

### Ćwiczenie 4.7 [K] – Bajty w praktyce

```python
for tekst in ["Ala", "Zażółć", "cześć 😀"]:
    print(tekst, len(tekst), len(tekst.encode("utf-8")))
```

Wypełnij tabelę i wyjaśnij różnice.

| Tekst | Liczba znaków | Liczba bajtów |
|---|---|---|
| `Ala` | 3 | 3 |
| `Zażółć` | 6 | 10 |
| `cześć 😀` | 7 | 12 |

---

# Lekcja 5. Typ łańcuchowy

### Ćwiczenie 5.1 – Indeksowanie

Dla napisu `s = "Programista"` podaj wynik:

```
a)  len(s)      = 11
b)  s[0]        = 'P'
c)  s[3]        = 'g'
d)  s[-1]       = 'a'
e)  s[0:6]      = 'Progra'
f)  s.find("m") = 5
```

### Ćwiczenie 5.2 – Niemutowalność

```python
tekst = "kot"
tekst[0] = "b"
```

**a)** Co się stanie po uruchomieniu tego kodu w Pythonie? 
Po uruchomieniu tego kodu w Pythonie zostanie zgłoszony błąd typu TypeError.
**b)** Zapisz poprawną wersję dającą napis `"bot"`. 
tekst = "kot"
tekst = "b" + tekst[1:]
**c)** Ile obiektów typu `str` istnieje po wykonaniu poprawnej wersji?
3

### Ćwiczenie 5.3 – Reprezentacja w pamięci

Narysuj zawartość pamięci dla napisu `"Ala"`:

**a)** w konwencji języka C (zakończenie bajtem zerowym),
Konwencja języka C (Null-terminated string)
Napis kończy się specjalnym bajtem zerowym \0 (kod ASCII 0), który oznacza koniec ciągu znaków.
Adres	Wartość w pamięci
0x01	'A'
0x02	'l'
0x03	'a'
0x04	'\0' (bajt zerowy)

**b)** w konwencji z zapisaną długością.
Konwencja z zapisaną długością (np. Pascal, Pascal-string, C++ std::string)
Na początku (w nagłówku napisu) zapisywana jest informacja o liczbie znaków (dla "Ala" długość wynosi 3), a dopiero po niej następują właściwe znaki.
Adres	Wartość w pamięci
0x01	3 (długość bufora)
0x02	'A'
0x03	'l'
0x04	'a'

Która wersja szybciej odpowiada na pytanie o długość napisu? Dlaczego?

Szybciej odpowiada wersja z zapisaną długością (b).

### Ćwiczenie 5.4 – Wydajność

```python
wynik = ""
for i in range(100000):
    wynik += str(i)
```

**a)** Dlaczego ten kod działa wolno?
Ten kod działa wolno, ponieważ napisy w Pythonie są niemutowalne.
**b)** Zapisz wersję szybszą.
wynik = "".join(str(i) for i in range(100000))
**c)** Jak nazywa się odpowiednik tego rozwiązania w Javie?
W języku Java bezpośrednim odpowiednikiem tego zoptymalizowanego mechanizmu (czyli mutowalnego bufora na tekst) jest klasa StringBuilder (lub bezpieczna wielowątkowo klasa StringBuffer).

### Ćwiczenie 5.5 – Parsowanie danych

Dany jest wiersz z pliku CSV:

```
  Kowalski;Jan;2008-05-14;klasa 2p  
```

Napisz w pseudokodzie lub w Pythonie ciąg operacji, który:
1. usunie białe znaki z początku i końca,
2. podzieli wiersz na pola,
3. wypisze samo nazwisko i rok urodzenia.
# Dane wejściowe
wiersz = "  Kowalski;Jan;2008-05-14;klasa 2p   "

# 1. Usunięcie białych znaków z początku i końca
oczyszczony_wiersz = wiersz.strip()

# 2. Podział wiersza na pola (używamy średnika jako separatora)
pola = oczyszczony_wiersz.split(";")

# 3. Wyciągnięcie nazwiska i roku urodzenia
nazwisko = pola[0]
data_urodzenia = pola[2]
rok_urodzenia = data_urodzenia.split("-")[0]  # Dzielimy "2008-05-14" po myślniku i bierzemy pierwszy element

# Wypisanie wyników
print(f"Nazwisko: {nazwisko}")
print(f"Rok urodzenia: {rok_urodzenia}")

### Ćwiczenie 5.6 – Porównywanie

Uporządkuj rosnąco według **kodów znaków** (tak jak zrobi to komputer):

```
"banan"   "Banan"   "Ananas"   "ananas"   "Żaba"   "zebra"
```

1. "Ananas" (A = 65)
2. "Banan" (B = 66)
3. "ananas" (a = 97)
4. "banan" (b = 98)
5. "zebra" (z = 122)
6. "Żaba" (Ż = 379)


Czy wynik jest zgodny z porządkiem alfabetycznym języka polskiego? Co trzeba zastosować, żeby był?

Nie, wynik nie jest zgodny z polskim porządkiem alfabetycznym z dwóch powodów:
• Wielkość liter: Komputer sortuje najpierw wszystkie wielkie litery alfabetu łacińskiego, a dopiero po nich litery małe (dlatego "Banan" trafia przed "ananas").
• Polskie znaki diakrytyczne: Litery z „ogonkami” lub kropkami (jak Ż) znajdują się w tabeli Unicode daleko poza standardowym alfabetem łacińskim, przez co trafiają na sam koniec (dlatego "Żaba" jest po "zebra").

import locale
# Ustawienie reguł sortowania dla języka polskiego
locale.setlocale(locale.LC_COLLATE, 'pl_PL.UTF-8')

slowa = ["banan", "Banan", "Ananas", "ananas", "Żaba", "zebra"]
# Sortowanie przy użyciu klucza lokalnego
slowa_posortowane = sorted(slowa, key=locale.strxfrm)

---

# Lekcja 6. Dobór typu prostego do problemu programistycznego

To zajęcia podsumowujące cały dział. Pracujemy według schematu z lekcji 2:
**czy może być ujemna → jaka jest wartość maksymalna → jaki zapas → jaki kontekst.**

### Ćwiczenie 6.1 – Formularz rejestracyjny

Projektujesz formularz rejestracji do serwisu. Dobierz typ dla każdego pola i uzasadnij wybór w jednym zdaniu.

| Pole | Typ | Uzasadnienie |
|---|---|---|
| Imię | string / str | Jest to ciąg znaków alfanumerycznych o zmiennej długości, który może zawierać narodowe diakrytyki. |
| Wiek | uint8 / byte | Wiek to zawsze dodatnia liczba całkowita, która idealnie mieści się w zakresie 1 bajta (0–255). |
| PESEL | string / str | Nie jest to liczba, lecz identyfikator tekstowy, który może zaczynać się od zera i wymaga zachowania stałej długości 11 znaków. |
| Numer telefonu | string / str | Nie jest to liczba, ponieważ nie wykonuje się na nim działań, a musi przechowywać znaki specjalne (np. +48) czy zera wiodące. |
| Adres e-mail | string / str | To identyfikator tekstowy zawierający znaki specjalne (jak @ czy .), służący wyłącznie do komunikacji. |
| Zgoda na regulamin | bool / boolean | Pole przyjmuje tylko jeden z dwóch stanów logicznych: zgoda została wyrażona (true) lub nie (false). |
| Wzrost w cm | uint8 / byte | Wzrost człowieka podawany w centymetrach to zawsze dodatnia liczba całkowita, która nie przekroczy wartości 255. |
| Waga w kg (z dokładnością do 0,1) | decimal / int (g) | Aby uniknąć błędów zaokrągleń zmiennoprzecinkowych, wagę należy zapisać typem dziesiętnym decimal lub jako całkowitą liczbę dekagramów (int). |

> **Wskazówka:** przy dwóch polach z tej listy odruchowy wybór typu liczbowego jest błędny. Zastanów się, czy na tych danych wykonuje się kiedykolwiek działania arytmetyczne.

### Ćwiczenie 6.2 – Sklep internetowy

Zaprojektuj typy dla tabeli `zamowienie`:

| Kolumna | Typ w aplikacji | Typ w bazie danych | Uzasadnienie |
|---|---|---|---|
| `id_zamowienia` | long / int64 | BIGINT PRIMARY KEY AUTO_INCREMENT | Unikalny identyfikator rośnie liniowo; typ 64-bitowy zapobiega wyczerpaniu puli identyfikatorów przy milionach transakcji. |
| `id_klienta` | long / int64 | BIGINT | Klucz obcy łączący zamówienie z użytkownikiem; musi mieć identyczny rozmiar jak klucz główny w tabeli klientów. |
| `data_zlozenia` | DateTime / datetime | DATETIME lub TIMESTAMP | Przechowuje pełną informację o momencie zakupu (rok, miesiąc, dzień, godzina, minuta i sekunda). |
| `wartosc_brutto` | decimal / Decimal | DECIMAL(10, 2) | Finanse wymagają bezwzględnej dokładności dziesiętnej; chroni przed utratą groszy wywołaną błędami zaokrągleń float/double. |
| `liczba_pozycji` | int / int32 | INT | Liczba unikalnych produktów w koszyku to zawsze dodatnia liczba całkowita, dla której standardowy zakres INT jest w zupełności wystarczający. |
| `czy_oplacone` | bool / boolean | BOOLEAN lub TINYINT(1) | Flaga przyjmująca tylko dwa logiczne stany określające status płatności: tak (true/1) lub nie (false/0). |
| `kod_rabatowy` | string / str | VARCHAR(30) | Ciąg znaków o zmiennej długości, który może być pusty (NULL), jeśli klient nie użył żadnego kuponu zniżkowego. |

### Ćwiczenie 6.3 – Znajdź błąd

W każdym przypadku wskaż błąd w doborze typu i zaproponuj poprawkę.

```
a)  float saldo_konta;                                           Błąd - float    decimal
b)  int numer_telefonu = 501234567;                              Błąd - int      string / VARCHAR(15)
c)  byte liczba_uczniow_w_szkole;                                Błąd - byte     int
d)  int identyfikator_uzytkownika;   // portal społecznościowy   Błąd - int      long (int64) / BIGINT
e)  char plec;                        // wartości 'K' lub 'M'    Błąd - char     enum
f)  int kod_pocztowy = 50137;         // dla kodu 50-137         Błąd - Typ liczbowy gubi formatowanie  string / VARCHAR(6)
```

### Ćwiczenie 6.4 – Sensor temperatury

Projektujesz oprogramowanie stacji pogodowej. Czujnik mierzy temperaturę w zakresie od −40 °C do +85 °C z dokładnością 0,1 °C, a odczyt zapisywany jest co minutę przez cały rok.

**a)** Jaki typ wybierzesz dla pojedynczego odczytu? Rozważ co najmniej dwa warianty.
1. Wariant A (float): Odruchowy wybór dla wartości z ułamkiem. Zapewnia wystarczającą dokładność, ale pojedynczy odczyt zajmuje 4 bajty (32 bity).
2. Wariant B (double): Standardowy typ zmiennoprzecinkowy w wielu językach. Nadmiarowy dla tak małego zakresu, a pojedynczy odczyt zajmuje 8 bajtów (64 bity).
**b)** Ile odczytów powstanie w ciągu roku?
W ciągu doby powstaje 1 440 odczytów (24 godziny × 60 minut). W zwykłym roku (365 dni) daje to dokładnie 525 600 odczytów.
**c)** Ile pamięci zajmą wszystkie odczyty przy każdym z rozważanych typów?
• Dla typu float (4 bajty): 525 600 × 4 bajty = 2 102 400 bajtów ≈ 2,01 MB
• Dla typu double (8 bajtów): 525 600 × 8 bajtów = 4 204 800 bajtów ≈ 4,01 MB
**d)** Zaproponuj rozwiązanie oszczędzające pamięć bez utraty dokładności.
Najbardziej efektywnym rozwiązaniem jest zastosowanie stałopozycyjnego kodowania całkowitoliczbowego (fixed-point representation) i przesunięcie skali.
Zamiast zapisywać temperaturę jako ułamek (np. 23.5), mnożymy ją przez 10 i zapisujemy jako całkowitą liczbę dziesiątych części stopnia (np. 235).
• Nasz wymagany zakres od −40°C do +85°C po pomnożeniu przez 10 zamienia się w przedział wartości całkowitych od −400 do +850.
• Przedział ten idealnie mieści się w standardowym, 16-bitowym typie całkowitym ze znakiem — int16 (lub short), którego zakres wynosi od −32 768 do 32 767.


### Ćwiczenie 6.5 – Zadanie zespołowe

W parach zaprojektujcie zestaw typów dla wybranego systemu:

- dziennik elektroniczny (oceny, frekwencja, uczniowie),
- system biblioteczny (książki, wypożyczenia, czytelnicy),
- sklep z biletami na koncerty,
- aplikacja do śledzenia treningów.

Przygotujcie tabelę z kolumnami: **nazwa danej · typ · zakres wartości · uzasadnienie**. Minimum 10 pozycji. Wynik prezentujecie klasie.

Nazwa danej	Typ (Aplikacja / DB)	Zakres wartości	Uzasadnienie
id_biletu	long / BIGINT	od 1 do 9.22 * 10^18	Unikalny identyfikator biletu. Sklepy z biletami generują miliony transakcji, dlatego 32-bitowy int mógłby się szybko wyczerpać.
nazwa_wydarzenia	string / VARCHAR(100)	do 100 znaków	Tekstowa nazwa koncertu (np. „Dawid Podsiadło – Trasa 2026”). Ograniczenie do 100 znaków optymalizuje indeksowanie i pamięć.
data_koncertu	DateTime / DATETIME	od roku 1000 do 9999	Przechowuje dokładny rok, miesiąc, dzień oraz godzinę rozpoczęcia koncertu, co pozwala na automatyczne blokowanie sprzedaży po starcie.
cena_podstawowa	decimal / DECIMAL(8, 2)	od 0.00 do 999 999.99 zł	Cena biletu brutto. Użycie typu stałopozycyjnego eliminuje błędy zaokrągleń zmiennoprzecinkowych (float), gwarantując zgodność księgową.
liczba_dostepnych_miejsc	int / INT	od 0 do 2 147 483 647	Maksymalna pojemność obiektu/stadionu. Standardowy int z zapasem obsłuży nawet największe festiwale muzyczne na świecie.
sektor	string / VARCHAR(10)	do 10 znaków	Oznaczenie strefy na stadionie lub w hali (np. „A1”, „PŁYTA_B”, „VIP”). Typ tekstowy, ponieważ sektory często łączą litery i cyfry.
rzad	uint8 / TINYINT UNSIGNED	od 0 do 255	Numer rzędu na widowni. Żadna hala koncertowa nie posiada więcej niż 255 rzędów, co pozwala na maksymalne oszczędzanie pamięci.
numer_miejsca	uint16 / SMALLINT UNSIGNED	od 0 do 65 535	Numer konkretnego krzesła w rzędzie. Może przekroczyć 255 na wielkich trybunach stadionu, stąd bezpieczny dobór typu 2-bajtowego.
kod_kreskowy_bilet	string / CHAR(13)	Dokładnie 13 znaków	Unikalny ciąg cyfr standardu EAN-13 generowany na bilet. Typ CHAR jest szybszy niż VARCHAR, gdy dane mają zawsze stałą długość.
czy_imienny	bool / BOOLEAN	true (1) lub false (0)	Flaga logiczna określająca, czy bilet wymaga podania danych osobowych uczestnika podczas weryfikacji przy wejściu na teren imprezy.
procent_znizki	uint8 / TINYINT UNSIGNED	od 0 do 100	Wartość rabatu dla biletów ulgowych lub akcji promocyjnych wyrażona w procentach. Zakres 1 bajta idealnie pokrywa skalę od 0% do 100%.

---

## Materiały uzupełniające

- Prezentacja do działu: `02-typy-danych.pdf`
- Tablica kodów ASCII – dowolne wydanie podręcznikowe
- Konsola Pythona do sprawdzania przykładów na bieżąco
