toggleHiddenAside
-----------------

Descrição

A função `toggleHiddenAside` é responsável por adicionar e remover classes de animação em um elemento, a fim de mostrar ou esconder o mesmo. É possível definir classes personalizadas para as animações de entrada e saída do elemento.

Este é um código em JavaScript que define uma função chamada `toggleHiddenAside()`. Essa função recebe um objeto como parâmetro com quatro propriedades: `elementSelector`, `showClass`, `hiddenClass` e `animeEndCallback`.

A propriedade `elementSelector` é uma string que representa um seletor CSS usado para encontrar o elemento que será manipulado pela função. A propriedade `showClass` é uma string que representa a classe CSS usada para mostrar o elemento. A propriedade `hiddenClass` é uma string que representa a classe CSS usada para esconder o elemento. A propriedade `animeEndCallback` é uma string que representa a classe CSS usada para animar o elemento.

A função começa limpando o console e imprimindo uma mensagem indicando que a função foi chamada. Em seguida, ela busca o elemento usando o seletor especificado e imprime-o no console.

Se o elemento não tiver a classe `showClass` ou a classe `animeEndCallback`, a função adiciona a classe `showClass` ao elemento.

A função adiciona um ouvinte de eventos para detectar quando a animação da classe `showClass` terminou. Quando isso acontece, a função adiciona a classe `animeEndCallback` ao elemento e adiciona outro ouvinte de eventos para detectar quando a animação da classe `animeEndCallback` terminou.

Se o elemento tiver a classe `animeEndCallback` e não tiver nenhuma das classes `showClass` ou `hiddenClass`, a função adiciona a classe `hiddenClass` ao elemento. Em seguida, adiciona outro ouvinte de eventos para detectar quando a animação da classe `hiddenClass` terminou e remove as classes `hiddenClass` e `animeEndCallback` do elemento.

Se o elemento tiver a classe `animeEndCallback` e não tiver nenhuma das classes `showClass` ou `hiddenClass`, a função adiciona a classe `hiddenClass` ao elemento. Em seguida, adiciona outro ouvinte de eventos para detectar quando a animação da classe `hiddenClass` terminou e remove as classes `hiddenClass` e `animeEndCallback` do elemento.

O código também define um botão com a classe `btnShowAside` e adiciona um ouvinte de eventos para detectar quando o botão é clicado. Quando o botão é clicado, a função `toggleHiddenAside()` é chamada com os parâmetros especificados no objeto passado para ela.


### **Parâmetros**

*   `elementSelector` (string): Seletor CSS do elemento que será mostrado ou escondido.
*   `showClass` (string): Nome da classe CSS que será adicionada ao elemento para exibi-lo.
*   `hiddenClass` (string): Nome da classe CSS que será adicionada ao elemento para escondê-lo.
*   `animeEndCallback` (string): Nome da classe CSS que será adicionada ao elemento ao final da animação.

### **Fundamentos**

A função `toggleHiddenAside` utiliza as seguintes propriedades do objeto `classList` do elemento selecionado:

*   `classList.contains(className)`: Verifica se o elemento possui a classe `className`.
*   `classList.add(className)`: Adiciona a classe `className` ao elemento.
*   `classList.remove(className)`: Remove a classe `className` do elemento.

Além disso, a função utiliza o evento `animationend` para detectar o final da animação e executar a remoção das classes.

### **Exemplo de como usar**

javascript

```javascript
const myButton = document.querySelector('.btnShowAside');
myButton.addEventListener('click', () => {
    toggleHiddenAside({
        elementSelector: 'aside',
        showClass: 'slideInLeft',
        hiddenClass: 'slideInRight',
        animeEndCallback: 'shake',
    })
});
```

Neste exemplo, a função `toggleHiddenAside` é chamada quando o botão `.btnShowAside` é clicado. O elemento `aside` será exibido com a animação `slideInLeft`, e ocultado com a animação `slideInRight`. Após a animação de saída, a classe `shake` será adicionada ao elemento.

### ***Explicações adicionais***

*   `once: true`: Opção do método `addEventListener` que faz com que o evento seja ouvido apenas uma vez.
*   `!ANIMATION_CLASSES.some`: O operador `!` nega o resultado da função `some`, que retorna `true` se pelo menos um dos elementos do array `ANIMATION_CLASSES` for encontrado na lista de classes do elemento. Isso significa que o bloco de código dentro do `if` só será executado se a classe `animeEndCallback` estiver presente no elemento e nenhuma das classes de animação estiver presente.
*   `c => myAside.classList.contains(c)`: Esta é uma função de callback passada para a função `some` do array `ANIMATION_CLASSES`. A função `some` verifica se pelo menos um elemento do array atende a condição estabelecida na função de callback. Neste caso, a função verifica se o elemento `c` está presente na lista de classes do elemento `myAside`.


### **Algumas melhorias que podem ser feitas no código são:**

