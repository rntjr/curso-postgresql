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

```
CREATE TABLE "SCH"."User"(

)
```
