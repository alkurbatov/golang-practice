# Идиоматичный Go: соглашения и антипаттерны

Рекомендации по написанию читаемого кода на Go.

## Инициализация объектов

Многие разработчики, пришедшие в `Go` из таких языков как `C++`, `Java` или
`Python`, часто пишут код создания и инициализации объекта так:

```go
package point

type Point struct {
    x, y int
}

func New() *Point {
    return &Point{}
}

func (p *Point) Init(x, y int) {
    p.x = x
    p.y = y
}
```

В `Go` применение `New` в паре с `Init` считается антипаттерном, так как
усложняет код и разбивает процесс создания объекта на две части. Идиоматичный
вариант:

```go
package point

type Point struct {
    x, y int
}

func New(x, y int) *Point {
    return &Point{x: x, y: y}
}
```

Название конструктора зависит от контекста пакета. `New` используется, когда
пакет предоставляет ровно один ключевой тип (например, пакет `point`). Если в
пакете несколько типов, конструктор называется `NewType`, где `Type` — имя
создаваемого типа:

```go
package geometry

type Point struct {
    x, y int
}

type Circle struct {
    x, y int
    radius int
}

func NewPoint(x, y int) *Point {
    return &Point{x: x, y: y}
}

func NewCircle(x, y, r int) *Circle {
    return &Circle{x: x, y: y, radius: r}
}
```

## Расположение мьютекса в структуре

Мьютекс размещается непосредственно над полями, которые он защищает.

```go
type Cache struct {
    // MaxRetryCount максимальное допустимое количество повторных попыток.
    MaxRetryCount int

    mu sync.Mutex
    // data хранит закешированные ответы.
    data map[string]string
    // hits содержит количество попаданий в кеш.
    hits int
}
```

## Именование методов

### Run и Start

Метод с названием Run всегда блокирующий (например, `RunHTTPServer`), для его
неблокирующего запуска необходимо использовать оператор `go`.

Метод с названием Start всегда неблокирующий (например, `StartHTTPServer`),
внутри уже происходит запуск фоновой горутины.

### Locked

Метод с суффиксом Locked всегда предполагает выполнение под мьютексом (например,
sync.Mutex), который был взят перед вызовом метода.

```go
type Registry struct {
    mu           sync.Mutex
    services     map[string]string // имя -> адрес
    lastModified time.Time
}

func (r *Registry) Register(name, addr string) {
    r.mu.Lock()
    defer r.mu.Unlock()

    r.services[name] = addr
    r.touchLocked()
}

func (r *Registry) Deregister(name string) {
    r.mu.Lock()
    defer r.mu.Unlock()

    delete(r.services, name)
    r.touchLocked()
}

// touchLocked обновляет время последнего изменения реестра.
// Должен вызываться под r.mu.
func (r *Registry) touchLocked() {
    r.lastModified = time.Now()
}
```

Такой подход позволяет переиспользовать логику работы с защищёнными данными
и избежать рекурсивного захвата мьютекса.
