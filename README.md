# [Curso Completo de PostgreSQL.](https://www.udemy.com/course/trabalhando-com-o-banco-de-dados-postgresql-completo)

# Sessão 2: Sobre o PostgreSQL - Instalação, execução e Primeiros comandos.

## Aula 6 - Download e Instalação do PostgreSQL

### Atividade

Pela escolha da não instalação do [SGBD](https://www.postgresql.org/download/) na maquina local, irei gerar um container para realizar as atividades durante o curso.

Foi instalado o docker e baixado a imagem do PostgreSQL utilizando o comando `sudo docker pull postgres:11.9`. Logo então foi iniciado o serviço utilizando o comando `sudo docker run --name same-postgres -e POSTGRES_PASSWORD=postgres -p 5432:5432 -d postgres:11.9`.

## Aula 7 - Permissões de Acesso ao Banco - pg_hba.conf

### Atividade

Dentro da pasta `./data` é possivel encontrar o arquivo `pg_hba.conf` e nele encontrar a seguinte configuração:<br>
| TYPE | DATABASE | USER | ADDRESS | METHOD |
| ----- | -------- | ---- | --------------- | ------ |
| local | all | all | 127.0.0.1/32 | md5 |
| host | all | all | 192.168.93.0/24 | md5 |

Essa pasta irá dar acesso a um IP em uma base de dados especifica, usuario e seu metodo de autenticação.

## Aula 8 - Primeiros Passos, PG ADMIN - CLIENT SQL Paralelos

### Atividade

Mostrado como criar um database através do pgAdmin 4.<br>
`Servers: Right Mouse Click > Create > Server...`<br>

```
General:
  Name: PostgresDocker
Connection:
  Hostname/address: localhost
  Port: 5432
  Maintenance database: postgres
  Username: postgres
  Password: postgres

SAVE!
```

<br>
Também ensinado como criar um novo Schema dentro do database.<br>

`Servers > Databases > postgres > Schemas: Right Mouse Click > Create > Schema...`<br>

```
General:
  Name: SCH
  Owner: postgres

SAVE!
```

Você pode definir qualquer usuário que quiser como ROOT do Schema. Todo e qualquer database pode ter inumeros Schemas.

## Aula 9 - Criando Tabelas e Campos

### Atividade

Também é possivel criar tabelas direto do pgAdmin e diversas outras coisas.<br>
`Servers > Databases > postgres > Schemas > SCH > Tables: Right Mouse Click > Create > Table...`

```
General:
  Name: User
  Owner: postgres
  Schema: SCH
Columns:
  Click Added +:
    Name: username
    Data type: character varying[]
    Length/Precision: 20
    Not NULL? Yes
    Primary Key? Yes
  Click Added +:
    Name: id
    Data type: bigint
    Not NULL? Yes
    Primary Key? Yes

ENTER!
```

Como também é possível criar uma tabela através de comandos de SQL.
Icone: `Query Tool`.

```sql
CREATE TABLE "User"(
  id bigint primary key not null,
  username varchar(10) not null
)
```

## Aula 10 - Gerando Dados - Inserindo Informações e Tipos de Consultas

### Atividade

É possivel também dizer que um campo é unico e/ou referenciavel utilizando CONSTRAINTS.
`Servers > Databases > postgres > Schemas > SCH > Tables > User > Constraints: Right Mouse Click > Create > "Unique constraint", "Primary Key" ou "Foreign Key"`

Também é possivel fazer isso através de comandos em SQL como por exemplo:

#### Primary Key e Unique

```sql
CREATE TABLE "User"(
  id bigint primary key not null
  username varchar(10) unique
)
```

#### Foreign Key, Primary Key e Unique

```sql
CREATE TABLE "User"(
  id bigint primary key not null
  username varchar(10) unique
)
CREATE TABLE "Role"(
  id bigint primary key not null
  name varchar(10) not null,
  idUser int
  constraint fk_user
    foreign key(idUser)
      references "User"(id)
)
```

Em casos de inserção/alteração/exclusão posterior de campos para chave primaria, campo unico ou chave estrangeira, se usa:

#### Primary Key

`ALTER TABLE "User" ADD password varchar(10) primary key not null`
`ALTER TABLE "User" ALTER COLUMN password varchar(20)`
`ALTER TABLE "User" DROP COLUMN password`

#### Foreign Key

`ALTER TABLE "Role" ADD CONSTRAINT fk_user FOREIGN KEY (idUser) REFERENCES "User"(id)`
`ALTER TABLE "Role" DROP CONSTRAINT fk_user`

#### Unique

`ALTER TABLE "User" ALTER COLUMN username unique`

## Aula 11 - Tipos de Campos - Integridade dos dados - CONSTRAINTS

### Atividade

Reforço sobre as CONSTRAINTS e suas variações, igualmente citada na aula anterior, porém agora de maneira mais pratica e com testes e casos de uso.

## Aula 12 - Criação e Conceituação de Views

### Atividade

A `View` é uma especie de tabela pré-formatada que tem como objetivo retornar dados ao cliente de maneira já organizada e limitada.
Ele apenas funciona como consulta.

Exemplo de criação:

```sql
CREATE VIEW Username as (
  SELECT username FROM "User"
)
```

## Aula 13 - Relação entre tabelas - Chaves Primárias - Estrangeiras

### Atividade

Reforço sobre chave primaria e chave estrangeira dentro de uma tabela, utilizando inserções dentro do banco de dados e analisando os erros que o mesmo trás.

# Seção 3:Trabalhando com os dados - Comandos básicos e avançados

## Aula 15 - Consultas SQL - Select

### Atividade

Explicado a forma e a estrutura do `SELECT` dentro de um SGBD, exemplo:

```sql
SELECT
  *
FROM tabela
INNER JOIN outra_tabela on outra_tabela.id = tabela.Id_outra_tabela
WHERE tabela.id = 1
```

## Aula 16 - Consultas SQL - Select

### Atividade

Explica a condição `WHERE` dentro de consultas, onde posse haver diversas condições da tabela principal ou das demais relacionadas.

```sql
SELECT * FROM tabela
  INNER JOIN outra_tabela on outra_tabela.id = tabela.Id_outra_tabela
    WHERE outra_tabela.id = 1
```

## Aula 17 - Dando nome aos campos e Tabelas 'ALIAS'

### Atividade

Explica que é possivel dar outro nome a coluna na hora de mostrar o resultado da consulta. Exemplo de caso de uso:

Existem dois campos que precisam ser unidos `NOME` e `SOBRENOME` para retornar em um unico campo e o cliente receber isso em uma LABEL.
É realizado uma concatenação com `||`, exemplo :

```sql
SELECT
  nome,
  sobrenome,
  (nome||' '||sobrenome) as nome_completo
FROM "User"
```

## Aula 18 - Operacões - SELECT, INSERT, DELETE, UPDATE

### Atividade

Explicado o conceito e estrutura das operações: `SELECT`, `INSERT`,`DELETE`,`UPDATE`.

## Aula 19 - Sub Selects - Múltiplas Consultas

### Atividade

Explicado o conceito de SubSelect e como utiliza-lo.
Exemplo Pratico:

```sql
SELECT * FROM (
  SELECT
    id,
    nome,
    cpf
  FROM "PESSOA"
) AS A
```

## Aula 20 - Junções - INNER JOIN, LEFT JOIN, FULL JOIN

### Atividade

Explicação do conceito de junções dentros dos bancos SQL para relacionamento de mais tabelas.

#### INNER JOIN

Prioriza a busca dos dados das duas tabelas relacionadas. Caso uma das duas, tenham em seu relacionamento um campo vazio não irão aparecer na consulta.

#### LEFT JOIN

Prioriza a busca dos dados por parte da tabela principal `FROM` na consulta. Caso a tabela relacionada tiver um campo vazio, irá imprimir `NULL`.

#### RIGHT JOIN

Prioriza a busca dos dados por parte da tabela relacionada. Caso a tabela principal não tenha o campo informado, ele não irá aparecer na consulta.

#### FULL JOIN

Não prioriza as busca dos dados, apenas devolve todos os dados das duas tabelas relacionadas.

## Aula 21 - Trabalhando com - CASE - IF - COALESCE - REPLACE - SUBSTR

### Atividade

Explica sobre a estrutura condicional `IF` e `CASE` dentro do banco de dados.
As duas possuem o mesmo funcionamento, porém como uma sintaxe diferente.

O `COALESCE` serve para identificar campos nulos e preenche-los com algum outro valor informado, exemplo: `COALESCE(nome,'')` ou `COALESCE(valor,0)`

O `REPLACE` você pode identificar algum caracter e remove-lo ou substitui-lo por algum outro caractér.

O `SUBSTRING` serve para cortar um texto de-a partir de onde informa-lo.

## Aula 22 - Comandos - Count , Max, Min, Limit , Sum, Group By, Order By

### Atividade

`Count` é utilizado para contagem de linhas dentro de uma consulta em especifico. É possivel colocar condições dentro dela para contagens de certas linhas em especifico. Sua sintexe é:

```sql
SELECT COUNT(username) FROM "User
```

`Max` busca o maior valor dentro de uma consulta. Sua sintexe é:

```sql
SELECT MAX(preco) FROM "Produto"
```

`Min` busca o menor valor dentro de uma consulta. Sua sintexe é:

```sql
SELECT MIN(preco) FROM "Produto"
```

`Limit` colocar um limite de resultados da consulta. Exemplo: é possivel retornar apenas 1 ou 10 resultados de uma consulta. Sua sintaxe é:

```sql
SELECT * FROM "User" Limit 1
```

## Aula 23 - Comando WITH - POSTGRE e ORACLE

### Atividade

O comando `WITH` funciona como se você criasse uma tabela temporária e consultadsse ela, porém, em nível de consulta mesmo.
Exemplo:

```sql
WITH PR AS (
  SELECT * FROM "User" WHERE estado = "PR"
),
SP AS (
  SELECT * FROM "User" WHERE estado = "SP"
)
SELECT * FROM PR
UNION
SELECT * FROM SP
```

Através desse comando é possivel fazer diversas comparações entre os dados consultados.

## Aula 24 - Introdução e conceituacão de Trigers

### Atividade

As triggers são operações realizadas de maneira espontanea para eventos especificos dentro do banco de dados. Quando uma operação de `INSERT`, `UPDATE` e `DELETE` é executado, podemos usar as triggers para fazer outra operação.

As operações de triggers que temos são:
`FOR`: é o valor padrão e faz com que a trigger seja disparado junto da ação.
`AFTER`: faz com que o disparo se de somente após a ação que o gerou.
`INSTEAD OF`: faz com que a trigger seja executada no lugar da ação.

## Aula 25 - Criação de Funcão e Triggers - Trabalhando em Paralelo

### Atividade

Explicado na aula como criar uma trigger, sua sintaxe e funcionamento.
Para a criação do gatilho, são feitos em duas etapas:

#### FUNCTION

```sql
CREATE OR REPLACE FUNCTION fn_nome()
RETURNS TRIGGER
LANGUAGE plpgsql
AS $BODY$
BEGIN

  IF(TG_TOP = 'UPDATE') THEN
    UPDATE tabela SET campo = dado
  ELSEIF(TG_TOP = 'INSERT') THEN
    UPDATE tabela SET campo = dado
  END IF;

END;
$BODY$
```

#### TRIGGER

```sql
CREATE TRIGGER t_nome { BEFORE | AFTER | INSERT OR UPDATE}
ON  tabela [ FOR [ EACH ] { ROW | STATEMENT } ]
WHEN (pg_trigger_depht() = 0)
EXECUTE PROCEDURE fn_nome ();
```
