## Defer, Panic e Recover
- Defer: adia a execução de uma função até o fim da função atual. Útil para fechar arquivos, conexões ou liberar recursos.
- Panic: gera um erro crítico que interrompe a execução.
- Recover: captura um panic e permite continuar a execução.
```go
package main

import "fmt"

func exemplo() {
    defer fmt.Println("defer: sempre executa no final")
    
    fmt.Println("executando função")
    
    panic("algo deu errado!") // interrompe aqui
    fmt.Println("isso não será executado")
}

func main() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("recover capturou o panic:", r)
        }
    }()
    
    exemplo()
    fmt.Println("continua execução após panic")
}
```

## Controle de fluxo
- For é o único loop em Go (não existe while/ do-while). Pode ser usado de três formas:
Tipo C: for i := 0; i < 5; i++ { }
Iterando sobre slice/array: for i, v := range slice { }
Loop infinito: for { }
```go
// loop simples
for i := 0; i < 3; i++ {
    fmt.Println("i =", i)
}

// loop com range
nomes := []string{"Ana", "Bea", "Clara"}
for i, nome := range nomes {
    fmt.Println(i, nome)
}

// loop infinito com break
contador := 0
for {
    if contador == 3 {
        break
    }
    fmt.Println("contador =", contador)
    contador++
}
```

- Switch poderoso: aceita intervalos, múltiplos valores e não precisa de break.
```go
nota := 7
switch {
case nota >= 9:
    fmt.Println("Excelente")
case nota >= 6:
    fmt.Println("Bom")
default:
    fmt.Println("Precisa melhorar")
}
```

## Errors em Go
Não existe exception como em Java/Python.
Tratamento explícito: sempre checar err != nil.
Boas práticas: sempre retornar error quando algo pode falhar, sem lançar exceção.
```go
package main

import (
    "fmt"
    "os"
)

func main() {
    arquivo, err := os.Open("arquivo.txt")
    if err != nil {
        fmt.Println("Erro ao abrir arquivo:", err)
        return
    }
    defer arquivo.Close()
    fmt.Println("Arquivo aberto com sucesso")
}
```