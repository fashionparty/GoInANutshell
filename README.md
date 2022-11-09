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


