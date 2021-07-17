# 🧙‍♂️ JavaScript Dicas/Truques Para Codar Como Herói 🦸‍♂️

### 1. Gerar números dentro de um intervalo.

Existem algumas situações que precisamos criar um array com intervalo de números. Por exemplo, pegar todos os anos dentro de um range de valores. Esta é a maneira mais fácil de implementá-lo.

```js
let inicio = 1900,
    fim = 2000;
[...new Array(fim + 1).keys()].slice(inicio);
// [ 1900, 1901, ..., 2000]

// Essa outra forma também funciona, porém pode gerar resultados inesperados em ranges muito grandes.
Array.from({ length: fim - inicio + 1 }, (_, i) => inicio + i);
```

### 2. Use array de valores como argumentos para funções

Tem casos em que você precisa coletar os valores em array(s) e, em seguida, passá-los como argumentos para a função. Com ES6 você pode apenas usar spread operator (...) e extrair seu array de `[arg1, arg2] > (arg1, arg2)`

```js
const partes = {
  primeira: [0, 2],
  segunda: [1, 3],
};

["Olá", "Mundo", "JS", "Truques"].slice(...partes.segunda);
// ["Mundo", "JS", "Truques"]
```

_Pode ser usado com qualquer função_


### 3. Use valores como argumentos com método Math
Então, somos bons em espalhar valores para colocá-los em funções. Porém quando precisamos encontrar Math.max ou Math.min de nossos números no array, fazemos da seguinte maneira.

```js
// Encontrar a posição y do elemento mais alto: 474px
const elementos =  [...document.body.children].map(
  el => el.getBoundingClientRect().y
);
Math.max(...elementos);
// 474

const numeros = [100, 100, -1000, 2000, -3000, 40000];
Math.min(...numeros);
// -3000
```

### 4. Mesclando arrays em arrays
Existe um bom método para Array chamado `Array.flat`, como um argumento ele precisa de profundidade que você deseja para nivelar. Mas e se você não souber a profundidade que precisa nivelar. Apenas coloque `Infinity` como argumento. Também há: [flatMap](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/flatMap) method.

```js
const arrays = [[10], 50, [100, [2000, 3000, [40000]]]];
arrays.flat(Infinity);
// [ 10, 50, 100, 2000, 3000, 40000 ]
```

### 5. Prevenir falhas do seu código
Não é bom ter um comportamento imprevisível em seu código, mas se tiver, você precisa lidar com isso.

Por exemplo. Um Erro comum `TypeError`, se você está tentando obter a propriedade de undefined/null e etc.

Observação: Use-o se o seu projeto não suportar [optional chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining?fbclid=IwAR2_X1H9hAPhmChM5ACKNrYHMWb-vA0G7KOmakCmhURzjl5Biy4ta8_bQrM)

```js
const encontrar = [{ nome: "Frank" }].find(i => i.nome === 'Alex');
console.log(encontrar.nome);
// TypeError: Cannot read property 'nome' of undefined
```

Você pode evitar assim
```js
const encontrar = [{ nome: "Frank" }].find(i => i.nome === 'Alex') || {};
console.log(encontrar.nome);
// undefined
```

Claro que depende das situações, mas para lidar com coisas menores está tudo bem. Você não precisa escrever um código enorme para lidar com isso.

### 6. Boa maneira de passar argumentos
Um bom exemplo de uso desse recurso são os `styled-components`, no ES6 você pode passar **Template literals** como argumento para função sem colchetes. Bom truque se você estiver implementando uma função que formate/converta seu texto.

```js
const fazerLista = (lista) =>
  lista
    .join()
    .trim()
    .split("\n")
    .map((s, i) => `${i + 1}. ${s}`)
    .join("\n");

fazerLista`
Ola, Mundo
Ola, Mundo
`;
// 1. Ola
// 2. Mundo
```

### 7. Troque variáveis como um Herói
Com a sintaxe de desestruturação, podemos facilmente trocar as variáveis.

```js
let a = "olá";
let b = "mundo";

// Errado
a = b
b = a
// { a: 'mundo', b: 'mundo' }

// Correto
[a, b] = [b, a];
// { a: 'mundo', b: 'olá' }
```
Uma solução que errada, seria colocar uma terceira variável temporária :(

### 8. Classificar por ordem alfabética
Trabalhei muito em empresas internacionais e seus aplicativos continham dados em outros idiomas. Quando você faz seus truques ** "incríveis" ** para classificar a lista desse tipo de dados, parece normal, às vezes porque há apenas algumas strings para aquele momento. Talvez pareça normal porque você não conhece o alfabeto desse idioma.
Use o correto para ter certeza de que ele está classificado em ordem alfabética para aquele idioma.

Por exemplo. Alfabeto Português Brasileiro
```js
// Errado
["a", "z", "d"].sort((a, b) => a - b);
// ['a', 'z', 'd']

// Correto
["a", "z", "d"].sort((a, b) => a.localeCompare(b));
// [ 'a', 'd', 'z' ]
```

### 9. Mascare bem
Um ótimo truque sobre máscaras, para quando você precisar mascarar qualquer variável. Não é uma senha, é claro :) é apenas um exemplo. Nós apenas pegamos parte da string `substr (-3)`, 3 caracteres de seu final e preenchemos o comprimento que saiu com qualquer símbolo (exemplo `*`)

```js
const senha = "secreta";
senha.substr(-3).padStart(senha.length, "*");
// ****eta
// Hmmm, acho que suas primeiras tentativas podem estar erradas
```

### 10. Gerar lista com números aleatórios

Podemos precisar disto para gerar números fakes, por inúmeras razões.

```jsx
Array.from({ length: 1000 }, Math.random)
// [ 0.6163093133259432, 0.8877401276499153, 0.4094354756035987, ...] - 1000 itens
```

### Conclusão

Busque entender como as coisas funcionam e mantenha o seu código limpo e bonito ❤️

