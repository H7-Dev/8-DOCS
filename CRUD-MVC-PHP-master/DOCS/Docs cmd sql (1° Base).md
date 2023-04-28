

Esse código é uma série de comandos SQL usados para criar uma nova base de dados chamada "db\_flashCardBar", selecioná-la como a base de dados atual e criar uma tabela chamada "tb\_baralhos" com várias colunas. A tabela é definida como tendo um ID de baralho, nome do baralho, data de criação, descrição do baralho e um identificador de marcador opcional. O comando SELECT é usado para mostrar todas as informações da tabela recém-criada, e o comando INSERT é usado para adicionar sete linhas à tabela com informações sobre cada baralho.


Claro, segue abaixo uma  documentação dos comandos SQL utilizados no código:

Documentação do Comando SQL 
===========================
### **1° Parte**

Criação da base de dados
------------------------

sql

```sql
CREATE DATABASE IF NOT EXISTS db_flashCardBar CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```

Cria uma nova base de dados chamada "db\_flashCardBar" com o conjunto de caracteres "utf8mb4" e collation "utf8mb4\_unicode\_ci", se a mesma não existir.

Seleção da base de dados
------------------------

```sql
USE db_flashCardBar;
```

Seleciona a base de dados "db\_flashCardBar" como a base de dados atual para que as próximas consultas sejam executadas nela.

Criação da tabela "tb\_baralhos"
--------------------------------

sql

```sql
CREATE TABLE IF NOT EXISTS tb_baralhos (
    idBar VARCHAR(255) NOT NULL,
    c_bar VARCHAR(255) NOT NULL,
    c_dt DATE NOT NULL,
    c_dtc DATE NOT NULL DEFAULT CURRENT_DATE,
    c_dtMod TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP,
    PRIMARY KEY (idBar)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COLLATE=utf8mb4_unicode_ci COMMENT='Tabela de usuários do sistema';
```

Cria uma nova tabela chamada "tb\_baralhos" com as seguintes colunas:

*   "idBar" - identificador único do baralho (texto com até 255 caracteres)
*   "c\_bar" - nome do baralho (texto com até 255 caracteres)
*   "c\_dt" - data de criação do baralho (data no formato "YYYY-MM-DD")
*   "c\_dtc" - data de criação do registro (data no formato "YYYY-MM-DD") com valor padrão de "CURRENT\_DATE"
*   "c\_dtMod" - data de modificação do registro (data e hora no formato "YYYY-MM-DD HH:MM:SS") com valor padrão de "CURRENT\_TIMESTAMP ON UPDATE CURRENT\_TIMESTAMP"
*   A coluna "idBar" é definida como chave primária da tabela.
*   A tabela é definida com o motor InnoDB, o conjunto de caracteres "utf8mb4" e collation "utf8mb4\_unicode\_ci", e um comentário descrevendo a tabela.

Consulta de dados da tabela "tb\_baralhos"
------------------------------------------

sql

```sql
SELECT * FROM tb_baralhos;
```

Exibe todas as informações de todas as linhas da tabela "tb\_baralhos".

Inserção de dados na tabela "tb\_baralhos"
------------------------------------------

sql
```sql
INSERT INTO tb_baralhos 
    (idBar, c_bar, c_dt, c_descr, idMarcador) 
    VALUES 
    (1, 'Baralho #001', '2023-01-01', 'Meu primeiro Baralho', 'Marcador A'),
    (2, 'Baralho #002', '2023-01-02', 'Meu segundo Baralho', NULL),
    (3, 'Baralho #003', '2023-01-03', 'Meu terceiro Baralho', 'Marcador A'),
    (4, 'Baralho #004', '2023-01-04', 'Meu quarto Baralho', 'Marcador A'),
    (5, 'Baralho #005', '2023-01-05', 'Meu quinto Baralho', 'Marcador B'),
    (6, 'Baralho #006', '2023-01-06', 'Meu sexto Baralho', 'Marcador B'),
    (7, 'Baralho #007', '2023-01-07', 'Meu setimo Baralho', 'Marcador C');
```


Documentação do Comando SQL 
===========================
**2° Parte**

Comandos SQL
------------

Os comandos SQL usados neste projeto são os seguintes:

### Adicionar Coluna

O seguinte comando adiciona uma nova coluna chamada "c\_descr" à tabela "tb\_baralhos":

sql

