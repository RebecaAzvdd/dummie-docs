## Golang

- Criação de projeto
mkdir go-playground && cd go-playground
go mod init go-playground

## Estruturas Básicas

- Declaração de tipos
```go
var nome string = "Rebeca"
idade := 25  // inferência
fmt.Println(nome, idade)
```
- Constantes e iota (muito usado para enums):
- Iota: É um contador automático usado em constantes, muito útil para criar enums.
Começa em 0 e incrementa automaticamente a cada linha.

```go
const (
    A = iota
    B
    C
)
fmt.Println(A, B, C) // 0, 1, 2
```

### Estruturas de dados
- Arrays e slices
- Slices: São arrays dinâmicos (tamanho variável) — diferente de arrays fixos.Permitem adicionar, remover e percorrer elementos facilmente. Cada slice tem len() (tamanho) e cap() (capacidade alocada).

```go
numeros := []int{1, 2, 3, 4}
numeros = append(numeros, 5)
fmt.Println(numeros, len(numeros), cap(numeros))
```
- Mapas
- Estrutura de chave → valor (semelhante a objetos JS ou dicionários Python).
```go
notas := map[string]float64{
    "Go":   9.5,
    "Java": 8.0,
}
fmt.Println(notas["Go"])
```

- Structs e métodos
- São estruturas de dados personalizadas, tipo classes sem métodos por padrão.
Permitem agrupar campos relacionados. Permite composição em vez de herança → Go prefere isso para reutilização.
```go
type Pessoa struct {
    Nome string
    Idade int
}

func (p Pessoa) Falar() {
    fmt.Println("Oi, meu nome é", p.Nome)
}

func main() {
    p := Pessoa{"Rebeca", 25}
    p.Falar()
}
```

- Interfaces (implícitas)
- São contratos de métodos que tipos podem implementar sem declarar explicitamente.
Go verifica se um tipo possui os métodos da interface; se sim, ele “implementa” a interface automaticamente.
Permite polimorfismo de forma leve e idiomática, sem precisar herança.
```go
type Animal interface {
    Falar() string
}

type Cachorro struct{}
func (c Cachorro) Falar() string { return "Au au" }

type Gato struct{}
func (g Gato) Falar() string { return "Miau" }

func main() {
    animais := []Animal{Cachorro{}, Gato{}}
    for _, a := range animais {
        fmt.Println(a.Falar())
    }
}
```

- Funções e erros
```go
func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, fmt.Errorf("divisão por zero")
    }
    return a / b, nil
}

func main() {
    r, err := dividir(10, 2)
    if err != nil {
        fmt.Println("Erro:", err)
    } else {
        fmt.Println("Resultado:", r)
    }
}
```
