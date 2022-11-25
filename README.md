# Go in a nutshell

![gns](https://user-images.githubusercontent.com/51796385/200906219-d6aa73b9-1749-4b56-a624-6c9e1bde918e.jpg)





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

