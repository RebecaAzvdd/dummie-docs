## Structs
- Declarar um tipo de um agrupador de dados

### Receiver 
- Função com receptor

```go
func (p produto) precoComDesconto() float64{
    // produto uma struct um tipo, float64 o retorno
}
```

### Struct Aninhada

```go
type item struct{

}

type pedido struct{
    itens []item // slice de item uma outra struct
}
```

### Pseudo Herança nas structs

```go
type item struct{
    nome string
}

type pedido struct{
    item // campos anonimos = posso acessar diretamente pela estrututa pedido pedido.nome
}
```

### Struct para Json

```go
type item struct{
    ID int `json:"id"`
    nome string `json:"nome"`
    preco int `json:"preco"`
}

func main() {
    fmt.Println(string(produtoJson))
}
```