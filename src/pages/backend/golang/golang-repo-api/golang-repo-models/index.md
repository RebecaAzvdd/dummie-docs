# Models

- Em aplicações backend, um model representa uma entidade de dados, normalmente ligada a uma tabela do banco de dados.

- Definição da struct do tipo Comment

```go
type Comment struct {
    ID        uint64    `gorm:"primary_key;auto_increment" json:"id"`
    UserID    uint32    `gorm:"not null" json:"user_id"`
    PostID    uint64    `gorm:"not null" json:"post_id"`
    Body      string    `gorm:"text;not null;" json:"body"`
    User      User      `json:"user"`
    CreatedAt time.Time `gorm:"default:CURRENT_TIMESTAMP" json:"created_at"`
    UpdatedAt time.Time `gorm:"default:CURRENT_TIMESTAMP" json:"updated_at"`
}
```

1. Campos da struct → Cada campo é uma coluna da tabela:
2. ID uint64 → identificador único
3. UserID uint32 → id do usuário dono do comentário
4. PostID uint64 → id do post relacionado
5. Body string → texto do comentário
6. User User → referência à struct User (associação)
8. CreatedAt, UpdatedAt → timestamps automáticos

### Tags → As tags servem para configurar GORM ou JSON:
```
gorm:"primary_key;auto_increment" json:"id"
gorm:"..." → instruções do GORM sobre como salvar esse campo no banco.
json:"..." → nome do campo quando a struct for serializada em JSON (para API).
```

## Funções de um Model

- Models não são só structs. Geralmente, contêm métodos que operam sobre os dados, como:
- Essas funções normalmente recebem uma instância do banco de dados:
1. Criar (SaveComment)

2. Buscar (GetComments)

3. Atualizar (UpdateAComment)

4. Deletar (DeleteAComment)
```go
func (c *Comment) SaveComment(db *gorm.DB) (*Comment, error) 
```
**(c *Comment)** → receptor do método, significa que esse método atua sobre uma instância do Comment.

**db *gorm.DB** → ponte para o banco de dados usando o GORM.

**Retorno (*Comment, error)** → o método retorna o comentário criado e um erro se houver.

## Operações no banco (CRUD)

### Salvar
```
err := db.Debug().Create(&c).Error
```

**db.Debug()** → imprime queries SQL no terminal para debugging.

**Create(&c)**  → cria um registro no banco.

**Error**  → captura erro.

### Buscar
```
err := db.Debug().Model(&Comment{}).Where("post_id = ?", pid).Order("created_at desc").Find(&comments).Error

Model(&Comment{}) → diz qual tabela usar.

Where("post_id = ?", pid) → filtro SQL.

Order("created_at desc") → ordena do mais recente.

Find(&comments) → preenche o slice de comentários.

Error → retorna erro se houver.
```

### Atualizar
- Atualiza campos específicos (Body e UpdatedAt) de um comentário.

```
db.Debug().Model(&Comment{}).Where("id = ?", c.ID).Updates(Comment{Body: c.Body, UpdatedAt: time.Now()})
```

### Deletar
```
db.Debug().Model(&Comment{}).Where("id = ?", c.ID).Delete(&Comment{})
```
