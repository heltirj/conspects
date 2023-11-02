# Основы
Материал взят из глав 
- Integers
- Iteration
## Введение в TDD
Основной принцип TDD - сначала пишем тест, указываем поведение функции на входе и выходе, затем - пишем код функции.

Для написания тестов в go используем файлы с постфиксом _test. Например, файл с функциями называется functions.go, мы создаём файл functions_test.go. 

Далее в этом файле мы пишем тест:

```go
package integers

import "testing"

func TestAdder(t *testing.T) {
	sum := Add(2, 2)
	expected := 4

	if sum != expected {
		t.Errorf("expected '%d' but got '%d'", expected, sum)
	}
}
```

После чего в файле functions.go создаём уже нужную функцию:

```go
func Add(x, y int) int {
	return x + y
}
```

## Документирование
Для написания документации используются следующие два принципа:
- Перед сигнатурой каждой функции пишем комментарий, начинающийся с её названия, после чего во втором лице пишем, что делает функция:

  ```go
  // Add takes two integers and returns the sum of them.
  func Add(x, y int) int {
   return x + y
  }
  ```
- Добавляем примеры поведения функции в тестовом файле.
  ```go
  func ExampleAdd() {
   	sum := Add(1, 5)
   	fmt.Println(sum)
   	// Output: 6
   }
   ```

Для просмотра документации используем модуль godoc. Если его нет в системе, его нужно установить с помощью `go get golang.org/x/tools/cmd/godoc`.

Далее пишем `godoc -http=:6060` и переходим в браузере на http://localhost:6060/pkg/. В открывшемся списке мы можем найти наш пакет. 

## Запуск тестов
Переходим в папку, где нужно запустить нужный тест, пишем `go test`. Результат будет выглядеть как:
```
heltirj@heltijr iteration % go test     
PASS
ok      learning_go_with_tests/iteration        0.527s
```
Чтобы увидеть, какие тесты у нас выполнились, пишем `go test -v `
```
heltirj@heltijr iteration % go test     
=== RUN   TestRepeat
--- PASS: TestRepeat (0.00s)
=== RUN   ExampleRepeat
--- PASS: ExampleRepeat (0.00s)
PASS
ok      learning_go_with_tests/iteration        0.130s
```

## Написание бенчмарков
Бенчмарки - это тесты производительности. Для их написания в тестовую функцию передаётся объект `*testing.B`
```go
func BenchmarkRepeat(b *testing.B) {
	for i := 0; i < b.N; i++ {
		Repeat("a")
	}
}
```
Для запуска бенчмарков используем `go test -bench=.`. Пример вывода:
```
goos: darwin
goarch: amd64
pkg: github.com/quii/learn-go-with-tests/for/v4
10000000           136 ns/op
PASS
```
Это значит, что тестируемая операция была выполнена 10000000 раз, в ходе чего было вычислено среднее время её выполнения.

## Дополнительное чтение
[Больше про написание экзэпмплов](https://go.dev/blog/examples) 
[Бенчмарки](https://pkg.go.dev/testing#hdr-Benchmarks)
