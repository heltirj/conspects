# Циклы, массивы, срезы
Материал взят из глав:
- Iteration
- Arrays and slices

## Цикл for
В go нет циклов while, do while, until, foreach и т. д. Весь их функционал реализуется с помощью цикла for.

## Примеры
```go
	package main

import "fmt"

func main() {

    i := 1
    for i <= 3 {
        fmt.Println(i)
        i = i + 1
    }

    for j := 7; j <= 9; j++ {
        fmt.Println(j)
    }

    for {
        fmt.Println("loop")
        break
    }

    for n := 0; n <= 5; n++ {
        if n%2 == 0 {
            continue
        }
        fmt.Println(n)
    }
}
```

Более частая ситуация - проходимся с помощью цикла for по какой-нибудь последовательности. В go четыре вида последовательностей - массив (array), срез (slice), карта (map), строка (string). 

## Массив
Коллекция с фиксированным количеством элементов, с данными одного типа.
Инициализируются двумя способами:
- [N]type{value1, value2, ..., valueN} e.g. numbers := [5]int{1, 2, 3, 4, 5}
- [...]type{value1, value2, ..., valueN} e.g. numbers := [...]int{1, 2, 3, 4, 5}

## Дополнительные материалы
[Строки форматирования] https://pkg.go.dev/fmt 





