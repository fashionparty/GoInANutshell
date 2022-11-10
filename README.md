# Go in a nutshell

![gns](https://user-images.githubusercontent.com/51796385/200906219-d6aa73b9-1749-4b56-a624-6c9e1bde918e.jpg)





## Podstawy

- Punktem startowym każdego programu Go jest funkcja `main`:
```
func main() {

}
```
- każdy plik w Go rozpoczyna się od klauzuli `package`. Pakiet to zbiór kodu przeznaczonego do podobnych zadań.
- Go nie używa średników ( są one opcjonalne )
- Go posiada wbudowane polecenie `go fmt`, które automatycznie formatuje napisany kod według ustalnego standardu
- Go **nie pozwoli** na skompilowanie kodu, w którym jest importowany nieużywany pakiet. Przed kompilacją trzeba koniecznie usunąć nieużywane importy.
- Go nie pozwoli również na kompilację, jeżeli w kodzie są nieużywane zmienne
- możemy importować wiele pakietów z użyciem pojedynczej instrukcji import:
```
import (
  "math
  "strings"
)
```
- sekwencje ucieczki:
`\n` - nowy wiersz
`\t` - tabulator
`\"` - cudzysłów
`\\` - lewy ukośnik
 - podstawowe typy w Go to: `int`, `float`, `string`, `bool`, `rune` ( rune == char z innych języków )
 - wydrukowanie runy zwróci jej Unicode
 - deklarowanie zmiennych w Go:
 
 W jednej instrukcji:
 ```
 var myName string = "Maykie"
 ```
 Przypisanie w osobnej instrukcji:
 ```
 var myName string
 myName = "Maykie"
 ```
 Przypisanie wielu zmiennych na raz:
 ```
 var name, class string = "Maykie", "Sorcerer"
 ```
 - istnieje krótka deklaracja pozwalająca ominąć słowo `var` i typ zmiennej. Jest to zalecany sposób deklaracji zmiennych.
 ```
 name := "Maykie"
 ```
 - zmienne, którym nie przypiszesz żadnej wartości otrzymają automatycznie wartości zerowe, są to `0` dla typów liczbowych, pusty łańcuch `""` dla stringów i `false` dla booleana
 - zmienne, funkcje i typy, których nazwy rozpoczynają się wielką literą, są eksportowane i stają się dostępne w pakietach innych niż bieżący, np. `fmt.Println`. Jest to reguła wymuszona przez sam język.
 - nie można wykonywać operacji matematycznych i porównań na różnych typach liczbowych, trzeba je najpierw skonwertować:
 ```
 var myInt int = 2
 fmt.Println(reflect.TypeOf(myInt))
 // int

 var myFloat = float64(myInt)
 fmt.Println(reflect.TypeOf(myFloat))
 // float64
  ```
 - parsowanie stringa na liczbę: 
 ```
 zczytanaLiczba, err = strconv.ParseFloat(input, 64)
 ```
 - konwersja `float` na `int` ucina część ułamkową bez zaokrąglania
 - czytanie z terminala w Go:
 ```
fmt.Print("Podaj imię: ")
reader := bufio.NewReader(os.Stdin)
input, err := reader.ReadString('\n')
fmt.Println(input)
fmt.Println(err)
```
- w odróżnieniu od innych języków, funkcje w Go mogą zwracać wiele wartości
- jeżeli nie chcemy korzystać ze zwracanej zmiennej możemy ją zastąpić pustym identyfikatorem - `_`:
```
input, _ := reader.ReaderString('\n')
```
- UWAGA - w go można nadpisać WSZYSTKO używając tej samej nazwy:
```
var int int = 12
```
- w Go nie można deklarować zmiennej dwa razy CHYBA, że deklaracja następuje przy wielu zmiennych na raz:
```
a := 1
a := 2
// błąd

a := 1
a, err = strconv.ParseFloat("1.23", 64)
// ok
```
## Uruchamianie kodu

1. Sprawdź czy Go jest zainstalowane przez `go version`
2. (opcjonalnie) Sformatuj kod przez `go fmt nazwaPliku.go`
3. Skompiluj kod przez `go build nazwaPliku.go`
4. Odpal .exe przez `nazwaPliku.exe`

Można też szybciej uruchomić program bez zapisywania pliku wykonywalnego przez `go run nazwaPliku.go`

## Instrukcje warunkowe i pętle

If:

```
if 12 == 12 && 5.0 >= 5.0 {
//todo
} else if 12==12 || 5.9 ==6.4 {
//todo
} else { 
//todo
}
```

For:
```
for i := 1; i<10; i++ {}
```

For inaczej:
```
x := 1
for x<10 {
x++
}
```

For nieskończony:
```
for i := 1; true, i++ {}
```

## Formatowanie stringów

Do formatowania tekstu służy `fmt.Printf` lub `fmt.Sprintf` jeżel chcemy zwrócić formatowany tekst:
```
fmt.Printf("Cena %s to %d grosze za sztuke.\n", "gumy do żucia", 23)
```
Instrukcje formatowania:
- `%f` - liczba zmiennoprzecinkowa
- `%d` - liczba całkowita
- `%s` - łańcuch znaków
- `%t` - watość logiczna
- `%v` - dowolna wartość dobrana na podstawie typu wartości
- `%#v` - dowolna wartość sformatowana w Go ( wyświetli np. "\n", instrukcja `%v` nie wyświetliła by nic )
- `T` - typ podanej wartości
- `%%` - znak procenta

Dodatkowe opcje:
```
fmt.Printf("%12s | %2d\n", "Liczba:", 50)
// Liczba: | 50

fmt.Printf(%.2f\n, 1.2600000000000002
// 1.26
```

## Funkcje

Funkcja przyjmująca dwa floaty i zwracająca jeden float oraz obiekt error
```
func mojaFunkcja(arg1 float64, arg2 float64) (float64, error) {
  
}
```

## Wskaźniki
Do pobrania adresu zmiennej używamy `&`
Typ wskaźnikowy to typ zmiennej wskazywanej prezez wskaźnik, np. `*int`

```
val myIntPointer = *int
myIntPointer = &myInt
```

Można również wykorzystać skrócony zapis:
```
myFloatPointer := &myFloat
```

Pobieranie wartości ze wskaźnika:
```
myInt := 4
myIntPointer := &myFloat

fmt.Println(myIntPonter)
// 0x1040a124

fmt.Println(&myIntPointer)
// 4
```

Modyfikowanie zmiennej znajdującej się po za funkcją za pomocą wskaźnika:
```
func main() {
  amount := 6
  double(&amount)
}

func addTwo(number *int) {
  *number += 2
}
```

## Pakiety i struktura projektu

```
- Nazwa Projektu
  - main.go
  - mod.go
  - pakiet1
    -plik.go
  -pakiet2
    -plik.go
```

Plik `mod.go` tworzymy przez polecenie `go mod init NazwaProjektu`

Struktura pliku `mod.go`:
```
module $NazwaModulu

go $versia

require {
  // zależności
}
```

- nazwy pakietów powinny być pisane małymi literami, powinny być skrótami, jeżeli składa się z więcej niż jednego słowa to NIE używamy camelcase'a
- nazwy funkcji i zmiennych eksportowanych (publicznych) są pisane wielką literą. Jest to mechanizm samego języka

## Stałe

Deklaracja:
```
const Stala int = 3
```

W stałych można pominąć typ ale nie można używać zapisu `:=`:
```
const Stala = 3
```

## Tablice

Inicjalizacja:
```
var notes [7]string
notes[0] = "a"
notes[1] = "b"
notes[2] = "c"
fmt.Println(notes[0])
```
Inicjalizacja literałem tablicowym:
```
notes := [3]int{"a","b","c"}
```
Uwaga - tablice są inicjalizowane wartościami zerowymi !

Jeżeli dodajemy elementy w ososbnych wierszach to w ostatnim wierszu MUSIMY postawić przecinek, nawet jeśli nie występuje po nim kolejny element:
```
notes := {
  "a",
  "b",
  "c",
}
```

Możemy użyć biblioteki `fmt` to sprawdzenia sygnatury tablicy: 
```
fmt.Printf("%#v\n", mojaTablica)
// [3]int{2,3,4}
```

Sprawdzanie wielkości tablicy: `len(mojaTablica)`

Przeglądanie tablicy za pomocą pętli for:
```
for i := 0 <= len(notes); i++ {
  fmt.Println(i, notes[i])
}
```

Bezpieczne tworzenie tablicy za pomocą for range:
```
for index, value := range mojaTablica {
  fmt.Println(index, value)
}
```

To samo z pominięciem zwracania indeksu:
```
for _, value := range mojaTablica {
  fmt.Println(value)
}
```
