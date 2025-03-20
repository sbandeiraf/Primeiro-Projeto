# Primeiro-Projeto # Desafio 02 @digitalcollage

# Objetivo 
Praticar o conceito de criação de ETL utilizando a ferramenta Pentaho

# Atividade  
1. Escolher um problema de negócio com base nos dados contidos na base de dados 'northwind.sql'
2. Criar a estrutura do Data Warehouse utilizando scripts em SQL
3. Criar os scripts de ingestão de dados utilizando o Pentaho (KTRs e Jobs)
4. Desenvolver um dashboard no Power BI

## Projeto: Volume de Vendas 

Este projeto foi desenvolvido para gerar insights referentes ao volume de vendas por clientes, funcionários e regiões, tendo como base o faturamento.

O foco é em um cenário fictício de uma empresa.  
Abaixo estão as fases detalhadas do projeto.

---

# Etapas do Projeto 
1. Escolher o problema de negócio que será analisado;
2. Realizar a análise exploratória;
3. Definir os campos que serão utilizados para a criação das tabelas de dimensões e fato;
4. Criação do Data Warehouse:
   - Realizar a conexão com o banco de dados 'northwind.sql' para popular o nosso DW no Pentaho;
   - Criar os ktrs para popular as tabelas;
   - Criar o JOB para executar os ktrs;
5. Realizar a conexão com o DW no PostgreSQL utilizando o Power BI;
6. Desenvolver o dashboard no Power BI para visualização de insights;
7. Publicar e disponibilizar o projeto online.

## Fase 1: Criação do Banco de Dados:

```sql
-- Criando a dimensão tempo:
CREATE TABLE dw_trabalho02.dim_tempo(
  id_tempo SERIAL PRIMARY KEY NOT NULL,
  data_inteira DATE,
  ano INT,
  mes INT,
  dia INT,
  mes_extenso VARCHAR(20),
  mes_abrev VARCHAR(20)
);

-- Criando a dimensão clientes:
CREATE TABLE dw_trabalho02.dim_clientes(
  id_cliente VARCHAR(10) PRIMARY KEY NOT NULL,
  nome_empresa VARCHAR(100),
  cidade VARCHAR(30)
);

-- Criando a dimensão funcionário:
CREATE TABLE dw_trabalho02.dim_funcionario(
  id_funcionario INT PRIMARY KEY NOT NULL,
  ultimo_nome VARCHAR(80),
  primeiro_nome VARCHAR(80),
  data_contratacao DATE
);

-- Criando a tabela FATO:
CREATE TABLE dw_trabalho02.fato_pedidos_(
  id_fato_pedido SERIAL PRIMARY KEY,
  id_cliente_fk VARCHAR(10) NOT NULL,
  id_funcionario_fk INT NOT NULL,
  id_tempo_fk INT NOT NULL,
  id_pedido INT NOT NULL,
  data_pedido DATE NOT NULL,
  preco_unitario FLOAT NOT NULL,
  quantidade INT NOT NULL,
  desconto FLOAT,
  valor_total FLOAT NOT NULL,
  CONSTRAINT fk_cliente FOREIGN KEY (id_cliente_fk) REFERENCES dw_trabalho02.dim_clientes(id_cliente),
  CONSTRAINT fk_funcionario FOREIGN KEY (id_funcionario_fk) REFERENCES dw_trabalho02.dim_funcionario(id_funcionario),
  CONSTRAINT fk_tempo FOREIGN KEY (id_tempo_fk) REFERENCES dw_trabalho02.dim_tempo(id_tempo)
);
```

Desenho da Modelagem Relacional:

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/Desenho%20da%20Modelagem%20Relacional.png" alt="Desenho da Modelagem Relacional" width="800"/>

## Fase 02: Conexão com o Banco (PostgreSQL) x Pentaho:

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/Conex%C3%A3o%20entre%20o%20banco%20e%20pentaho.png" alt="Conexão com banco - Pentaho" width="800"/>

## Fase 03: Criação dos ETLs:
a. ETL_DW_DIM_CLIENTES: 

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/print_etl_dim_cliente.png" alt="ETL_DW_DIM_CLIENTES" width="800"/>

b. ETL_DW_DIM_FUNCIONARIOS: 

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/print_etl_dim_funcionario.png" alt="ETL_DW_DIM_FUNCIONARIOS" width="800"/>

c. ETL_DW_DIM_TEMPO: 

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/print_etl_dim_tempo.png" alt="ETL_DW_DIM_TEMPO" width="800"/>

d. ETL_DW_FATO_PEDIDOS_: 

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/print_etl_dw_fato_pedido.png" alt="ETL_DW_FATO_PEDIDOS_" width="800"/>

e. JOB: 

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/JOB_Desafio02.png" alt="JOB" width="800"/>

Obs.: Arquivos em anexo.

## Fase 04: Popular as Tabelas Rodando o JOB:

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/Populando%20as%20tabelas.png" alt="Populando as Tabelas" width="800"/>

## Fase 05: Conectando o DW no Power BI:

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/Conectando%20com%20Power%20BI.png" alt="Conectando com Power BI" width="800"/>

## Fase 06: Dashboard:

<img src="https://github.com/sbandeiraf/Primeiro-Projeto/blob/main/DEASHBOARD.png" alt="Dashboard" width="800"/>

## Fase 07: Publicação do Dashboard:

