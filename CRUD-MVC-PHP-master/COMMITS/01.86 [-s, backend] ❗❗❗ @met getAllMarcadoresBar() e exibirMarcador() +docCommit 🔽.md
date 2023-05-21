### commit 01:85 [-s-backend] Obter registro de tabela e mostrar usando a tag pre (MODEL E CONTROLLER)

# **Como Obter registro de tabela e mostrar usando a tag pre no CONTROLLER a partir do MODEL**

Objetivo: Usando a estrutura MCV obter dados de uma tabela em base de dados Msql e popular um dropdown (uma tag select)

Estrutura das Pastas:

```TS
// CONTROLLER
CONTROLLER\atualizar_favorito.php
CONTROLLER\c.del.livro.php
CONTROLLER\c.edt.baralhos.php
CONTROLLER\c.inserir.baralho.php
CONTROLLER\c.listar.baralhos.php
=> CONTROLLER\c.listarAspecto.baralhos.php
CONTROLLER\ControllerEditar Part 1.md
CONTROLLER\ControllerEditar Part 2.md
CONTROLLER\processa.php
// MODEL
MODEL\JS
MODEL\SQL
MODEL\banco.php
MODEL\cadastroLivro.php
=> MODEL\dao.baralhos.php
MODEL\processa.php
// VIEW
VIEW\JS
VIEW\LIBS
VIEW\SCSS
VIEW\aside.html
VIEW\body.php
VIEW\breadcrumbs.php
VIEW\footer.php
VIEW\head.php
VIEW\index.php
VIEW\pag.frm.baralhos.html
VIEW\pag.frm.baralhos.php
VIEW\pag.home.html
VIEW\pag.home.php
VIEW\v.edt.baralhos.php
VIEW\v.inserir.baralho.php
VIEW\x.index.html
VIEW\x.php
init.php
```

Primeiro
=========

Devemos criar um método na class `baralhosDAO`, o método pode ter qualquer nome, neste caso, será chamado de `getAllMarcadoresBar`. A classe `baralhosDAO`, está no arquivo `dao.baralhos.php` dentro da pasta **MODEL**.

Veja o código:
```php
public function getAllMarcadoresBar() {
    $query = "SELECT * FROM tb_marca";
    $result = $this->mysqli->query($query);

    $result = $this->mysqli->query($query);
    if ($result->num_rows > 0) {
        $array = array();
        while($row = $result->fetch_array(MYSQLI_ASSOC)) {
            $array[] = $row;
        }
        return $array;
    } else {
        return array();
    }
}
```


O código é um método de uma classe em PHP. O objetivo desse método é recuperar todos os registros da tabela `"tb\_marca"` do banco de dados.
Aqui está uma descrição passo a passo do que o código faz:

1.  Executa a consulta SQL: `"SELECT \* FROM tb\_marca"` para selecionar todos os registros da tabela "tb\_marca".
2.  Armazena o resultado da consulta na variável `$result` usando o método `query()` do objeto `$this->mysqli`. Presumindo que `$this->mysqli` seja uma instância de uma classe que representa uma conexão com o banco de dados MySQLi.
3.  Verifica se o número de linhas retornadas pelo resultado da consulta (`$result`) é maior que zero usando a propriedade `num\_rows`. Isso verifica se há registros na tabela.
4.  Se houver registros, o código inicializa um array vazio chamado `$array` para armazenar os resultados.
5.  Em seguida, o código entra em um loop `while` para iterar sobre cada linha retornada pela consulta. O método `fetch\_array()` é usado para obter uma linha como uma matriz associativa (usando a constante `MYSQLI\_ASSOC`) e armazená-la no array `$array`.
6.  Depois que todas as linhas são percorridas, o array `$array` é retornado.
7.  Se não houver registros na tabela, o código retorna um array vazio.

Esse método pode faz parte de uma classe maior `(baralhosDAO)` que lida com operações relacionadas ao banco de dados. Ao chamar esse método, você receberá um array contendo todos os registros da tabela "tb\_marca".

