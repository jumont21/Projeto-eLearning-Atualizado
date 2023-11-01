# Projeto-eLearning-Atualizado
Sistema de venda de materiais educacionais digitais
### Laboratório de Engenharia de Software
## Diagrama de Classes Completo

```mermaid

classDiagram
 direction LR
  class Usuario {
    +ID: int
    +Nome: string
    +Email: string
    +Senha: string
   }

  class Comprador {
    +ID: int
    +Nome: string
    +Email: string
    +Senha: string
    +Endereco
    +Telefone
    +Histcompra
    +Logar(CPF: String, senha: String): boolean
    +AutenticarComprador(email: String)
    +ConsultarHistoricoCompra()
    +EnviarChatPrivado(destinatario: Vendedor, mensagem: string, dataEnvio: date): boolean
  }

  class GestorComentario {
    +CriarComentario()
    +AtualizarComentario()
    +VisualizarComentario()
    +ExcluirComentario()
  }

   class GestorComentarioOfensivo {
    +RemoverComentarioOfensivo()
  }

  class GestorAvaliacao {
    +CriarAvaliacao()
    +AtualizarAvaliacao()
    +VisualizarAvaliacao()
    +ExcluirAvaliacao()
  }

  class GestorProduto {
    +FavoritarProduto()
    +SolicitarProduto()
    +FinalizarCompraProduto()
  }

  class Vendedor {
  +ID: int
  +Nome: string
  +Email: string
  +Senha: string
  +Telefone: string
  +Produto: string
  +Descricao: string

  +Logar(CNPJ: String, senha: String): boolean
  +AutenticarVendedor(email:string)
  +ConsultarHistoricoCompra(): List<ProdutoComprado>
  
}

class GestorListaProduto {
    +CriarListagem()
    +VisualizarListagem()
    +AtualizarListagem()
    +ExcluirListagem()
}

class ChatPrivado {
   +ID: int  
   +Remetente: string  
   +Destinatario: string
   +Conteudo: string  
   +DataEnvio: date  
   +Lido: boolean  
 
   +EnviarMensagem(mensagem: string): boolean
   +LerMensagensNaoLidas(): List<Mensagem>
}

    class Produto {
    +ID: int
    +Nome: string
    +Descricao: string
    +Preco: float
    +Categoria: string

}

class ProdutoComprado {
    +ID: int
    +Nome: string
    +Descricao: string
    +Preco: float
    +DataCompra: date
}

  class Administrador {
  +GestorCompradores
  +GestorVendedores
  +GestorRelatorio
}

class GestorComprador {
  +RemoverCompradores()
}

class GestorVendedor {
  +RemoverVendedores()
}

class GestorRelatorio {
  +CriarRelatorio()
  +LerRelatorio(id: int)
  +AtualizarRelatorio(id: int, novoConteudo: string)
  +ExcluirRelatorio(id: int)
}

  class ListaProduto {
    +ID: int
    +Nome: string
    +Produtos: List<Produto>
  }

  class Compra {
    +ID: int
    +Produto: Produto
    +Comprador: Comprador
    +AprovarCompra()
    +EfetuarPagamento()
  }

  class Avaliacao {
    +ID: int
    +Nota: int
    +Comentario: string
    +AvaliarVendedor()
    +AvaliarProduto()
  }

  class Comentario {
    +ID: int
    +Texto: string
    +Autor: Comprador
    +Produto: Produto
  }

  class Relatorio {
    +ID: int
    +Dados: string
    +GerarRelatorio()
  }

  class Busca {
    +FiltrarPorCategoria()
    +FiltrarPorPreco()
  }

  Usuario "1" <|-- "1" Comprador : Tipo 
  Usuario "1" <|-- "1" Vendedor : Tipo 
  Usuario "1" <|-- "1" Administrador : Tipo 
  
  Comprador "1" --|> "*" GestorComentario : Gerencia
  Comprador "1" --|>  "*" Avaliacao : Gerencia 
  Comprador "1" --|>  "*" GestorProduto : Gerencia 
  Comprador "1" --|>  "*" ProdutoComprado : Gerencia
  Comprador "1" --|>  "*" Compra : Gerencia
  Comprador "1" --|>  "*" Avaliacao : Gerencia 
  Comprador "1" --|>  "*" Comentario : Gerencia 
  Comprador "1" --|>  "*" ChatPrivado : Gerencia 
  Comprador "1" --|>  "*" ProdutoComprado : Gerencia 
  Comprador "1" --|>  "1" Busca : Gerencia 
  Comprador "1" --> "1" GestorAvaliacao : Gerencia 

  Vendedor "1" o-- "1" ListaProduto : Gerencia Lista 
  Vendedor "1" o-- "0..*" ChatPrivado : Recebe Chat 
  Vendedor "1" *-- "1" GestorListaProduto : Gerencia Lista 

  Administrador "1" --> "1" GestorComprador : Gerencia Comprador 
  Administrador "1" --> "1" GestorVendedor : Gerencia Vendedor 
  Administrador "1" --> "1" GestorRelatorio : Gera Relatório 
  Administrador "1" --> "1" GestorComentarioOfensivo : Remove Comentario Ofensivo 
  Administrador "1" --> "1" Comprador : Remove Comprador 
  Administrador "1" --> "1" Vendedor : Remove Vendedor 
  Administrador "1" --> "1" Relatorio : Gera Relatório 


  Produto "1" *-- "0..*" ListaProduto : Contido em 

  Compra "1" o-- "0..1" ProdutoComprado : Aprovar Compra 

  ListaProduto "1" *-- "0..*" Produto : Contém Produto 

  Busca "1" --> "1" Produto : Retorna Produto

```
## Diagrama de Classes Dividido

