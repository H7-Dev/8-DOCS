Documentação do código JavaScript da func `hiddenElementClickOut`
=========================================================


Este código é uma função em JavaScript chamada `hiddenElementClickOut` que adiciona um manipulador de eventos 'click' à tela e executa uma determinada ação quando o usuário clica fora de um elemento específico.

A função recebe um objeto com os seguintes parâmetros:

*   `mainElement`: o elemento principal que a função está monitorando para cliques fora dele;
*   `mediaQuery`: uma expressão de mídia que verifica se a largura da tela é menor ou igual a 768 pixels;
*   `elementClasses`: uma matriz de classes de elementos a serem ignorados ao clicar fora do `mainElement`;
*   `xClass`: a classe CSS adicionada ao `mainElement` quando ele é exibido;
*   `classEffectOut`: a classe CSS que é adicionada ao `mainElement` quando ele é removido.

A função verifica se o elemento clicado está fora do `mainElement` e não está em uma das classes listadas em `elementClasses`. Se for o caso, a classe `classEffectOut` é adicionada ao `mainElement`, que executa uma animação, e a classe `xClass` é removida após a animação terminar.

A função também registra algumas informações no console, como uma mensagem quando o usuário clica fora do `mainElement`.

No final do código, a função é chamada e passa alguns argumentos, incluindo o `mainElement`, uma expressão de mídia, uma matriz de classes de elementos a serem ignorados e classes CSS para serem adicionadas ou removidas quando a ação é executada.


Esta é uma função em JavaScript que adiciona um manipulador de eventos 'click' à tela e executa uma determinada ação quando o usuário clica fora de um elemento específico.

Instalação
----------

O código já está escrito e pode ser incorporado em um arquivo `.js` em seu projeto. Certifique-se de incluir o código em seu arquivo HTML.

Como usar
---------

A função `hiddenElementClickOut` é chamada passando um objeto com os seguintes parâmetros:

*   `mainElement`: (obrigatório) o elemento principal que a função está monitorando para cliques fora dele;
*   `mediaQuery`: (obrigatório) uma expressão de mídia que verifica se a largura da tela é menor ou igual a 768 pixels;
*   `elementClasses`: (opcional) uma matriz de classes de elementos a serem ignorados ao clicar fora do `mainElement`;
*   `xClass`: (opcional) a classe CSS adicionada ao `mainElement` quando ele é exibido;
*   `classEffectOut`: (opcional) a classe CSS que é adicionada ao `mainElement` quando ele é removido.

javascript

```javascript
hiddenElementClickOut({
  mainElement: asideMain,
  mediaQuery: mediaQuery,
  elementClasses: ['clickOutIgnore'],
  xClass: 'shake',
  classEffectOut:'slideInRight'
});
```

### mainElement

O parâmetro `mainElement` é um elemento DOM que representa o elemento principal que a função está monitorando para cliques fora dele. Este parâmetro é obrigatório para o correto funcionamento da função.

javascript

```javascript
const asideMain = document.querySelector('aside.main')
```

### mediaQuery

O parâmetro `mediaQuery` é uma expressão de mídia que verifica se a largura da tela é menor ou igual a 768 pixels. Este parâmetro é obrigatório para o correto funcionamento da função.

javascript

```javascript
const mediaQuery = window.matchMedia('(max-width: 768px)');
```

### elementClasses

O parâmetro `elementClasses` é uma matriz de classes de elementos a serem ignorados ao clicar fora do `mainElement`. Este parâmetro é opcional e pode ser omitido se não houver classes a serem ignoradas.

javascript

```javascript
elementClasses: ['clickOutIgnore'],
```

### xClass

O parâmetro `xClass` é a classe CSS adicionada ao `mainElement` quando ele é exibido. Este parâmetro é opcional e pode ser omitido se não houver classes CSS a serem adicionadas.

javascript

```javascript
xClass: 'shake',
```

### classEffectOut

O parâmetro `classEffectOut` é a classe CSS que é adicionada ao `mainElement` quando ele é removido. Este parâmetro é opcional e pode ser omitido se não houver classes CSS a serem adicionadas.

javascript

```javascript
classEffectOut:'slideInRight'
```

Funcionamento
-------------

A função `hiddenElementClickOut` adiciona um manipulador de eventos 'click' à tela e executa uma determinada ação quando o usuário clica fora de um elemento específico.

A função verifica se o elemento clicado está fora do `mainElement` e não está em uma das classes listadas em `elementClasses`. Se for o caso, a classe `classEffectOut` é adicionada ao `mainElement`, que executa uma animação, e a classe `xClass` é removida após a

### ***Explicações adicionais***

***A tabela abaixo tem alguns explicações adicionais do método e ou recursos usado:***

| Método | Descrição |
| --- | --- |
| `animationend` | É um evento que é acionado quando uma animação CSS termina. Ele é adicionado ao elemento principal usando `mainElement.addEventListener('animationend', callbackFunction, { once: true })` para remover a classe `xClass` após a conclusão da animação `classEffectOut`. |
| `once` | É uma opção de configuração para o método `addEventListener()` que indica que o ouvinte de eventos deve ser acionado somente uma vez e depois removido automaticamente. É usado junto com o `animationend` neste código para remover a classe `xClass` após a conclusão da animação `classEffectOut`. |
| `event.target` | É uma propriedade do objeto `event` que representa o elemento que disparou o evento. Neste código, é usado para verificar se o elemento clicado não é o elemento principal nem um dos elementos a serem ignorados. |
| `classList.contains()` | É um método que verifica se uma classe específica existe na lista de classes de um elemento. É usado neste código para verificar se o elemento principal tem a classe `xClass`. |
| `element.closest()` | É um método que retorna o ancestral mais próximo que corresponde a um seletor CSS especificado. É usado neste código para verificar se o elemento clicado não é um dos elementos a serem ignorados. |
| `classList.add()` | É um método que adiciona uma ou mais classes a um elemento. É usado neste código para adicionar a classe `classEffectOut` ao elemento principal. |
| `classList.remove()` | É um método que remove uma ou mais classes de um elemento. É usado neste código para remover as classes `xClass` e `classEffectOut` do elemento principal após a conclusão da animação `classEffectOut`. |
| `console.clear()` | É um método que limpa a saída do console. É usado neste código para limpar a saída do console antes de imprimir mensagens de depuração. |
| `console.trace()` | É um método que exibe uma pilha de chamadas de função que levou à chamada do método `console.trace()`. É usado neste código para imprimir a mensagem de depuração "A função hiddenElementClickOut() foi chamada." juntamente com a pilha de chamadas de função. |
| `document.addEventListener()` | É um método que adiciona um ouvinte de eventos ao documento. Neste código, é usado para adicionar um ouvinte de eventos 'click' à tela. |
| `window.matchMedia()` | É um método que retorna um objeto `MediaQueryList` que representa a consulta de mídia especificada. Neste código, é usado para criar uma consulta de mídia que corresponde a uma largura de tela máxima de 768 pixels. |