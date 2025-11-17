## Test
-  teste unitário é uma prática central apoiada pelo sistema integrado pacote e o comando.```testing go test```

- Os testes são normalmente escritos em arquivos com o sufixo, localizado no mesmo pacote do código que eles testam._test.go

- Uma função de teste deve começar com a palavra e pegue uma indicação para como seu único parâmetro, que fornece métodos para relatar falhas de teste e registro.

- Comando de cobertura de test go test -cover
- Gerar relatorio de cobertura go test -coverprofile=resultado.out

```Testtesting.T```

```go
func TestHelloName(t *testing.T) {
    name := "Gladys"
    want := regexp.MustCompile(`\b`+name+`\b`)
    msg, err := Hello("Gladys")
    if !want.MatchString(msg) || err != nil {
        t.Errorf(`Hello("Gladys") = %q, %v, want match for %#q, nil`, msg, err, want)
    }
}
```

### Dataset