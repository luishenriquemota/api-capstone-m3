## Endpoints

A API tem um total de 08 endpoints, sendo em volta dos usuários (Client) e (Collector) 

O url base da API é https://api-capstone-m3.herokuapp.com/


## Rotas que não precisam de autenticação

<h2 align ='center'> Cadastro do usuário </h2>

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
	"email": "luis@gmail.com",
	"password": "123456",
	"name": "client",
	"cpf": "cpf || cnpj",
	"image":"url.img",
	"city": "Vargem grande paulista",
	"type": "client",
	"wallet": 1
}
```

Existem dois campo obrigatórios para essa rota que são os de email e password, você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

<h2 align ='center'> Login do usuário </h2>

`POST /login - FORMATO DA REQUISIÇÃO`
```json
{
	"email": "teste@gmail.com",
	"password": "123456"
}
```

Este endpoint é usado para fazer login do usuário que já está cadastrado.

<h2 align ='center'> Mostrar dados do usuário </h2>

`GET /users/:userid - FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"email": "client@gmail.com",
	"password": "$2a$10$iwhrBx36SIRkxvoxM52XBubW/lPa7T6a1aHMUpVlnUy9f5IukGfvu",
	"name": "client",
	"cpf": "cpfcnpj",
	"image": "url.img",
	"city": "curitiba",
	"type": "client",
	"wallet": 1,
	"id": 1
}
```

Este endpoint é usado para mostrar os dados de um usuário específico, passando com o id do usuário na rota.

## Rotas que necessitam de autenticação

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após estar logado, ele deve conseguir utilizar todas os rotas que serão descritas abaixo.


## rotas do client

<h2 align ='center'> Cadastrar um resíduo </h2>

este endpoint é usado para cadastrar um resíduo.

`POST /waste - FORMATO DA REQUISIÇÃO`
```json
{
	"category": "Eletronicos",
	"measure": 10,
	"client_id": 3,
	"image": "url.img",
	"status": "Pendente",
	"id": 2
}
```

<h2 align ='center'> Alterar dados do resíduo cadastrado </h2>

caso o client tenha errado algum dado preenchido na hora de cadastrar o resíduo, ele pode alterar usando este endpoint:

`PATCH /waste/:id - FORMATO DA REQUISIÇÃO`
```json
{
	"category": "Papel",
}
```

<h2 align ='center'> Deletar resíduo cadastrado </h2>

Também é possível deletar o resíduo cadastrado, utilizando este endpoint:

`DELETE /waste/:id`
```json
não é necessário um corpo da requisição.
```

## Rotas do collector

<h2 align ='center'> Listar empresas </h2>

Aqui o coletor poderá listar as empresas e ver a descrição de cada uma delas.

`GET /companies - FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"name": "ecoreciclagens",
	"city": "Curitiba",
	"image": "logo.img",
	"materials": [
		"Papel",
		"Plastico"
	]
},
{
	"name": "reciclaEletronicos",
	"city": "Vargem grande paulista",
	"image": "logo.img",
	"materials": [
		"Eletronicos"
	]
}
```

<h2 align ='center'> Listar todos resíduos </h2>

Podemos listar todos os resíduos que os clients cadastraram  com este endpoint:

> `GET /waste - FORMATO DA RESPOSTA - STATUS 200`
```json
{
	"category": "Papel",
	"measure": 5,
	"client_id": 1,
	"image": "url.img",
	"status": "Pendente",
	"id": 1
},
{
	"category": "Eletronicos",
	"measure": 10,
	"client_id": 3,
	"image": "url.img",
	"status": "Pendente",
	"id": 2
},
{
	"category": "Oleo",
	"measure": 3,
	"client_id": 1,
	"image": "url.img",
	"status": "Pendente",
	"id": 3
}
```

<h2 align ='center'> Alterar resíduo </h2>

Com este endpoint podemos fazer a alteração de qualquer propriedade do resíduo, mas utilizaremos para alterar o "status" e adicionar a propriedade "collector_id".

`PATCH /waste/:id - FORMATO DA REQUISIÇÃO`
```json
{
	"status": "reservado",
	"collector_id": 2
}
```
O "collector_id" ira recerber o id do collector que ira realizar a coleta do resíduo.

<h2 align ='center'> Abandono do resíduo coletado </h2>

Com este endpoint o coletor poderá desistir de um resíduo que foi pego por ele, assim fazendo com que o resíduo volte para a lista de resíduos pendentes

`PUT /waste/:id - FORMATO DA RESPOSTA`
```json
não é necessário um corpo da requisição.
```
