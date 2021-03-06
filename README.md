# api-v1
A api disposta aqui é para uso público de desenvolvedores e nossos clientes.

# Autenticação

- É necessario um usuário do tipo "admin" gerar o token em `Configurações >> Integrações >> Token de integrações` ou gerar o token através da api;
- O token não expira e pode ser renovado a qualquer hora pelo usuário;
- Após gerar o token, utilizar no cabeçalho como X-Api-Key o token gerado;
- Se o token estiver inválido, será retornado `401`, como erro de permissão e acesso não autorizado;

## POST - /ApiAuth/autenticar

### body
```
{
    "email": string,
    "senha": string
}
```

### retornos
```
200 - OK;
400 - Erro de validação;
400 - Erro de autenticação;
502 - Erro interno no servidor;

{
    "body": {
        "token": string, // X-Api-Key
        "empresa": string, // Estabelecimento
        "usuario": string // Nome do usuário
    },
    "errors": {},
    "data": [],
}
```

## POST - /api/v1/pedidos/buscar/

### body
```
{
    "id": int // ID do pedido
}
```

### cabeçalho
```
{
    "X-Api-Key": string // Gerado anteriormente na autenticação
}
```

### retornos
```
200 - OK;
400 - Erro de autenticação;
400 - Erro de validação;
502 - Erro interno no servidor;

{
    "body": {
        "idPedido": int,
        "cep": string,
        "nm": string,
        "complemento": string,
        "bairro": string,
        "cidade": string,
        "estado": string,
        "pais": string,
        "latitude": string,
        "longitude": string,
        "valor": float,
        "formaDePagamento": string,
        "ifood": string, // ID do pedido na plataforma do ifood
        "estoque": {
            [
                {
                    "qtds": string,
                    "idProduto": string,
                    "precoProduto": string,
                    "ingredientes": {
                        string idIngrediente: int qtdIngrediente
                    },
                    "opcoes": {
                        string idOpcao: int qtdOpcao
                    },
                    "opcoesValores": {
                        string idOpcao: float valorOpcao
                    }
                }
            ]
        },
        "clienteEmail": string,
        "clienteNome": string,
        "clienteTel": string
    },
    "errors": {},
    "data": [],
}
```

# Links úteis
- [Central de Ajuda](https://ajuda.gamadelivery.app)
- [Ambiente de homologação](https://staging.gamadelivery.app)
- [Collection no postman](./API.postman_collection.json)