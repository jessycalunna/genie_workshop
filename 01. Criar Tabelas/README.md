<img src="../images/header.jpg">

# 01. Importe os dados para o storage

Importe os arquivos de dados no Container disponível.

# 02. Crie o database
``` sql
USE CATALOG jessyca_demos;

CREATE DATABASE IF NOT EXISTS genie_workshop;

```

## 02.1. Crie as tabelas com os arquivos disponíveis

1. Crie a tabela de vendas
``` sql
CREATE TABLE jessyca_demos.genie_workshop.tb_vendas
AS SELECT * FROM parquet.`abfss://jessyca-demos@oneenvadls.dfs.core.windows.net/genie-workshop/dados/vendas.parquet`
```
2. Crie a tabela de estoque
``` sql
CREATE TABLE jessyca_demos.genie_workshop.tb_estoque
AS SELECT * FROM parquet.`abfss://jessyca-demos@oneenvadls.dfs.core.windows.net/genie-workshop/dados/estoque.parquet`;
```
3. Crie a dimensão de medicamento
``` sql
CREATE TABLE jessyca_demos.genie_workshop.dim_medicamento
AS SELECT * FROM parquet.`abfss://jessyca-demos@oneenvadls.dfs.core.windows.net/genie-workshop/dados/dim_medicamento.parquet`;
```
4. Crie a dimensão de loja
``` sql
CREATE TABLE jessyca_demos.genie_workshop.dim_loja
AS SELECT * FROM parquet.`abfss://jessyca-demos@oneenvadls.dfs.core.windows.net/genie-workshop/dados/dim_loja.parquet`;
```





