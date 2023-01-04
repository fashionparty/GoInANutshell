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
- [18. Moduły, pakiety, importy](https://github.com/fashionparty/GoInANutshell/blob/main/18.md)
- [19. Gorutyny](https://github.com/fashionparty/GoInANutshell/blob/main/19.md)
- [20. Testowanie](https://github.com/fashionparty/GoInANutshell/blob/main/20.md)
- [21. Programowanie sieciowe](https://github.com/fashionparty/GoInANutshell/blob/main/21.md)
- [22. Funkcje pierwszoklasowe](https://github.com/fashionparty/GoInANutshell/blob/main/22.md) 





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

