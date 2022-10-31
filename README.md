# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Projetos Front-end.

## URL

https://projeto-frontend-api.herokuapp.com

### Rotas que não precisam de autorização

## Cadastro

POST /register

Exemplo do body:
```json
{
	"name": "Teste",
	"email": "teste@mail.com",
	"password": "Teste123@",
	"img": "teste.com",
	"description": "A gente testa tudo",
	"creationDate": "21/02/2000",
	"openingHours": "9:00 - 16:00"
}
```

Exemplo da resposta:
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlYUBtYWlsLmNvbSIsImlhdCI6MTY2NzIzOTA0MiwiZXhwIjoxNjY3MjQyNjQyLCJzdWIiOiIyIn0.2Y11guBkCrwgI2oM9R5c7uJvBb-pCutQsXDNyX11e4I",
	"user": {
		"email": "testea@mail.com",
		"name": "Teste",
		"img": "teste.com",
		"description": "A gente testa tudo",
		"creationDate": "21/02/2000",
		"openingHours": "9:00 - 16:00",
		"id": 2
	}
}
```

## Login

POST /login

Exemplo do body:
```json
{
  "email": "teste@mail.com",
  "password": "Teste123@"
}
```

Exemplo da resposta:
```json
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQG1haWwuY29tIiwiaWF0IjoxNjY3MjM5MDA1LCJleHAiOjE2NjcyNDI2MDUsInN1YiI6IjEifQ.MNSHlXhmopXaV_32L9_nHQUEEYrGTzasdD8rSWu2nhU",
	"user": {
		"email": "teste@mail.com",
		"name": "Teste",
		"img": "teste.com",
		"description": "A gente testa tudo",
		"creationDate": "21/02/2000",
		"openingHours": "9:00 - 16:00",
		"id": 1
	}
}
```

## Anúncios

Visualizar anúncios:

GET /announcement

Exemplo da resposta:
```json
[
  {
    "type": "Financeiro",
    "description": "Faça igual a milhares de brasileiros e escolha o Santander",
    "userId": 1,
    "id": 1
  },
  {
    "type": "Restaurantes",
    "description": "O BURGER KING do Brasil é um master franqueado do Burger King Corporation no país.",
    "userId": 1,
    "id": 2
  }
]
```

Visualizar anúncio com o dono dele:

GET /announcement?_expand=user

Exemplo da resposta:
```json
[
  {
    "type": "Financeiro",
    "body": "Tarifa zero no pacote de serviços?",
    "userId": 1,
    "id": 1,
    "user": {
      "email": "santander@mail.com",
      "password": "$2a$10$/k5sawhTYgQ34Aj.gvRrGOK.ZEDxoR7ANQVCJmLp0f/rcCh1wcFUi",
      "name": "Santander",
      "img": "https://www.santander.com.br/sites/WPC_CMS/imagem/21-09-08_194400_santander-banner.png?blobnocache=true",
      "description": "Faça igual a milhares de brasileiros e escolha o Santander",
      "id": 1
    }
  },
  {
    "type": "Restaurantes",
    "body": "Encontre um fantasma pelo App do BK, compre um Whopper e ganhe outro!",
    "userId": 2,
    "id": 2,
    "user": {
      "email": "bk@mail.com",
      "password": "$2a$10$/k5sawhTYgQ34Aj.gvRrGOK.ZEDxoR7ANQVCJmLp0f/rcCh1wcFUi",
      "name": "Burger King",
      "img": "https://francashopping.com.br/lojas_files/27778.jpg",
      "description": "O BURGER KING do Brasil é um master franqueado do Burger King Corporation no país.",
      "id": 2
    }
  }
]
```

### Rotas que precisam de autorização

## Usuário

Visualizar usuário:

GET /users/${id}

Exemplo da resposta:
```json
{
	"email": "teste@mail.com",
	"password": "$2a$10$e.SMXhb75yQonn4v2L9MaujLvPXAWCDt9SM23YID3BJtt30EmORnm",
	"name": "Teste",
	"img": "teste.com",
	"description": "A gente testa tudo",
	"creationDate": "21/02/2000",
	"openingHours": "9:00 - 16:00",
	"id": 1
}
```

Visualizar usuário com os anúncios que ele criou:

GET /users/1?_embed=announcement

Exemplo da resposta:
```json
{
	"email": "teste@mail.com",
	"password": "$2a$10$e.SMXhb75yQonn4v2L9MaujLvPXAWCDt9SM23YID3BJtt30EmORnm",
	"name": "Teste",
	"img": "teste.com",
	"description": "A gente testa tudo",
	"creationDate": "21/02/2000",
	"openingHours": "9:00 - 16:00",
	"id": 1,
	"announcement": [
		{
			"body": "Muito bom os testes",
			"userId": 1,
			"id": 1
		}
	]
}
```

## Criar anúncio

POST /announcement

Exemplo do body:
```json
{
  "body": "Muito bom os testes",
  "userId": 1
}
```

Exemplo da resposta:
```json
{
	"body": "Muito bom os testes",
	"userId": 1,
	"id": 2
}
```
