# Testy jednostkowe w C++ – Microsoft Native Unit Test

Materiały dydaktyczne dotyczące testów jednostkowych w języku C++ z wykorzystaniem frameworka **Microsoft Native Unit Test** dostępnego w środowisku **Visual Studio**.

## Zakres materiału

Repozytorium obejmuje:

- wprowadzenie do testów jednostkowych,
- zasady tworzenia testowalnego kodu,
- wykorzystanie frameworka Microsoft Native Unit Test,
- przykładowe testy jednostkowe w C++,
- organizację projektu testowego,
- wzorzec AAA (Arrange – Act – Assert),
- wykorzystanie asercji.

---

# Czym są testy jednostkowe?

Test jednostkowy to test sprawdzający pojedynczy element aplikacji, najczęściej:

- funkcję,
- metodę,
- klasę.

Test wykonywany jest w izolacji od pozostałych elementów systemu w celu zweryfikowania poprawności działania kodu.

## Zalety testów jednostkowych

- szybsze wykrywanie błędów,
- większa stabilność projektu,
- łatwiejsza refaktoryzacja,
- poprawa jakości kodu,
- możliwość automatycznego testowania.

---

# Cechy dobrych testów – zasada FIRST

- **F (Fast)** - Testy powinny działać szybko
- **I (Independent)** - Testy powinny być niezależne od siebie
- **R (Repeatable)** - Testy powinny zawsze zwracać ten sam wynik
- **S (Self)** - Test powinien sam określać wynik PASS lub FAIL
- **T (Timely)** - Testy powinny być tworzone możliwie wcześnie

---

# Struktura testu – AAA

- **Arrang**e - Przygotowanie danych oraz obiektów potrzebnych do testu.
- **Act** - Uruchomienie testowanej funkcjonalności.
- **Assert** - Sprawdzenie, czy wynik jest zgodny z oczekiwaniem.

---

# Tworzenie testowalnego kodu

Kod testowalny powinien być:

- łatwy do izolowania,
- niezależny od środowiska,
- deterministyczny,
- prosty do automatycznego uruchamiania.

## Jak przygotować kod do testów jednostkowych

W przypadku środowiska **Microsoft Native Unit Test Framework** kluczową zasadą jest przygotowanie kodu tak, aby był **modułowy** -  zależności muszą być odseparowane.

**Zasady**:

- oddziela się logikę od wartstwy prezentacji
- używa się wstrzykiwania zależności
- unika się zmiennych globalnych i singletonów
- umieszcza się deklaracje w plikach nagłówkowych (np. Calculator.h, Calculator.cpp)
- tworzy się klasy o jednej odpowiedzialności

**Plik nagłówkowy i plik źródłowy**

W pliku nagłówkowym (.h) powinny znajdować się deklaracje elementów, które mają być dostępne w innych plikach programu. Nagłówek opisuje interfejs modułu, natomiast implementacja znajduje się zwykle w pliku źródłowym (.cpp).

Typowa zawartość pliku nagłówkowego:

- strażnik nagłówka (#pragama once)
- deklaracje pól składowych (atrybutów, właściwości)
- deklaracje pól statycznych (inicjalizacja w pliku źródłowym)
- deklaracje klas
- deklaracje funkcji
- definicje struktur i typów
- szablony (templates)
- stałe i definicje potrzebne innym plikom

W pliku nagłówkowym nie umieszcza się dyrektywy **using namespace std**, ponieważ ma to wpływ na wszystkie pliki dołączające ten nagłówek. Należy również mieć na uwadze, że zasadniczo w testach jednostkowych **nie testuje się pliku zawierającego main(), lecz klasy, funkcje i moduły biznesowe**.

## Przykład przygotowania kodu do testów jednostkowych

**Calculator.h**

```cpp
    #pragma once
    
    class Calculator
    {
    public:
        int Add(int a, int b);
    };
```

**Calculator.cpp**

```cpp
    #include "Calculator.h"
    
    int Calculator::Add(int a, int b)
    {
        return a + b;
    }
```

**Dołączenie pliku nagłówkowego do projektu testów jednostkwoych**

```cpp
    #include "../Application/Calculator.h"
```

## Film - test bez biblioteki statycznej
[![Test bez biblioteki statycznej](https://img.youtube.com/vi/OZQhOUneeGc/0.jpg)](https://www.youtube.com/watch?v=OZQhOUneeGc)

## Film - test z biblioteką statyczną
[![Test bez biblioteki statycznej](https://img.youtube.com/vi/r3X0AK7TjIA/0.jpg)](https://www.youtube.com/watch?v=r3X0AK7TjIA)

## Dobre praktyki

### Jedna odpowiedzialność
Klasa lub metoda powinna odpowiadać za jeden problem.

### Funkcje deterministyczne
Dla tych samych danych wejściowych funkcja zawsze zwraca ten sam wynik.

### Czyste funkcje
Czyste funkcje:
- nie mają skutków ubocznych,
- nie zależą od środowiska,
- są łatwe do testowania.

### Izolacja
Kod powinien umożliwiać testowanie bez uruchamiania całej aplikacji.

---

# Microsoft Native Unit Test

Microsoft Native Unit Test to framework do testów jednostkowych dla języka C++ dostępny w środowisku Visual Studio.

## Najważniejsze cechy

- integracja z Visual Studio,
- obsługa Test Explorer,
- natywna obsługa C++,
- wbudowany system asercji.

---

# Najczęściej używane asercje

| Metoda | Opis |
|---|---|
| `Assert::AreEqual()` | porównanie wartości |
| `Assert::AreNotEqual()` | sprawdzenie różnicy |
| `Assert::IsTrue()` | sprawdzenie warunku logicznego |
| `Assert::IsFalse()` | sprawdzenie negacji warunku |
| `Assert::IsNull()` | sprawdzenie wartości nullptr |
| `Assert::IsNotNull()` | sprawdzenie istnienia obiektu |
| `Assert::Fail()` | wymuszenie błędu testu |

---

# Przykład testu jednostkowego

## Funkcja produkcyjna

```cpp
    int Add(int a, int b)
    {
        return a + b;
    }
```

## Test jednostkowy

```cpp
    TEST_CLASS(AddTests)
    {
    public:
    
        TEST_METHOD(Add_ReturnsCorrectResult)
        {
            // Arrange
            int a = 2;
            int b = 3;
    
            // Act
            int result = Add(a, b);
    
            // Assert
            Assert::AreEqual(5, result);
        }
    };
```

---

# Struktura projektu

Przykładowa organizacja projektu:

```text
/Project
│
├── Add.h
├── Add.cpp
│
└── Tests
    └── AddTests.cpp
```

---

# Uruchamianie testów

1. Otwórz projekt w Visual Studio.
2. Zbuduj rozwiązanie.
3. Otwórz:
   - `Test > Test Explorer`
4. Uruchom:
   - `Run All Tests`

---

# Wymagania

- Visual Studio 2022
- Desktop development with C++
- Microsoft Native Unit Test Framework

---

# Licencja

Materiały dydaktyczne do użytku edukacyjnego.
