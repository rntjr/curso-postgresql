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
|------|----------|------|---------|--------|
| local | all | all | 127.0.0.1/32 | md5 |
| host | all | all | 192.168.93.0/24 | md5 |

Essa pasta irá dar acesso a um IP em uma base de dados especifica, usuario e seu metodo de autenticação.

## Aula 8 - Primeiros Passos, PG ADMIN - CLIENT SQL Paralelos

### Atividade
