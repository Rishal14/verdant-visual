---
title: "Entendendo classes do Javascript"
isDraft: true
---


const user = {
  fistName: "Renato",
  secondName: "Lacerda",
  favoriteColor: "Vermelho",
};
```

Certo, o problema é que eu provavelmente não quero escrever esse objeto para cada um dos meus usuários. Uma forma muito mais interessante seria ter uma função que cria esse objeto.

```javascript
function createUser(firstName, secondName, favoriteColor) {
  return { firstName, secondName, favoriteColor };
}

const user1 = createUser("Renato", "Lacerda", "Vermelho");
```

!! { firstName } é a mesma coisa que escrever { firstName: firstName}.
