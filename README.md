# Primeiro-Projeto # Projeto Desafio 02 

# Objetivo 
Prática do conceito de criação de ETL utilizando ferramenta Pentaho

# Atividade  
  1. Escolher um problema de negócio com base nos dados contidos na base de dados 
“northwind.sql ou dw_northwind”

  2. Criar a estrutura do Data Warehouse, utilizando os scripts em SQL 
  
  3. Criar os scripts de ingestão de dados utilizando Pentaho (KTRs e Jobs)

  4. Desolver um DEASHBOARD no power BI


## Projeto: Volume de vendas 

Este projeto foi desenvolvido para gerar insights referente ao volume de vendas por cliente, funcionarios e região, tomando como base o faturamento.

O foco é em um cenário fictício de uma empresa.
Abaixo estão as fases detalhadas do projeto.

---

# Etapas do Projetos 
  1. Escolher o problema de negocio que sera analisado;
  2. Análise Exploratória;
  3. Definir os campos que sera utlizado para criação das tabelas dimensões e fato;
  4. Criação do Data Warehouse
  5. Realizado a conexão com o banco de dados northwind.sql para popular o nosso DW no pentaho;
  6. Realizado a criação dos ETLs para popular as tabelas;
  7. Realizar a criação do JOB para executar os ETLs;
  8. Realizado a conexão com o DW no postregre com o Power BI
  9. Realizado a criação do DEASHBOARD no Power BI para visualização de insights;
  10. Publicação e disponibilização do projeto online.


## Fase 1: Criação do Banco de Dados

```sql
--Criando a dimensão tempo:

CREATE TABLE dw_trabalho02.dim_tempo(
id_tempo SERIAL PRIMARY KEY NOT NULL,
data_inteira date,
ano int,
mes int,
dia int,
mes_extenso varchar(20),
mes_abrev varchar(20)
)

--criando a dimensão clientes:

CREATE TABLE dw_trabalho02.dim_clientes(
id_cliente VARCHAR(10) PRIMARY KEY NOT NULL,
nome_empresa VARCHAR(100),
cidade VARCHAR(30)
)

-- criando a dimensão funcionario:

CREATE TABLE dw_trabalho02.dim_funcionario(
id_funcionario INT PRIMARY KEY NOT NULL,
ultimo_nome VARCHAR(80),
primeiro_nome VARCHAR(80),
data_contratacao date
)


--criando a dimensão FATO:

CREATE TABLE dw_trabalho02.fato_pedidos_(
id_fato_pedido serial PRIMARY KEY,
id_cliente_fk VARCHAR(10) NOT NULL,
id_funcionario_fk INT NOT NULL,
id_tempo_fk INT NOT NULL,
id_pedido int NOT NULL,
data_pedido date NOT NULL,
preco_unitario float NOT NULL,
quantidade int NOT NULL,
desconto float,
valor_total float NOT NULL,

CONSTRAINT fk_cliente FOREIGN KEY (id_cliente_fk) REFERENCES dw_trabalho02.dim_clientes(id_cliente),
CONSTRAINT fk_funcionario FOREIGN KEY (id_funcionario_fk) REFERENCES dw_trabalho02.dim_funcionario(id_funcionario),
CONSTRAINT fk_tempo FOREIGN KEY (id_tempo_fk) REFERENCES dw_trabalho02.dim_tempo(id_tempo)

);

```