```sql
ALTER TABLE tb_baralhos
ADD c_descr VARCHAR(255) NULL AFTER c_dt;
```

### Adicionar Coluna para Chave Estrangeira

O seguinte comando adiciona uma nova coluna chamada "idMarcador" à tabela "tb\_baralhos" que servirá como chave estrangeira para a tabela "tb\_marca":

sql

```sql
ALTER TABLE tb_baralhos ADD idMarcador VARCHAR(255) NULL AFTER c_descr;
```

### Criar Restrição de Chave Estrangeira

O seguinte comando cria uma restrição de chave estrangeira chamada "fk\_tb\_marca", que associa a coluna "idMarcador" da tabela "tb\_baralhos" à coluna "idMarcador" da tabela "tb\_marca":

sql

```sql
ALTER TABLE tb_baralhos ADD CONSTRAINT fk_tb_marca
    FOREIGN KEY (idMarcador) REFERENCES tb_marca(idMarcador)
    ON DELETE SET NULL
    ON UPDATE CASCADE;
```

As restrições das chaves estrangeiras (foreign keys) ponto a ponto, em geral, referem-se às operações de atualização e exclusão de registros relacionados em tabelas distintas.

* A restrição ON UPDATE CASCADE é usada para manter a consistência entre a tabela referenciadora e a tabela referenciada, ou seja, quando uma chave primária na tabela referenciada é atualizada, a mesma atualização é refletida na tabela referenciadora automaticamente, garantindo a integridade referencial.

*  Já a restrição ON DELETE SET NULL é utilizada para permitir a exclusão de registros na tabela referenciada, mesmo que haja registros na tabela referenciadora que apontem para eles. Quando um registro na tabela referenciada é excluído, a referência correspondente na tabela referenciadora é definida como nula.

* Outras restrições de chaves estrangeiras incluem a restrição ON DELETE CASCADE, que exclui automaticamente os registros correspondentes na tabela referenciadora quando um registro na tabela referenciada é excluído, e a restrição ON UPDATE SET NULL, que define a referência correspondente na tabela referenciadora como nula quando uma chave primária na tabela referenciada é atualizada.

>É importante notar que as restrições de chaves estrangeiras são uma forma essencial de garantir a integridade referencial em bancos de dados relacionais, >impedindo a inserção de dados inconsistentes ou inválidos que possam afetar a precisão e confiabilidade dos dados armazenados.


Documentação do Comando SQL 
===========================
**3° Parte**

Comandos SQL
------------
### Selecionar Dados com Junções

O seguinte comando seleciona dados das tabelas "tb\_baralhos" e "tb\_marca" usando uma junção do tipo LEFT JOIN e filtrando por um valor específico na coluna "c\_bar":

sql

```sql
SELECT tb_baralhos.*, tb_marca.*
FROM tb_baralhos
LEFT JOIN tb_marca
ON tb_baralhos.idMarcador = tb_marca.idMarcador
WHERE tb_baralhos.c_bar = 'Baralho #001';
```

O seguinte comando faz o mesmo que o anterior, mas selecionando apenas as colunas "idBar", "c\_bar", "idMarcador" das tabelas "tb\_baralhos" e "idMarcador" da tabela "tb\_marca":

sql

```sql
SELECT tb_baralhos.idBar, tb_baralhos.c_bar, tb_baralhos.idMarcador, tb_marca.idMarcador
FROM tb_baralhos
LEFT JOIN tb_marca
ON tb_baralhos.idMarcador = tb_marca.idMarcador
WHERE tb_baralhos.c_bar = 'Baralho #001';
```

O seguinte comando seleciona dados das tabelas "tb\_baralhos" e "tb\_marca" usando uma junção do tipo LEFT JOIN e filtrando por um valor específico na coluna "idMarcador":

sql

```sql
SELECT tb_baralhos.idBar, tb_baralhos.c_bar, tb_baralhos.idMarcador, tb_marca.idMarcador
FROM tb_baralhos
LEFT JOIN tb_marca
ON tb_baralhos.idMarcador = tb_marca.idMarcador
WHERE tb_baralhos.idMarcador = 'Marcador A';
```

O seguinte comando seleciona dados das tabelas "tb\_baralhos" e "tb\_marca" usando uma junção do tipo RIGHT JOIN:

sql

```sql
SELECT tb_baralhos.idBar, tb_baralhos
```


