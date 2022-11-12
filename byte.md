## Определение

**`byte`** - это тип данных, псевдоним для `uint8`.
- имеет ограничение от 0 до 255 в числовом диапазоне, так же как и `uint8`
- тип данных `byte` используется только для семантического различия между `uint8` и `byte`
- `byte` может представлять только символ ASCII, то есть 1 байт

## Объявление

При объявление `byte` можно использовать прямые кавычки `''` или числовое значение от `0 - 255` и явно указать тип данных `byte`. 
Нулевым значением для `byte` является `0`(uint8):

```go
var i byte = 's'
var j byte
var k byte = 120
var l = 120 // int

fmt.Println(i) // 115
fmt.Println(j) // 0
fmt.Println(k) // 120
fmt.Println(l) // 120

fmt.Printf("Size: %d\n", unsafe.Sizeof(i)) // Size: 1
fmt.Printf("Size: %d\n", unsafe.Sizeof(j)) // Size: 1
fmt.Printf("Size: %d\n", unsafe.Sizeof(k)) // Size: 1
fmt.Printf("Size: %d\n", unsafe.Sizeof(l)) // Size: 8 (int зависит от процессора, в моем случае int64, поэтому 8)

fmt.Printf("Type: %s\n", reflect.TypeOf(i)) // Type: uint8
fmt.Printf("Type: %s\n", reflect.TypeOf(j)) // Type: uint8
fmt.Printf("Type: %s\n", reflect.TypeOf(k)) // Type: uint8
fmt.Printf("Type: %s\n", reflect.TypeOf(l)) // Type: int

fmt.Printf("Character: %c\n", i) //  Character: s
fmt.Printf("Character: %c\n", j) //  Character:
fmt.Printf("Character: %c\n", k) //  Character: x
fmt.Printf("Character: %c\n", l) //  Character: x
// `byte` - это всего лишь семантическое разделение(псевдоним `uint8`), поэтому строка выше не должна вызывать вопросов
```

Как было сказанно выше `byte` подходит только для работы с символами ASCII. Поэтому задать многобайтовый символ типу данных `byte` просто невозможно:

```go
var i byte = 'л' // вызовет ошибку, 'л' - не входит в ASCII(0-255), надо использовать тип `rune`
```

Если при объявлении опустить указание типа `byte`, то по умолчанию присвоится тип `rune`:

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
