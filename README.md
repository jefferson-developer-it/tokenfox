# Token Fox

``A new way to create and manage token!``

Token fox was created to enhance token management.

## Create a token

```js
const tokenFox = require("token-fox");

const myToken = tokenFox.Sign({
     date_expires: 30, // Expiration time
     date_expires_type: "day", // Expiration type (default = min)
     origin: "*", // Origin (use to authorize requests)
     username: "test", // Username - Token owner
     secret: "test", // Secret word
     detail: {
         username: "test"
     } // detail is additional information you can add to the token
 })

console.log(myToken);

// Output: eyJkYXRlX2NyZWF0aW9uIjoxNjcxNTQ0OTY2MDc0LCJkYXRlX2V4cGlyZXMiOjE2NzE1NDY3NjYwNzQsIm9yaWdpbiI6IioiLCJ1dWlkIjoiNjU5LTgzNDM4MC00My04LjE1OSJ9.eyJkZXRhaWwiOnsidXNlcm5hbWUiOiJ0ZXN0ZSJ9LCJ1c2VybmFtZSI6InRlc3RlIn0=.ZXlJd0lqb3hNREFzSWpFaU9qY3hMQ0l5SWpvNE5pd2lNeUk2TVRJeUxDSTBJam94TURBc0lqVWlPamN4TENJMklqbzROU3dpTnlJNk5qRjk=

```
## Manage your token

```js
const tokenFox = require("token-fox");

const myToken = new tokenFox.ManagerToken(token, "Secret Word")

// Obtaining

myToken.GetUsername() // Returns the username
myToken.GetInfo("key") // Returns a value added to the detail
myToken.GetUUID() // Returns a unique identifier
myToken.Get(chave, from? "header"|"pl"|"*"|"details") // Returns the requested value from your given source

// Updaters
myToken.SetUsername(newValue) // Creates a new token and returns
myToken.SetInfo(item: {key?: value}) // Create a new token with this new information and return
myToken.SetOrigin(newValue) // Create a new token with this origin
myToken.ExpiresAdd(time, type? "day"|"year"|"sec"|"min") // Extends the expiration time

// Important to note that it does not change the token inside myToken, for this:
myToken.Refresh(newToken)
// Example
myToken.Refresh(myToken.ExpiresAdd(30, "min"))
```