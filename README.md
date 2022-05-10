# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.


### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"


## Endpoint
O Endpoint da API é esta aqui -> https://json-server-luis.herokuapp.com/


## rotas que não precisam de autenticação

O usuario sem fazer login ou se cadastrar, pode visualizar os posts feitos pelos os outros usuarios

`GET /posts -  FORMATO DA RESPOSTA - STATUS 200`
```json

[
    {
      "img": "url.image",
      "id": 1
    },
    {
      "img": "url.image",
      "description": "text",
      "id": 2
    },
    {
      "img": "url.image",
      "description": "text",
      "userId": "2",
      "id": 3
    },
    {
      "img": "url.image",
      "description": "text",
      "userId": "1",
      "id": 4
    }
  ]
  ```


## Rotas que precisam de autenticação

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}

Após o usuario estar logado ele deve conseguir criar posts, e tambem consegue visualiazar as mensagens não só dele como a de outros usuarios e tambem criar suas mensagens

<h2 align ='center'> Criar post </h2>

`POST /posts - FORMATO DA REQUISIÇÃO - STATUS 201`
```json
{
	"img": "url",
	"desctipton": "lorem ipsum",
    "userId": "2"
}
```
   Os campos mostrados no exemplo não são obrigatórios, mas o ideal e ter eles, e você consegue mandar mais coisas no corpo da requisição não só eles



<h2 align ='center'> Criar mensagens </h2>

Da mesma forma de criar posts, consegimos criar mensagens, desta forma:

`POST /messages - FORMATO DA REQUISIÇÃO - STATUS 201`
```json
{
	"message": "text",
    "userId": "2"
}
```

<h2 align ='center'> Visualizar mensagens </h2>

`GET /messages - FORMATO DA REQUISIÇÃO - STATUS 200`
```json
[
	{
		"text": "texto teste",
		"userId": "2",
		"id": 1
	},
	{
		"text": "texto teste",
		"id": 2
	},
	{
		"text": "texto teste",
		"userId": "1",
		"id": 3
	},
	{
		"text": "texto teste",
		"userId": "1",
		"id": 4
	}
]
```