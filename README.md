# Javascript Básico para Programadores
##### Por [pedrohdjs](https://www.github.com/pedrohdjs)
Nesse pequeno texto, faço uma breve introdução à linguagem Javascript tendo como alvo quem já programou em outras linguagens
Todo o conteúdo aqui foi baseado em experiência prévia e na [documentação do MDN](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript).
O repositório está sempre aberto para novas pull requests com correções e conteúdo adicional!

## Tabela de Conteúdos
  * [O que o Javascript faz?](#o-que-o-javascript-faz-)
  * [Como executar Javascript](#como-executar-javascript)
  * [Variáveis](#vari-veis)
    + [Tipos de dados](#tipos-de-dados)
    + [Tipos de declarações](#tipos-de-declara--es)
  * [Comparações](#compara--es)
  * [Outros operadores](#outros-operadores)
  * [Estruturas de decisão](#estruturas-de-decis-o)
  * [Estruturas de repetição](#estruturas-de-repeti--o)
  * [Arrays](#arrays)
  * [Funções](#fun--es)
    + [Declarações típicas](#declara--es-t-picas)
    + [Arrow functions](#arrow-functions)
    + [Funções são variáveis como quaisquer outras](#fun--es-s-o-vari-veis-como-quaisquer-outras)
    + [Funções anônimas](#fun--es-an-nimas)
  * [Chamadas assíncronas](#chamadas-ass-ncronas)
    + [Promises](#promises)
    + [Funções assíncronas](#fun--es-ass-ncronas)
    + [Callbacks](#callbacks)
  * [Mais sobre objetos](#mais-sobre-objetos)
    + [Objetos globais](#objetos-globais)
    + [Desestruturação (destructuring)](#desestrutura--o--destructuring-)
    + [Desestruturação de objetos](#desestrutura--o-de-objetos)
    + [Desestruturação de arrays](#desestrutura--o-de-arrays)
    + [Desestruturação renomeando](#desestrutura--o-renomeando)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## O que o Javascript faz?
- A princípio...
  - Todo o carregamento dinâmico em páginas web (modificar o HTML de uma página durante o acesso)
- Com o Node.js...
  - Frontends implementados através de frameworks (como React, Angular e Vue.js)
  - Backend
  - Aplicações mobile (!!!!!!!) com o React Native
- Basicamente, dá pra fazer quase tudo com Javascript!

## Como executar Javascript
- Incluindo código javascript em arquivos HTML através da tag **script**
- Executando localmente com o node.js 
    ```node meuarquivo.js```
- Ambientes de execução online (recomendo usar [esse aqui](https://playcode.io/new/) pra dar a primeira brincada com o Javascript)

## Variáveis
Javascript é uma linguagem **dinamicamente tipada**, sem necessidade de declarar explicitamente os tipos das variáveis. 
### Tipos de dados
Dentre os tipos de dados existentes, temos:
- **Number**: Um número (seja ele int ou float)
    ```javascript
    let meuNumero = 5;
    let meuNumero2 = 15.754
    ```
- **String**: Uma sequência de caracteres (não existe char)
    ```javascript
    let minhaString = "Olá, mundo!"; //Válido
    let minhaString2 = 'Olá, mundo'; //Também válido!
    ```
- **Boolean**: true ou false
    ```javascript
    let oCodelabEhPerfeito = true;

    //Você pode também atribuir expressões a booleanos!
    let cincoEhMenorQueDois = 5 < 2 //false 
    ```
- **undefined**: Uma variável que não foi inicializada
    ```javascript
    let variavel; //Até que seja atribuido um valor, variavel é undefined
    variavel = 2; //Agora variavel é Number
    variavel = "batata";//Agora variavel é String
    //variáveis podem receber valores de qualquer tipo! (O que não significa que deveriam)
    ```
- **null**: Só null mesmo, padrão
    ```javascript
    let nadaPraVerAqui = null;
    ```
- **Object**: Um objeto, que armazena pares chave-valor de dados. Alguns objetos, como os Arrays, podem armazenar funções que alteram seus próprios valores (ver [Arrays](#Arrays) para exemplos)
    ```javascript
    let meuObjeto = {chave1: 1, chave2: "valor da chave 2"};
    meuObjeto.chave1; //Retorna o valor 1
    meuObjeto["chave2"]; //Retorna o valor "valor da chave 2";

    //Objetos no Javascript tem a estrutura flexível, diferente de uma struct em C.
    meuObjeto.batataEhBom = true; //Atribui true a batataEhBom no objeto.
    meuObjeto.batataEhBom; //Retorna o valor true

    //Variáveis podem ser inicializadas como objetos vazios
    let objeto2 = {};
    objeto2.chave = "valor";
    ```
    Objetos do Javascript são representados em JSON (Javascript Object Notation), e JSON é um formato de dado usado até mesmo fora do Javascript devido a simplicidade do modelo.

### Tipos de declarações
Existem 3 tipos de declarações de variáveis em javascript:

- **let**: Variável com escopo local
- **var**: Variável com escopo global
    ```javascript
    if(true){
        var chegouNoIf = 5;
    }
    else if (false){
        var naoChegouNoIf = 10;
    }
    else{
        let issoNemExiste = 15;
    }

    //chegouNoIf existe e tem valor 5
    chegouNoIf;

    /*naoChegouNoIf existe mas é undefined, dado que o valor 10 não foi 
    atribuído a ela como o if não chegou na atribuição*/
    naoChegouNoIf; 

    //issoNemExiste não existe aqui pois tem apenas escopo local dentro do else.
    issoNemExiste;
    ```
- **const**: Constante com o mesmo escopo do let. A variável não pode ser reatribuída, mas, **chaves de objetos declarados com const podem ser modificadas**
    ```javascript
    const valorConstante = 5;
    valorConstante = 3; //Erro!

    const objetoConstante = {valor1: true};
    objetoConstante.valor1 = 5; //Nenhum erro aqui
    ```

## Comparações
As comparações podem ser feitas com os operadores típicos (==, >, <, !=, >= e <=).
Mas, as comparações feitas com == e != são flexíveis. Veja no exemplo:
```javascript
    if (55 == "55"){
        console.log("Sim, é igual"); //Essa linha será executada, imprimindo "Sim, é igual" no console.
}
```
Muitas vezes, isso pode ser um problema, por permitir que comparações de variáveis de tipos diferentes seja feita, portanto, o uso dos operadores == e != não é recomendado.
Ao invés disso, **use os operadores === e !==, que comparam conteúdo e tipo das variáveis.**
```javascript
    if (55 === "55!){
        console.log("Sim, é igual"); //Essa linha não será executada dessa vez
}
```

## Outros operadores
Javascript suporta também os operadores +, -, *, /, ++, --, +=, -=, *= e /=.

## Estruturas de decisão
Javascript oferece suporte às estruturas típicas if, else, else if e switch case.

## Estruturas de repetição
Javascript oferece suporte às estruturas típicas for, while, do while, break e continue.
Há também as estruturas for in, para iterar sobre as chaves de um objeto, e for of, para iterar sobre os valores de um Array.
```javascript
let meuObjeto = {chave1: "valor1", chave2: "valor2", chave3: "valor3"};
for (let chave in meuObjeto){
    console.log(chave); //Imprime chave1, chave2 e chave3
}

let meuArray = [3,5,7];
for (let valor of meuArray){
    console.log(valor); //Imprime 3, 5 e 7
}
```
E, falando em arrays...

## Arrays
Arrays em javascript nada mais são que um tipo de objeto. A diferença é que as chaves de um array são definidas automaticamente em ordem incremental (0, 1, 2, e assim em diante).
Arrays podem ser inicializados com [] e contém alguns métodos que podem inserir ou remover valores, simulando estruturas de dados como pilhas e filas conforme for necessário.
```javascript
let meuArray = []; //Arrays também podem ser inicializados vazios

//A função Array.push(valor) insere o valor no fim do array.
meuArray.push(1); //[1] 
meuArray.push(2); //[1,2] 
meuArray.push(3); //[1,2,3] 

//A função Array.pop() remove o último elemento do array e retorna seu valor
let ultimoElemento = meuArray.pop(); //[1,2]
console.log(ultimoElemento); //Imprime 3

//A função Array.unshift(valor) insere um valor no início do array
meuArray.unshift(4); //[4,1,2]

//A função Array.shift() remove o primeiro elemento do array
meuArray.shift(); //[1,2]
```

## Funções
As funções em Javascript podem ser declaradas de duas maneiras:
### Declarações típicas 
Funções podem ser declaradas normalmente através da palavra-chave **function**:
```javascript
    function logStuff (nome) {
        console.log("Hello, " + nome + "!");
    }
    logStuff("Tapete"); //Imprime "Hello, Tapete!"
```
    

### Arrow functions
Funções também podem ser declaradas atribuindo seus valores a variáveis conforme a seguinte sintaxe:
```javascript
    let soma = (a,b) => {
        return a + b;
    }
    console.log(soma(3,4)); //Imprime 7.
```
Para arrow functions de uma linha, pode ser usada a seguinte sintaxe:
```javascript
    let soma = (a,b) => a + b; //Exatamente a mesma função do exemplo anterior
```
Arrow functions com apenas um argumento podem ser representadas sem parênteses no argumento:
```javascript
    let soma2 = a => a + 2; //Retorna o valor passado + 2
    console.log(soma2(10)); //Imprime 12
```
### Funções são variáveis como quaisquer outras
Independente do tipo de declaração utilizado, a função será tratada como uma variável, podendo ter seu valor sobreescrito (prática não recomendada) ou mesmo sendo passadas como argumentos de outras funções, conforme o exemplo:
```javascript
    //Função que retorna true se o número for par ou false se o número for ímpar
    function ehPar (valor){
        return valor%2 === 0;
    }

    /*Função que recebe um array e uma função como argumentos, e imprime no console 
    apenas os valores para os quais a função teste recebida retorna true*/
    function imprimirFiltrado(arr,teste){
        for(let value of arr){
            if(teste(value)){
                console.log(value);
            }
        }
    }

    const myArr = [1,2,3,4];
    imprimirFiltrado(myArr,ehPar); //Imprime 2 e 4
    
    //Função que retorna true se o número for ímpar
    function ehImpar (valor){
        return valor%2 === 1;
    }

    imprimirFiltrado(myArr,ehImpar); //Imprime 1 e 3
```

### Funções anônimas
Em alguns casos, queremos usar funções apenas como argumento para alguma outra função, sem necessidade de repetir seu uso. Nesses casos, podemos utilizar funções anônimas, como nesse exemplo, que reimplementa o exemplo anterior:
```javascript
    function imprimirFiltrado(arr,teste){
        for(let value of arr){
            if(teste(value)){
                console.log(value);
            }
        }
    }

    const myArr = [1,2,3,4];
    imprimirFiltrado(myArr, val => val%2 === 0); //Imprime 2 e 4
    imprimirFiltrado(myArr, function(val) {
        return val%2 === 1;
    }); //Imprime 1 e 3
```
Como podemos ver, funções anônimas podem ser declaradas com qualquer sintaxe de funções!

## Chamadas assíncronas
No javascript, algumas chamadas feitas são assíncronas e retornam Promises.
Esse conceito pode ser bastante abstrato, mas, basicamente, o que acontece:
```javascript
    //funcaoAssincrona retorna alguma Promise com um JSON
    const resultado = funcaoAssincrona();
    console.log(resultado); //undefined
```

Isso acontece porque chamadas assíncronas rodam em paralelo com o resto do código. Sendo assim, o código avança para a próxima linha antes da função assíncrona acabar de ser executada.
Normalmente, funções que demoram mais tempo, como chamadas a uma API, são assíncronas. 

### Promises
Funções assíncronas retornam objetos especiais do tipo Promise. Não há necessidade de compreender completamente o conceito de Promise nesse momento, mas, basicamente, uma **Promise é um objeto que vai passar a conter a resposta assim que a execução do código assíncrono nela for finalizada**. A Promise não contém a resposta logo no momento em que é instanciada, devemos aguardar sua **resolução**, quando tudo ocorre como esperado ou **rejeição**, que é quando algo dá errado.


### Funções assíncronas

Há vários jeitos de lidar com Promises, mas, o jeito de fazer isso que te permite ter um código mais limpo é declarar uma função assíncrona.
Funções assíncronas são declaradas com a palavra-chave **async** antes de function e permitem o uso do comando **await** em seu corpo, conforme esse exemplo, reimplementando o exemplo anterior de maneira adequada:
```javascript
    async function fazerCoisas(){
        /*O await faz com que a função não saia dessa linha até que a promise 
        retornada por funcaoAssincrona seja resolvida.*/
        const resultado = await funcaoAssincrona();

        //Não precisa de await, pois console.log é uma função síncrona
        console.log(resultado); 
    }
    fazerCoisas();
```
Note que como fazerCoisas() é uma função assíncrona, se tivessemos algum uso para o valor que essa função retorna, precisaríamos de outra função com async/await.

### Callbacks
Outro jeito comum de se lidar com chamadas assíncronas são os callbacks. Callbacks são funções que recebem como valor o conteúdo retornado pela função que chama o Callback e usam esse valor para algo. 
No caso das Promises, temos o método Promise.then(resolve,reject), que recebe a função resolve, que é executada se a promise funcionar corretamente e a função reject, que é chamada se occorer algum erro durante a execução da primeira função.
```javascript
    //funcaoAssincrona continua retornando uma Promise com um JSON
    const promiseCaputrada = funcaoAssincrona();
    promiseCapturada.then((res) => {
        console.log(res);
    }, (err) => {
        console.log("Deu ruim!!!!");
        console.log(err);
    })
```
Para implementar seus próprios callbacks em funções async, basta que as funções recebam um parâmetro que seja uma função e então executem esse parâmetro-função, conforme o exemplo:
```javascript
    const fazerCoisas = async (callback) => {
        const res = await algumaFuncaoAssincrona();
        callback(res);
    }
```

## Mais sobre objetos
### Objetos globais
No Javascript, alguns objetos estão sempre presentes, sem a necessidade de serem instanciados. A exemplo disso, temos o objeto **document**, que é permite a manipulação do HTML de uma página, o objeto **console** que nos possibilita imprimir coisas no console e o objeto **Math**, que nos dá uma série de funções utilitárias matemáticas. Para utilizar um desses objetos, basta os invocar como se já tivessem sido declarados.
```javascript
    console.log(Math.sqrt(16)); //Imprime 4
```
### Desestruturação (destructuring)
### Desestruturação de objetos
As vezes, temos um objeto muito grande e precisamos extrair apenas algumas propriedades dele. Nessas horas, podemos utilizar a declaração através de desestruturação de objetos, conforme o exemplo:
```javascript
    const myObject = {
        pi: 3.1415,
        phi: 1.618,
        sqrt2: 1.41
    }

    /*Declara as variáveis pi e sqrt2 conforme os valores dessas chaves em myObject*/

    let {pi, sqrt2} = myObject; 
    console.log(pi); // imprime 3.1415
    console.log(sqrt2); // imprime 1.618
    console.log(phi); //dá erro, pois phi não foi definido
```
### Desestruturação de arrays
Também podemos desestruturar arrays para obter alguns de seus valores. 
```javascript
    const myArray = [5,4,3,2,1];
    let [primeiroValor, segundoValor] = myArray;
    console.log(primeiroValor); //Imprime 5
    console.log(segundoValor); //Imprime 4

```
Na desestruturação de Arrays também podemos ignorar valores não desejados.
```javascript
    const myArray = [5,4,3,2,1];
    let [primeiroValor, , terceiroValor] = myArray;
    console.log(primeiroValor); //Imprime 5
    console.log(terceiroValor); //Imprime 3
```
### Desestruturação renomeando
Em ambas as desestruturações, podemos também declarar variáveis com novos nomes extraindo campos do objeto
```javascript
    const myObject = {
        pi: 3.1415,
        phi: 1.618,
        sqrt2: 1.41
    }

    //Extrai o valor de myObject.pi na variável valorDePi
    let {pi: valorDePi} = myObject; 
    console.log(valorDePi); //3.1415
    console.log(pi); //Erro, pois pi não foi declarado
```
