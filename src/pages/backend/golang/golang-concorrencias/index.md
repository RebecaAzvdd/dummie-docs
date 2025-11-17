### [Concorrencias Doc do Go](https://go.dev/doc/effective_go#goroutines)
### [Site Externo Goroutines](https://dev.to/jeffotoni/um-pouco-sobre-goroutines-em-go-3lbk)
### [Concorrencias](https://medium.com/@rafaelmgr12/concorr%C3%AAncia-em-go-85b6a127b12f)
### [Select](https://gobyexample.com/select)


## Concorrencias vs Paralelismo
- Go é uma linguagem concorrente
- Paralelismo - Executar codigo simultaneamento em processadores fisicos diferentes.
- Concorrencia - intercalar (administrar) varios processos ao mesmo tempo e isso pode ocorrer em um unico processador fisico

- Paralelismo exige muito mais do SO e do hardware.
- Concorrencia é a forma de estruturar o seu programa. E a composição de processos (funcoes) que executam de forma independente.

## Goroutines
- Ao definir a palavra go ele vai chamar esse codigo de forma idependente similar uma thread.
```go
func main() {
    go fale() //fale é uma func que esta usando uma for para definir a iteraçãp
    fale() //roda na thread principal
}
```

## Chanels
- Chanel é um tipo é usado para comunicar enviar e receber as informações. Usado com goroutines
- ``<-chan`` canal somente de leitura
```go
func main(){
    ch := make(chan int, 1)
    ch <- 1 // enviando dados para o canal
    <-ch // recebendo dados do canal

    ch <- 2
    fmt.println(<-ch)
}
```

- **Multiplexar** misturar (mensagens) em um canal só

## Deadlocks
- ocorre quando todas as goroutines são bloqueadas e esperam que umas às outras prossigam, resultando na parada do programa indefinidamente.

### Buffer
- tamanho variável que implementa ambos e interfaces, permitindo que ele seja usado para manipulação eficiente de dados na memória

### Select

### Padrão de Concorrencias

