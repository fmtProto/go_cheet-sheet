## Определение

**`byte`** - это тип данных, псевдоним `uint8`, используются для того, чтобы отличить `byte` от реальных 8-битных целых чисел без знака`(uint8)`.  
В Go используется `byte` или `rune` для представления значений символов, потому что нет типа данных `char`. 

- `byte` имеет ограничение от 0 до 255 в числовом диапазоне, так же как и `uint8`
- тип данных `byte` используется для различия между `uint8` и `byte`
- `byte` создан для представления символов `ASCII`(символ `ASCII` как раз занимает в памяти 1 байт)

## Объявление
Инициализировать байтовую переменную можно:
- **путем назначения десятичного целого числа от 0 до 255**
```go
var a byte = 90
fmt.Println(a)                            // 90
fmt.Printf("Size: %d", unsafe.Sizeof(a))  // Size: 1
fmt.Printf("Type: %s", reflect.TypeOf(a)) // Type: uint8
fmt.Printf("Character: %c", a)            // Character: Z
```
- **путем назначения `ASCII` символа, указывая его в одинарных кавычках `''`**
```go
var a byte = 'Z'
fmt.Println(a)                            // 90
fmt.Printf("Size: %d", unsafe.Sizeof(a))  // Size: 1
fmt.Printf("Type: %s", reflect.TypeOf(a)) // Type: uint8
fmt.Printf("Character: %c", a)            // Character: Z
```
- **путем назначения целых чисел в отличной от 10-ой системах счисления(2-ая, 8-ая, 16-ая)**
```go
var a byte = 0b01011010 // Binary
var b byte = 0o132      // Octal
var c byte = 0x5a       // Hex

fmt.Println(a, b, c)                       // 90 90 90
fmt.Printf("Character: %c,%c,%c", a, b, c) // Character: Z,Z,Z
```
  
Требуется явно указывать тип данных `byte`, иначе по умолчанию присвоится тип `rune`:
```go
var i  = 's' // тип данных `rune`
fmt.Println(i)                               // 115 
fmt.Printf("Size: %d\n", unsafe.Sizeof(i))   // Size: 4
fmt.Printf("Type: %s\n", reflect.TypeOf(i))  // Type: int32
fmt.Printf("Character: %c\n", i)             // Character: s

var j = 'л' // тип данных `rune`
fmt.Println(j)                               // 1083
fmt.Printf("Size: %d\n", unsafe.Sizeof(j))   // Size: 4
fmt.Printf("Type: %s\n", reflect.TypeOf(j))  // Type: int32
fmt.Printf("Character: %c\n", j)             // Character: л

var l = 120 // явно не указан тип byte, поэтому по умолчанию это int
fmt.Println(l) // 120
fmt.Printf("Size: %d\n", unsafe.Sizeof(l))  // Size: 8 (int зависит от процессора, в моем случае int64, поэтому 8)
fmt.Printf("Type: %s\n", reflect.TypeOf(l)) // Type: int
fmt.Printf("Character: %c\n", l)            // Character: x
// %c представляет кодовую точку Unicode, соответствующую значению 120 типа int
```

Нулевым значением для `byte` является `0`(uint8)
```go
var j byte
fmt.Println(j) // 0
fmt.Printf("Size: %d\n", unsafe.Sizeof(j))  // Size: 1
fmt.Printf("Type: %s\n", reflect.TypeOf(j)) // Type: uint8
fmt.Printf("Character: %c\n", j)            // Character:
```

Как было сказанно выше, `byte` подходит только для работы с символами `ASCII`. Поэтому задать многобайтовый символ типу данных `byte` просто невозможно:
```go
var i byte = 'л' // вызовет ошибку, 'л' - не входит в ASCII(0-255), надо использовать тип `rune`
```
## Конвертация
### string -> []byte
```go
fmt.Println([]byte("hello"))   // [104 101 108 108 111] по 1 байту на символ
fmt.Println([]byte("привет")) //  [208 191 209 128 208 184 208 178 208 181 209 130]  по 2 байта на символ
```
### []byte -> string
```go
i := []byte{104, 101, 108, 108, 111}
j := []byte{208, 191, 209, 128, 208, 184, 208, 178, 208, 181, 209, 130}

fmt.Println(string(i)) // hello
fmt.Println(string(j)) // привет
```
