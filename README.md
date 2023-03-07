<h1 align="center">Borscht House</h1>

Fake API a base de JSON-Server + JSON-Server-Auth, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

A url base da API é https://borschthouse.onrender.com

[borscht house.zip](https://github.com/Equipe-8/borscht-house-server/files/10899559/borscht.house.zip)

<br/>

<h2 align="center"> Criação de usuário </h2>

```
POST /register - FORMATO DA REQUISIÇÃO
```

<br/>

```
{
  "name": "Teste",
  "email": "teste@gmail.com",
  "contact": "15997945635",
  "address": "Joa Soares, 25",
  "password": "654321",
  "confirmPassword": "654321"
}
```

<br/>

Caso dê tudo certo, a resposta será assim:

```
POST /users - FORMATO DA RESPOSTA - STATUS 201
```

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InRlc3RlQGdtYWlsLmNvbSIsImlhdCI6MTY3ODA0MzI4NCwiZXhwIjoxNjc4MDQ2ODg0LCJzdWIiOiIyIn0.oboGnP65PZE33tMVD3qL4q1rt3f7GMwTYfaloYEWXJg",
	"user": {
		"email": "teste@gmail.com",
		"name": "Teste",
		"contact": "15997945635",
		"address": "Joa Soares, 25",
		"confirmPassword": "654321",
		"id": 2
	}
}
```

<br/>

<h2 align="center">Possíveis erros </h2>

Caso você acabe errando e mandando algum campo errado, a resposta de erro será assim:

A senha necessita de 6 caracteres.

`POST /users -   FORMATO DA RESPOSTA - STATUS 400`

`"Password is too short"`

<br/>

Email já cadastrado:

`POST /users -   FORMATO DA RESPOSTA - STATUS 400`

`"Email already exists"`

<br/>

<h2 align="center">Login</h2>

`POST /login - FORMATO DA REQUISIÇÃO`

```
{
  "email": "test@mail.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```
{
	"accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjc4MDQzNTMyLCJleHAiOjE2NzgwNDcxMzIsInN1YiI6IjEifQ.iCTJvSqIGFAcf5p7gM2ldTjHLQy_9My6-IlYvE0bOL8",
	"user": {
		"email": "kenzinho@mail.com",
		"name": "Kenzinho",
		"id": 1
	}
}
```

<br/>

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token no localStorage para fazer a gestão do usuário no seu frontend.

<br/>

<h2 align="center">Rotas que necessitam de autorização</h2>

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token} Após o usuário estar logado, ele deve conseguir buscar os produtos da borscht house:

<br/>

<h2 align="center">Auto login</h2>

`GET /users/{userId}`

É necessario o Authorization: Bearer {token}.

<br/>

Não é necessário um corpo da requisição.

Caso dê tudo certo, a resposta será assim:

```
{
	"email": "teste@mail.com",
	"password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOhkuyt7FO",
	"name": "teste",
	"id": 2
}
```

<br/>

<h2 align="center">Editar Usuario</h2>

`PATCH /users/{userId}`

É necessario o Authorization: Bearer {token}.

```
{
  "address": "Jose Antonio, 259"
}
```

Caso dê tudo certo, a resposta será assim:

`GET /products - FORMATO DA RESPOSTA - STATUS 200`
<br/>

```
{
	"email": "teste@gmail.com",
	"password": "$2a$10$2VCkYSrs1vDUagvaN.JnpuRdK2gH5Mf71aWDgi84gk5vb7pKGV2Uy",
	"name": "Teste",
	"contact": "15997945635",
	"address": "Jose Antonio, 259",
	"confirmPassword": "654321",
	"id": 2
}
```

<br/>

<h2 align="center">Deletar Usuario</h2>

É necessario o Authorization: Bearer {token}.

`DELETE /users/{userId}`

<br/>
Não é necessário um corpo da requisição.

Caso dê tudo certo, a resposta será assim:

`{}`

<br/>

<h2 align="center">Produtos</h2>

É necessario o Authorization: Bearer {token}.

`GET /products`

Não é necessário um corpo da requisição.
Caso dê tudo certo, a resposta será assim:

`GET /products - FORMATO DA RESPOSTA - STATUS 200`

```
[
	{
		"name": "Borscht Vegetariano",
		"img": "http://localhost:3001/assets/food/borscht-ua.jpg",
		"country": "Ucrânia",
		"countryId": 1,
		"description": {
			"detail": "É um prato tradicional da Ucrânia, distingue-se pela sua consistência espessa e pela cor forte do seu principal ingrediente: a beterraba. Para ter um sabor mais apurado, a sopa é preparada no dia anterior e aquecida imediatamente antes de servir.",
			"ingredient": "beterraba, cebola, alho, couve, tomates,farinha de trigo, sour cream."
		},
		"id": 1,
		"countryFlag": "http://localhost:3001/assets/flags/ukraine-map-flag.svg"
	},
    {...}
]

```

<br/>

<h2 align="center">Países</h2>

É necessario o Authorization: Bearer {token}.

`GET /coyntries`

Não é necessário um corpo da requisição.
Caso dê tudo certo, a resposta será assim:

`GET /products - FORMATO DA RESPOSTA - STATUS 200`

```
[
	{
		"countryName": "Ucrânia",
		"countryId": 1,
		"about": {
			"1": "A Ucrânia é um país da Europa Oriental. kiev é a capital e a cidade mais populosa da Ucrânia. Fica no centro-norte do país, ao longo do rio Dnieper.",
			"2": "Seu nome vem de uma palavra que significa “fronteira”. ",
			"3": "A imigração ucraniana no Brasil ocorreu nos séculos XIX e XX, O Brasil abriga a maior comunidade ucraniana da América Latina, onde 75% da polulação da cidade Prudentópolis-PR são de ascendência ucraniana."
		}
	},
    {...}
]
```