1.  Refatoração da função para melhor legibilidade e manutenção.
2.  Verificação da existência do elemento antes de tentar acessá-lo.
3.  Utilização de constantes ou variáveis ​​para os valores das classes CSS, para evitar a repetição de código.
4.  Melhorar o nome das classes CSS para deixar mais claro o que cada uma representa.
5.  Adicionar comentários ao código para explicar as partes mais complexas.
6.  Utilização de uma biblioteca de animação, como a GSAP, para simplificar a animação.
7.  Adicionar opções de configuração adicionais, como duração e direção da animação.
8.  Implementar testes unitários para garantir o bom funcionamento da função em diferentes cenários.
9.  Adicionar suporte para navegadores mais antigos ou desatualizados, utilizando polyfills ou fallbacks adequados.
10.  Adicionar suporte para elementos criado do forma dinâmica, isto é, após o carregamento do DOM.

### **Código completo**
javascript
```JS
/**  
  @fn001
  @func toggleHiddenAside()
  @Descrição Função que alterna a visibilidade de um elemento com animação CSS.
*/

function toggleHiddenAside({elementSelector, showClass, hiddenClass, animeEndCallback}) {
    console.clear();
    console.trace("A função toggleHiddenAside() foi chamada.");

    const myAside = document.querySelector(elementSelector);
    console.log(myAside);

    if (!myAside.classList.contains(showClass) && !myAside.classList.contains(animeEndCallback)) {
        myAside.classList.add(showClass);
    }

    myAside.addEventListener('animationend', () => {
        console.log(`A animação da classe --${showClass} terminou.`);

        myAside.classList.add(animeEndCallback);
        console.log(`A animação da classe --${animeEndCallback} foi adicionada.`);

        myAside.addEventListener('animationend', () => {
            console.log(`A animação da classe --${animeEndCallback} terminou.`);


            myAside.classList.remove(showClass);

        }, {
            once: true
        });
    }, {
        once: true
    });
    const ANIMATION_CLASSES = [showClass, hiddenClass];
    if (myAside.classList.contains(animeEndCallback) && !ANIMATION_CLASSES.some(c => myAside.classList.contains(c))){
        myAside.classList.add(hiddenClass);

        myAside.addEventListener('animationend', () => {
            console.log(`A animação da classe --${hiddenClass} terminou.`);
            myAside.classList.remove(hiddenClass);
            myAside.classList.remove(animeEndCallback);
            
        }, {
            once: true
        });
    }
    if (myAside.classList.contains(animeEndCallback) && !ANIMATION_CLASSES.some(c => myAside.classList.contains(c))) {
        myAside.classList.add(hiddenClass);
        console.log('A class foi adicionada slideInRight');

        myAside.addEventListener('animationend', () => {
            console.log(`A animação da classe --${hiddenClass} terminou.`);

            myAside.classList.remove(hiddenClass, animeEndCallback);
            console.log('As classes slideInRight e shake estão removidas');

        }, {
            once: true
        });
    }
}

```

slideInLeft
```SCSS
.slideInLeft {
    -webkit-animation-name: slideInLeft;
    animation-name: slideInLeft;
    -webkit-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;

    @-webkit-keyframes slideInLeft {
        0% {
            -webkit-transform: translateX(-100%);
            transform: translateX(-100%);
            visibility: visible;
        }

        100% {
            -webkit-transform: translateX(0);
            transform: translateX(0);
        }
    }

    @keyframes slideInLeft {
        0% {
            -webkit-transform: translateX(-100%);
            transform: translateX(-100%);
            visibility: visible;
        }

        100% {
            -webkit-transform: translateX(0);
            transform: translateX(0);
        }
    }


}
```

shake
```SCSS
.shake {
    animation-name: shake;
    animation-duration: 0.3s;
    animation-fill-mode: both;
    animation-timing-function: cubic-bezier(0.36, 0.07, 0.19, 0.97);


    @keyframes shake {
        0% {
            transform: translateX(0);
        }

        25% {
            transform: translateX(-10px);
        }

        50% {
            transform: translateX(10px);
        }

        75% {
            transform: translateX(-10px);
        }

        100% {
            transform: translateX(0);
        }
    }
}
```
slideInRight
```SCSS 

.slideInRight {
    -webkit-animation-name: slideInRight;
    animation-name: slideInRight;
    -webkit-animation-duration: 1s;
    animation-duration: 1s;
    -webkit-animation-fill-mode: both;
    animation-fill-mode: both;

    @-webkit-keyframes slideInRight {
        0% {
            -webkit-transform: translateX(0);
            transform: translateX(0);
            visibility: visible;
        }

        100% {
            -webkit-transform: translateX(-101%);
            transform: translateX(-101%);
        }
    }

    @keyframes slideInRight {
        0% {
            -webkit-transform: translateX(0);
            transform: translateX(0);
            visibility: visible;
        }

        100% {
            -webkit-transform: translateX(-101%);
            transform: translateX(-101%);
        }
    }
}
```

Considerações Finais
-----

Estado inicial da aside (scss)
```SCSS

aside {
    min-width: 250px;
    height: 100%;
    position: absolute;
    // add animação
    transform: translateX(-101%);
    transition: transform 0.3s ease-in-out;
}
```

    Não configura para elementos criado dinâmicamente (após carregamento do DOM)




