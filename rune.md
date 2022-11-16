## Определение

**`rune`** - это тип данных, псевдоним для `int32`, представляет кодовую точку `Unicode`.

- имеет ограничение от -2_147_483_648 до 2_147_483_647 в числовом диапазоне, так же как и `int32`
- тип данных `rune` используется для различия между `int32` и `rune`
- `rune` создан представлять символы `Unicode`, то есть до 4 байт(точка `Unicode` может иметь максимальную длину 4 байта )

## Объявление

Переменную типа `rune` часто инициализируют:
- **путем назначения `Unicode` символа, указывая его в одинарных кавычках `''`**
```go
var a rune = 'л'
fmt.Println(a)                            // 1083
fmt.Printf("Size: %d", unsafe.Sizeof(a))  // Size: 4
fmt.Printf("Type: %s", reflect.TypeOf(a)) // Type: int32
fmt.Printf("Character: %c", a)            // Character: л
fmt.Printf("Unicode CodePoint: %U", a)    // Unicode CodePoint: U+043B
```

- **путем назначения десятичного целого числа в диапазоне `int32`**
```go
var a rune = 1083
fmt.Println(a)                            // 1083
fmt.Printf("Size: %d", unsafe.Sizeof(a))  // Size: 4
fmt.Printf("Type: %s", reflect.TypeOf(a)) // Type: int32
fmt.Printf("Character: %c", a)            // Character: л
fmt.Printf("Unicode CodePoint: %U", a)    // Unicode CodePoint: U+043B
```

При объявление перменной типа `rune` указание типа является необязательным(в отличие от типа `byte`). 
```go
var a = 'л' // тип rune
b := 'и'    // тип rune
```

Нулевым значением для rune является `0` (int32):
```go
var a rune
fmt.Println(a)                            // 0
fmt.Printf("Size: %d", unsafe.Sizeof(a))  // Size: 4
fmt.Printf("Type: %s", reflect.TypeOf(a)) // Type: int32
fmt.Printf("Character: %c", a)            // Character:
fmt.Printf("Unicode CodePoint: %U", a)    // Unicode CodePoint: U+0000
```

Как было сказанно выше, `rune` создана для работы с символами `Unicode`. Поэтому задать многобайтовый символ типу данных `rune` очень просто(в отличие от `byte` которому это сделать невозможно):
```go
k := '\U0001F3A8'
l := '£'

fmt.Println(k) // 127912 значение кодовой точки в десятичном формате
fmt.Println(l) // 163 значение кодовой точки в десятичном формате

fmt.Printf("Size: %d\n", unsafe.Sizeof(k)) // Size: 4
fmt.Printf("Size: %d\n", unsafe.Sizeof(l)) // Size: 4

fmt.Printf("Type: %s\n", reflect.TypeOf(k)) // Type: int32
fmt.Printf("Type: %s\n", reflect.TypeOf(l)) // Type: int32


fmt.Printf("Character: %c\n", k) //  Character: 🎨
fmt.Printf("Character: %c\n", l) //  Character: £

fmt.Printf("Unicode CodePoint: %U\n", k) // Unicode CodePoint: U+1F3A8
fmt.Printf("Unicode CodePoint: %U\n", l) // Unicode CodePoint: U+00A3
```

## Цикл for range

В Go присутствует синтаксический сахар при обходе строки. 
Если использовать конструкцию `for range`, строка автоматически будет преобразована в `[]rune`, то есть обход будет по `Unicode` символам:
```go
k := "привет😀"

for _, v := range k {
    fmt.Println(string(v))
}
// п
// р
// и
// в
// е
// т
// 😀
```

## Конвертация

### string -> []rune
```go
i := "hello"
j := "привет"

fmt.Println([]rune(i)) // [104 101 108 108 111] кодовые точки в десятичном формате
fmt.Println([]rune(j)) // [1087 1088 1080 1074 1077 1090] кодовые точки в десятичном формате

fmt.Printf("%U\n", []rune(i)) // [U+0068 U+0065 U+006C U+006C U+006F]
fmt.Printf("%U\n", []rune(j)) // [U+043F U+0440 U+0438 U+0432 U+0435 U+0442]
```
### []rune -> string
```go
i := []rune{104, 101, 108, 108, 111}
j := []rune{'\u043F', '\u0440', '\u0438', '\u0432', '\u0435', '\u0442'}
l := []rune{'п', 'о', 'к', 'а'}

fmt.Println(string(i)) // hello
fmt.Println(string(j)) // привет
fmt.Println(string(l)) // пока
```
