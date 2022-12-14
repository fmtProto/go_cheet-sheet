## `Switch`

`switch` - это условный оператор, с помощью которого удобно показывать действия программы в ситуациях с разными возможными вариантами. Все, что можно написать с помощью оператора `switch`, можно написать и с помощью оператора `if/else`.  

Оператор `switch` начинается с ключевого слова `switch`, за которым идет переменная, для которой производится сравнение. Далее идет пара фигурных скобок `{}`, в которых идет перечесление возможных вариантов. Каждый такой вариант начинается с ключевого слова `case`, за которым сразу следует сравниваемое значение, через двоеточие указывается действие, которое следует произвести при равентсве данного значения со сравниваемой переменной. `default` - выполнится если ни один из вариантов не подходит, является необязательным.

Пример ниже выведет: `двадцать`, но если бы значением переменной `num` было бы любое число кроме `5`, `20` или `100`, то результатом исполнения программы было бы - `такое число отсутствует`.
```go
num := 20

switch num {
case 5:
    fmt.Println("пять")
case 20:
    fmt.Println("двадцать")
case 100:
    fmt.Println("сто")
default:
    fmt.Println("такое число отсутствует")
}
```

Так же варианты в `case` можно перечеслять через запятую, если для них нужно выполнить одинаковое действие. Пример ниже выведет - `съедобное`, так же как если бы значение `sub` было бы `апельсин` или `банан`.
```go
sub := "арбуз"

switch sub {
case "апельсин", "арбуз", "банан":
    fmt.Println("съедобное")
case "утюг", "шкаф", "тарелка":
    fmt.Println("несъедобное")
default:
    fmt.Println("неопознано")
}
```

Кроме того, в `case` можно перечислять не только конкретные варианты, но и целые условия. В этом случае переменная для сравнения, располагающаяся сразу после ключевого слова `switch` не требуется. Пример ниже выведет - `малолетний`. 
Порядок `case` очень важен, потому что `switch` идет сверху вниз и  останавливает свое выполнение на первом варианте, который вернет `true`, до остальных вариантов он даже не дойдет.
```go
age := 13

switch {
case age >= 18:
    fmt.Println("совершеннолетний")
case age >= 14:
    fmt.Println("спросить паспорт")
case age >= 0:
    fmt.Println("малолетний")
default:
    fmt.Println("Возраст должен быть больше 0")
}
```

Ключевое слово `fallthrough` указывает выполнить следующий за нашим `case` без проверки значения, то есть выполнить его в любом случае. Пример ниже выведет - `AB`.
```go
start := "A"
switch start {
case "A":
    fmt.Print("A")
    fallthrough
case "B":
    fmt.Print("B")
case "C":
    fmt.Print("C")
}
```

Go использует неявный оператор `break` для каждого варианта. Это отличается от таких языков, как `PHP` или `Java`, где `break` необходим. Если нужно, мы также можем явно указать `break`.
```go
sub := "арбуз"

switch sub {
case "апельсин", "арбуз", "банан":
    fmt.Println("съедобное")
    break
case "утюг", "шкаф", "тарелка":
    fmt.Println("несъедобное")
    break
default:
    fmt.Println("неопознано")
}
```