### Diagrama 1: Usuário, Comprador, Vendedor, Administrador

``` mermaid 

classDiagram
 direction LR
  class Usuario {
    +ID: int
    +Nome: string
    +Email: string
    +Senha: string
   }

  class Comprador {
    +ID: int
    +Nome: string
    +Email: string
    +Senha: string
    +Endereco
    +Telefone
    +Histcompra
    +Logar(CPF: String, senha: String): boolean
    +AutenticarComprador(email: String)
    +ConsultarHistoricoCompra()
    +EnviarChatPrivado(destinatario: Vendedor, mensagem: string, dataEnvio: date): boolean
  }

  class Vendedor {
    +ID: int
    +Nome: string
    +Email: string
    +Senha: string
    +Telefone: string
    +Produto: string
    +Descricao: string

    +Logar(CNPJ: String, senha: String): boolean
    +AutenticarVendedor(email:string)
    +ConsultarHistoricoCompra(): List<ProdutoComprado>
  }

  class Administrador {
  +GestorCompradores
  +GestorVendedores
  +GestorRelatorio
}

  Usuario "1" <|-- "1" Comprador : Tipo 
  Usuario "1" <|-- "1" Vendedor : Tipo 
  Usuario "1" <|-- "1" Administrador : Tipo 


```

### Diagrama 2: GestorComentario, GestorComentarioOfensivo, GestorAvaliacao, GestorProduto

``` mermaid

classDiagram
 direction LR

   class GestorComentario {
    +CriarComentario()
    +AtualizarComentario()
    +VisualizarComentario()
    +ExcluirComentario()
  }

   class GestorComentarioOfensivo {
    +RemoverComentarioOfensivo()
  }

  class GestorAvaliacao {
    +CriarAvaliacao()
    +AtualizarAvaliacao()
    +VisualizarAvaliacao()
    +ExcluirAvaliacao()
  }

  class GestorProduto {
    +FavoritarProduto()
    +SolicitarProduto()
    +FinalizarCompraProduto()
  }

  Comprador "1" --|> "*" GestorComentario : Gerencia 
  Comprador "1" --|>  "*" Avaliacao : Gerencia 
  Comprador "1" --|>  "*" GestorProduto : Gerencia 


```

### Diagrama 3: ChatPrivado, Produto, ProdutoComprado, ListaProduto, Compra

``` mermaid

classDiagram
 direction LR

class ChatPrivado {
   +ID: int  
   +Remetente: string  
   +Destinatario: string
   +Conteudo: string  
   +DataEnvio: date  
   +Lido: boolean  
 
   +EnviarMensagem(mensagem: string): boolean
   +LerMensagensNaoLidas(): List<Mensagem>
}

class Produto {
    +ID: int
    +Nome: string
    +Descricao: string
    +Preco: float
    +Categoria: string
}

class ProdutoComprado {
    +ID: int
    +Nome: string
    +Descricao: string
    +Preco: float
    +DataCompra: date
}

class Compra {
    +ID: int
    +Produto: Produto
    +Comprador: Comprador
    +AprovarCompra()
    +EfetuarPagamento()
}

  class ListaProduto {
    +ID: int
    +Nome: string
    +Produtos: List<Produto>
  }

ChatPrivado "1" --|> "0..*" Usuario : Envolvido em 
Produto "1" *-- "0..*" ListaProduto : Contido em 
Compra "1" o-- "0..1" ProdutoComprado : Aprovar Compra 


```

### Diagrama 4: Comentário, Relatório, Busca, GestorListaProduto

``` mermaid

classDiagram
 direction LR

class GestorComentarioOfensivo {
    +RemoverComentarioOfensivo()
  }

class Relatorio {
    +ID: int
    +Dados: string
    +GerarRelatorio()
}

class Busca {
    +FiltrarPorCategoria()
    +FiltrarPorPreco()
}

class GestorListaProduto {
    +CriarListagem()
    +VisualizarListagem()
    +AtualizarListagem()
    +ExcluirListagem()
}

Administrador "1" --|> "*" GestorComentarioOfensivo : Gerencia
Administrador "1" --|> "*" Relatorio : Gerencia 
Administrador "1" --|> "*" Busca : Gerencia 
Vendedor "1" *-- "1" GestorListaProduto : Gerencia Lista 


```