Esse método estar localizado na pasta **MODEL**. Na ***estrutura MVC, o modelo (model)*** é responsável por lidar com a lógica de negócios e a interação com os dados.

A pasta **"model"** geralmente contém classes e métodos que lidam com a recuperação, manipulação e persistência dos dados. No exemplo, o método getAllMarcadoresBar() está na classe que representa o modelo relacionado à tabela "tb_marca".

Segundo
=======
Agora criamos um método na class `CrtlListarAspectosBaralhos`, o nome deste método será `exibirMarcador`. A class `CrtlListarAspectosBaralhos` esté no arquivo `c.listarAspecto.baralhos.php` na pasta **CONTROLLER.**


Veja o código:
```php
<?php
require_once("../MODEL/dao.baralhos.php");
class CrtlListarAspectosBaralhos{
    private $livrosDAO;
    public function __construct(){
        $this->livrosDAO = new baralhosDAO();
    }
    public function exibirMarcador(){
        $resultado = $this->livrosDAO->getAllMarcadoresBar();

        if (!empty($resultado)) {
            echo '<pre>';
            print_r($resultado);
            echo '</pre>';
        } else {
            echo 'Nenhum registro encontrado.';
        }
    }
}
// Instancie a classe CrtlListarAspectosBaralhos
$objeto = new CrtlListarAspectosBaralhos();
// Chame o método exibirMarcador
$objeto->exibirMarcador();
?>
```

> O código que você compartilhou parece ser uma classe chamada `CrtlListarAspectosBaralhos` que lida com a exibição de marcadores de baralhos. Aqui está uma descrição passo a passo do que o código faz:
> 
> 1.  Inclui o arquivo "`../MODEL/dao.baralhos.php`" usando o `require_once`. Isso sugere que haja um arquivo chamado **"dao.baralhos.php"** na pasta **"../MODEL"** que contém a definição da classe "`baralhosDAO`".
> 2.  Define a classe "`CrtlListarAspectosBaralhos`" que possui um atributo privado chamado "`$livrosDAO`" e um construtor "`\_\_construct()`". O construtor inicializa o atributo "`$livrosDAO`" criando uma instância da classe "`baralhosDAO`".
> 3.  Define um método chamado "`exibirMarcador()`" que chama o método "getAllMarcadoresBar()" da classe "`baralhosDAO`" através do objeto "`$this->livrosDAO`". O resultado é armazenado na variável "`$resultado`".
> 4.  Verifica se "`$resultado`" não está vazio usando a função `empty()`. Se não estiver vazio, o código exibe os dados formatados usando `echo '<pre>'; print_r($resultado); echo '</pre>';`.
> 5.  Se "`$resultado`" estiver vazio, o código exibe a mensagem ***"Nenhum registro encontrado."*** usando `echo`.
> 6.  Instancia a classe "```CrtlListarAspectosBaralhos```" usando "`$objeto = new CrtlListarAspectosBaralhos()`".
> 7.  Chama o método "`exibirMarcador()`" no objeto "`$objeto`" usando "`$objeto->exibirMarcador()`".
> 
> Portanto, quando você executar esse código, ele irá criar uma instância da classe "`CrtlListarAspectosBaralhos`", chamar o método "`exibirMarcador()`" e exibir os marcadores de baralhos, caso existam, ou a mensagem "Nenhum registro encontrado.".


👍👉 RESULTADO
===============

![image](https://github.com/H7-Dev/README.X/assets/93455937/a4759759-52dc-4613-acdf-e56d92cad928)

Próximos passos
===============
Criar um view para mostrar ao usuário o resultado processado no controller e obtidos a partir da MODEL

Considerações finais
=====================
- O método getAllMarcadoresBar pertecen a class baralhosDAOS está no MODEL/dao.baralhos.php
- O método exibirMarcador pertence a class CrtlListarAspectosBaralhos em CONTROLLER/c.listarAspecto.baralhos.php
