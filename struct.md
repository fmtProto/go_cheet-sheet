## `Struct(Структура)`

`Cтруктура(struct)` - это именованная коллекция данных(полей данных), которые могут быть разных типов и представляют в целом единую сущность. Структуру в Go можно сравнить с классом в объектно-ориентированных языках.
```go
// формат
type struct_name struct {
    field_name1 field_type1
    field_name2 field_type2
    ...
}

// пример
type people struct {
    name string
    age  int
}
```

Для создания экземпляра структуры нужно создать структурную переменную.
```go
type people struct {
    name string
    age  int
}

// каждое поле в одной строке
people1 := people{
    name: "Oleg",
    age:  23,
} // {name:Oleg age:23}

// не присваивая значения ни одному из полей
var people2 = people{} // {name: age:0}

// все поля в одной строке
people3 := people{name: "Anna", age: 20} // {name:Anna age:20}

// можно объявить не все поля
var people4 = people{
    age: 20,
} // {name: age:20}

// без имен полей, значения для каждого поля должны быть указаны последовательно
people5 := people{"Sam", 11} // {name:Sam age:11}
```

Доступ к полям структуры можно получить с помощью оператора точки `.`.
```go
type people struct {
    name string
    age  int
}

people1 := people{
    name: "Oleg",
    age:  23,
}

fmt.Println(people1.name) // Oleg
```

Точно так же значение может быть присвоено и полю структуры. 
```go
people1 := people{
    name: "Oleg",
    age:  23,
}

people1.name = "Frank"

fmt.Println(people1.name) // Frank
```

Указатель на структуру:
- `&`
```go 
type people struct {
    name string
    age  int
}

people1 := &people{
    name: "Oleg",
    age:  23,
}

fmt.Println(people1) // &{Oleg 23}
```
- `new()`
Использование `new()`: 1. создаст стурктуру 2. Инициализирует все поля их нуевыми значениями 3. Вернет ссылку на созданную структуру
```go
type people struct {
    name string
    age  int
}

people1 := new(people)

fmt.Println(people1)       // &{ 0}
fmt.Printf("%+v", people1) // &{name: age:0}
fmt.Printf("%p", people1)  // 0xc000010030
```

Структура может иметь анонимные поля, то есть поля без имени. Тип станет именем поля. 
```go
type people struct {
    string
    age int
}

people1 := people{
    string: "Ben",
    age:    40,
}

fmt.Printf("%+v", people1)  // {string:Ben age:40}
fmt.Println(people1.string) // Ben
```

Структура передается по значению, то есть копируется

___дописать___ вложенные структуры,  сравнение,   metadata fields,  печать структуры(маршал, %+v)
