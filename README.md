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

## Wycinki

Deklaracja:
```
var mojWycinek [] string
```

Deklaracja zwykłej tablicy zawsze tworzy tablicę zainicjalizowaną wartościami zerowymi lub tymi, które podasz. Wycinek w przeciwieństwie do tablicy nie jest od razu inicjalizowany.

Inicjalizacja wycinków:
```
var mojWycinek := make([]int, 5)
```

Wycinki również można inicjalizować literałem:
```
notes := []string{"a", "b", "c"}
```

Operator wycinka:
```
var tablica = [5]string{"a", "b", "c", "d", "e"}
wycinek := tablica[1:3] // można pominąć liczby wewnątrz nawiasu kwadratowego żeby czytać od/do końca tablicy
fmt.Println(wycinek)
// [b, c]
```

Dodawnie elementów:
```
s1 := []string{"a", "b"}
s1 = append(s1, "c")
fmt.Println(s1)
// [a b c]
```

UWAGA - zmiana elementu w tablicy będzie dotyczyła wycinków z niej utworzonych!!

UWAGA2 - zawsze kiedy tworzysz wycinek pod spodem jest tworzona tablica bazowa. Kilka wycinków może korzystać z tej samej tablicy bazowej. Trzeba tego zawsze pilnować bo pracowanie z wycinkami może być zagmatwane:
```
s1 := []string{"a", "b"}
s2 := append(s1, "c", "d")
s3 := append(s2, "e", "f")
s4 := append(s3, "g", "h")

fmt.Println(s1, s2, s3, s4)
// [a b] [a b c d] [a b c d e f] [a b c d e f g h]
s4[0] = "X"
fmt.Println(s1, s2, s3, s4)
// [a b] [a b c d] [X b c d e f] [X b c d e f g h]
```

Niezainicjalizowane wycinki mają wartość `nil`. Nie są jednak niebezpieczne, ponieważ mechanizm języka będzie je traktował jako puste zbiory - możemy na nich wywoływać metody `len` czy `append`.

## Funkcje wariadyczne

Deklaracja:
```
func mojaFunkcja(arg1 int, arg2 ... string) {
  // arg2 jest wycinkiem
}
```

Tylko ostatni argument może być wariadyczny.
Argumentu wariadycznego nie trzeba podawać - w samej funkcji stanie się on pustym wycinkiem.

Do funkcji wariadycznej możne przekazać wycinek zamiast grupy argumentów ale w takim wypadku trzeba użyć wielokropka:
```
mojWycinek := []{1,2,3}
mojaFunkcjaWariadycza(mojWycinek...)
```

## Mapy

Deklaracja:
```
var mojaMapa map[string]float64
// utworzenie zmiennej mapy o kluczu string i wartości float64

mojaMapa := make(map[string]int)
// utworzenie samej mapy
```

Krótka deklaracja:
```
mojaMapa := make(map[string]int)
```

Usuwanie elementów:
```
delete(mojaMapa, "klucz")
```

Na mapach operujemy tak jak na tablicach i wycinkach. Róznica polega na tym, że w tablicach i wycinkach indeksami mogą być tylko liczby całkowite.

Deklarowanie literałem:
```
mojaMapa := map[string]flaot64 {"a": 1.2, "b": 5.6}
```

For range w przypadku map przegląda mapę za każdym razem w INNEJ kolejności:
```
for key, value := range mojaMapa{}
```
Jeżeli chcemy posortowaną mapę to najlepiej zapisać ją w wycinku i osobno posortowac.

## "Idiom przecinek Go"

Często trudno jest stwierdzić czy wartość zerowa danej tablicy/wycinka/mapy została utworzona automatycznie, czy może zapisano element, który jest równy wartości zerowej. Istnieje technika żeby to sprawdzić:
```
mojaMapa := map[string]int{"a": 3, "b": 0}
var value int
var ok bool

value, ok = counters["b"]
fmt.Println(value, ok)
// 3 true

value, ok = counter["c"]
fmt.Println(value, ok)
// 0 false
```

## Struktury

Struktura to zestaw pól różnych typów, przypomina klasę z OOP ale jest od niej dużo prostsza. Strukturę możemy stworzyć literałem ale w ten sposób tworzymy coś na wzór singletona bo jest ona przypisana tylko do konkretnej zmiennej. Aby stworzyć szablon `ala klasa należy użyć typu zdefiniowanego.

Deklaracja:
```
val mojaStruktura struct {
  pole1 string
  pole2 int
}

mojaStruktura.pole1 = "a"
mojaStruktura.pole2 = 3
```

Literał struktur:
```
myCar := {name: "Bitroen Cerlingo", topSpeed: 45)
// pominięte pola uzyskają wartość zerową
```
## Typy zdefiniowane

Szablon do tworzenia struktur. Należy je definiować w ciele pakietu.

Deklaracja:
```
type mojTyp struct {
  pole1 string
  pole2 int
}

var mojaZmienna mojTyp
mojaZmienna.pole1 = "a"
mojaZmienna.pole2 = 3
```

Nie można ustawić domyślnych wartości w strukturze. Domyślnych kontruktor należy stworzyć w postaci funkcji zwracajacej domyślną strukturę.
Settery uzyskujemy przez pisanie własnych funkcji ze wskaźnikami:
```
func applyDiscount(s *subscriber) {
// subscriber.price = (...)
}

func main() {
  var s subscriber
  subscriber1 := defaultSubscriber
  applyDiscount(&subscriber1)
}
```

## Struktury zagnieżdżone

```
type Address struct {
  street string
}

type Employee struct {
  Adress: Adress
}

func main() {
  var emp Employee
  emp.Adress.street = "Bagienna"
}
```

Można pomijać nazwę zagnieżdżonej struktury jeśli będzie anonimowa:
```
type Employee struct {
type Address struct {
  Street string
}

type Employee struct {
  Adress
}

func main() {
  var emp Employee
  emp.street = "Bagienna"
}
```

Jeśli wystąpią dwie zagnieżdżone struktury anonimowe o takich samych polach to będziesz musiał używać pełnych wywołań.

