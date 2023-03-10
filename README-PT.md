# Token Fox
``Uma nova maneira de criar e gerencia token!``

O Token fox foi criado para aprimorar o gerenciamento de token.

## Crie um token

```js
const tokenFox = require("token-fox");

const myToken = tokenFox.Sign({
    date_expires: 30, // Tempo de expiração
    date_expires_type: "day", // Tipo de expiração (default = min)
    origin: "*" // Origem (use para autorizar requisições)
}, {
    username: "teste", // Username - Dono do token
    secret: "teste", // Palavra secreta
    detail: {
        username: "teste"
    } // detail são informações adicionais que você pode adicionar ao token
})

console.log(myToken);
// Output: eyJkYXRlX2NyZWF0aW9uIjoxNjcxNTQ0OTY2MDc0LCJkYXRlX2V4cGlyZXMiOjE2NzE1NDY3NjYwNzQsIm9yaWdpbiI6IioiLCJ1dWlkIjoiNjU5LTgzNDM4MC00My04LjE1OSJ9.eyJkZXRhaWwiOnsidXNlcm5hbWUiOiJ0ZXN0ZSJ9LCJ1c2VybmFtZSI6InRlc3RlIn0=.ZXlJd0lqb3hNREFzSWpFaU9qY3hMQ0l5SWpvNE5pd2lNeUk2TVRJeUxDSTBJam94TURBc0lqVWlPamN4TENJMklqbzROU3dpTnlJNk5qRjk=
```

## Gerencie seu token
```js
const tokenFox = require("token-fox");

const myToken = new tokenFox.ManagerToken(token, "palavra-chave")

// Obtenção

myToken.GetUsername() // Retorna o username
myToken.GetInfo("chave") // Retorna um valor adicionado ao detail
myToken.GetUUID() // Retorna um identificador único
myToken.Get(chave, from? "header"|"pl"|"*"|"details") // Retorna o valor solicitado da sua determinada origem

// Atualizadores
myToken.SetUsername(novoValor) // Cria um novo token e retorna
myToken.SetInfo(item: {key?: valor}) // Cria um novo token com essa nova informação e retorna
myToken.SetOrigin(novoValor) // Cria um novo token com essa origem
myToken.ExpiresAdd(tempo, tipo? "day"|"year"|"sec"|"min") // Extende o tempo de expiração

// Importante avisar que não altera o token dentro de myToken, para isso:
myToken.Refresh(novoToken)
// Exemplo
myToken.Refresh(myToken.ExpiresAdd(30, "min"))
```