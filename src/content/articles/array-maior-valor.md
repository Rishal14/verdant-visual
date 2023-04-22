---
title: "Retornando o maior valor em um Array"
publishDate: 2023-04-12
---


```javascript
const numbers = [4, 5, 4, 9, 13, 41, 43, 57, 30];
```

## Utilizando `sort()`



```javascript
function getLargestNumber(numbersArray) {
  return numbersArray.sort().slice(-1)[0];
}

getLargestNumber(numbers); // 9
```



```javascript
numbers.sort(); // [ 13, 30, 4, 4, 41, 43, 5, 57, 9 ]
```



```javascript
numbers.sort((a, b) => a - b); // [ 4, 4, 5, 9, 13, 30, 41, 43, 57 ]
```

Agora que temos o comportamento esperado, podemos refazer a nossa função:

```javascript
function getLargestNumber(numbersArray) {
  return numbersArray.sort((a, b) => a - b).slice(-1)[0];
}

getLargestNumber(numbers); // 57
```



```javascript
numbers.sort((a, b) => a - b); // [ 4, 4, 5, 9, 13, 30, 41, 43, 57 ]
numbers; // [ 4, 4, 5, 9, 13, 30, 41, 43, 57 ]
```



```javascript
function getLargestNumber(numbersArray) {
  return [...numbersArray].sort((a, b) => a - b).slice(-1)[0];
}

getLargestNumber(numbers); // 57
numbers; // [4, 5, 4, 9, 13, 41, 43, 57, 30]
```


```javascript
function getLargestNumber(numbersArray) {
  return [...numbersArray].sort((a, b) => a - b).at(-1);
}
```

## Iterando o array



```javascript
function getLargestNumber(numbersArray) {
  let largestNumber = 0;
  for (let i = 0; i < numbers.length; i++) {
    if (numbersArray[i] > largestNumber) {
      largestNumber = numbersArray[i];
    }
  }
  return largestNumber;
}

getLargestNumber(numbers); // 57
```



```javascript
getLargestNumber([-10, -1, -30, -45]); // 0
```



Não definir um valor inicial para `largestNumber` não funciona, pois a comparação `numbersArray[i] > largestNumber` sempre vai retornar `false`. Definir `largestNumber` como `null` também não resolve nosso problema[^3]:

[^3]: Para entender melhor o comportamento do `null` quando comparado com um número, dê uma lida nesse artigo: [Javascript : The Curious Case of Null >= 0](https://blog.campvanilla.com/javascript-the-curious-case-of-null-0-7b131644e274)

```javascript
let largestNumber;

2 > largestNumber; // false
-2 > largestNumber; // false

largestNumber = null;

2 > largestNumber; // true
-2 > largestNumber; // false
```

A solução então é usar o primeiro elemento do Array como valor inicial de `largestNumber` e começar o nosso loop do index 1.

```javascript
function getLargestNumber(numbersArray) {
  let largestNumber = numbersArray[0];
  for (let i = 1; i < numbers.length; i++) {
    if (numbersArray[i] > largestNumber) {
      largestNumber = numbersArray[i];
    }
  }
  return largestNumber;
}

getLargestNumber(numbers); // 57

const negativeNumbers = [-4, -5, -4, -9, -1, -3];
getLargestNumber(negativeNumbers); // -1
```



```javascript
function getLargestNumber(numbersArray) {
  let largestNumber = numbersArray[0];
  for (const number of numbersArray) {
    if (number > largestNumber) {
      largestNumber = number;
    }
  }
  return largestNumber;
}
```



```javascript
function getLargestNumber(numbersArray) {
  return numbersArray.reduce((accumulator, number) => {
    if (number > accumulator) {
      return number;
    } else return accumulator;
  });
}

getLargestNumber(numbers); // 57

const negativeNumbers = [-4, -5, -4, -9, -1, -3];
getLargestNumber(negativeNumbers); // -1
```



```javascript
function getLargestNumber(numbersArray) {
  return numbersArray.reduce((accumulator, number) => {
    return number > accumulator ? number : accumulator;
  });
}
```

## Utilizando Math.max()


function getLargestNumber(numbersArray) {
  return Math.max.apply(null, numbersArray);
}

getLargestNumber(numbers); // 57
```

Mas aqui também podemos usar a sintaxe de "espalhamento" (spread).

```javascript
function getLargestNumber(numbersArray) {
  return Math.max(...numbersArray);
}

getLargestNumber(numbers); // 57
```

## Conclusão

Chegamos em quatros formas diferentes de escrever a função:

```javascript
function getLargestNumberBySort(numbersArray) {
  return [...numbersArray].sort((a, b) => a - b).at(-1);
}

function getLargestNumberByFor(numbersArray) {
  let largestNumber = numbersArray[0];
  for (const number of numbersArray) {
    if (number > largestNumber) {
      largestNumber = number;
    }
  }
  return largestNumber;
}

function getLargestNumberByReduce(numbersArray) {
  return numbersArray.reduce((accumulator, number) => {
    return number > accumulator ? number : accumulator;
  });
}

function getLargestNumberByMax(numbersArray) {
  return Math.max(...numbersArray);
}

getLargestNumberBySort([]); // undefined
getLargestNumberByFor([]); //  undefined
getLargestNumberByReduce([]); // ERRO: Reduce of empty array with no initial value
getLargestNumberByMax([]); // -Infinity

getLargestNumberBySort(["string", 4, 6]); // 6
getLargestNumberByFor(["string", 4, 6]); // string
getLargestNumberByReduce(["string", 4, 6]); // string
getLargestNumberByMax(["string", 4, 6]); // NaN
```

