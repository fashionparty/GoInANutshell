# Go in a nutshell

![gns](https://user-images.githubusercontent.com/51796385/200906219-d6aa73b9-1749-4b56-a624-6c9e1bde918e.jpg)

- [1. Konfiguracja środowiska](https://github.com/fashionparty/GoInANutshell/blob/main/1.md)
- [2. Typy podstawowe i deklaracje](https://github.com/fashionparty/GoInANutshell/blob/main/2.md)
- [3. Tablice i Wycinki](https://github.com/fashionparty/GoInANutshell/blob/main/3.md)
- [4. Łańcuchy, runy i bajty](https://github.com/fashionparty/GoInANutshell/blob/main/4.md)
- [5. Mapy](https://github.com/fashionparty/GoInANutshell/blob/main/5.md)
- [6. Struktury](https://github.com/fashionparty/GoInANutshell/blob/main/6.md)
- [7. Blok globalny](https://github.com/fashionparty/GoInANutshell/blob/main/7.md)
- [8. Specyficzna instrukcja if](https://github.com/fashionparty/GoInANutshell/blob/main/8.md)
- [9. Pętle for](https://github.com/fashionparty/GoInANutshell/blob/main/9.md)
- [10. Instrukcja switch](https://github.com/fashionparty/GoInANutshell/blob/main/10.md)
- [11. Instrukcja goto](https://github.com/fashionparty/GoInANutshell/blob/main/11.md)
- [12. Funkcje](https://github.com/fashionparty/GoInANutshell/blob/main/12.md)
- [13. Defer](https://github.com/fashionparty/GoInANutshell/blob/main/13.md)
- [14. Wskaźniki](https://github.com/fashionparty/GoInANutshell/blob/main/14.md)
- [15. Metody](https://github.com/fashionparty/GoInANutshell/blob/main/15.md)
- [16. Interfejsy](https://github.com/fashionparty/GoInANutshell/blob/main/16.md)
- [17. Obsługa błędów](https://github.com/fashionparty/GoInANutshell/blob/main/17.md)


## Podstawy

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

## Wskaźniki


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
  Street string
}

type Employee struct {
  Adress: Adress
}

func main() {
  var emp Employee
  emp.Adress.Street = "Bagienna"
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
  emp.Street = "Bagienna"
}
```

Jeśli wystąpią dwie zagnieżdżone struktury anonimowe o takich samych polach to będziesz musiał używać pełnych wywołań.

