<img src="../images/header.jpg">

# 01. Criar o Genie Space

1. No menu principal (à esquerda), clique em `New` > `Genie space`

<img src="../images/genie_01.png"><br><br>

# 02. Configure o Genie
    - Defina o nome do Genie Space como `Assistente de Vendas` ou um nome que considere adequado para a execução do Hands-On
    - Selecione seu SQL Warehouse
    - Selecione as seguintes tabelas:
        - tb_vendas
        - tb_estoque
        - dim_medicamento
        - dim_loja
    - Clique em `Save`

<img src="../images/genie_02.png" width=800>

# 03. Faça perguntas para o Genie

Com o Genie Space preparado, podemos começar a fazer nossas análises!

Basta usar o chat para fazer as perguntas abaixo:
- Qual o faturamento em out/22?
- Agora, quebre por produto
- Mantenha somente os 10 produtos com maior faturamento
- Monte um gráfico de barras
- Qual o total de produtos vendidos em genéricos?
- Qual o valor total vendido de ansiolíticos?
- Quais produtos tiveram uma proporção de vendas por estoque maior que 0.8 em Outubro de 2022?

<img src="../images/genie_05.png"><br><br>

Note que, mesmo com muito pouco contexto, a Genie já conseguiu:
- Inferir quais as tabelas e colunas relevantes para responder nossas perguntas
- Aplicar filtros e agregações
- Responder perguntas adicionais sobre uma resposta anterior
- Entender como utilizar jargões
- Combinar diferentes tabelas
- Calcular métricas derivadas

Aproveite para explorar e fazer perguntas adicionais!

# 04. Usando Comentários

Faça a seguinte pergunta:
- Qual o valor total de venda por loja? Exiba o nome da loja

Note que, apesar de o Genie identificar as tabelas que utilizaria para trazer esse resultado, ele não foi capaz de responder à pergunta de forma correta. Por quê?

No menu `Catalog` > `<nome-do-catalogo>` > `<nome-do-schema>` > `dim_loja`, verifique o nome da coluna que apresenta o nome da loja
<img src="../images/genie_10.png">

A coluna que contém o nome da loja não está com uma nomenclatura adequada para que o Genie consiga se basear por ela. Vamos adicionar um comentário nessa coluna para que seja possível utilizar a coluna correta para apresentar a informação pedida.
1. Acesse o SQL Editor
2. Altere a tabela adicionando o comentário para a coluna **nlj**
`ALTER TABLE dim_loja ALTER COLUMN nlj COMMENT 'Nome da loja'`
3. Faça a pergunta **Qual o valor total de venda por loja? Exiba o nome da loja**

Perceba que dessa vez o Genie utilizou a coluna correta que contém o nome da loja. Documentar as tabelas com comentários é sempre uma boa prática! Isso ajuda a compreensão, a descoberta e o reaproveitamento desses dados por outras pessoas. Além disso, o Genie vai ficar bem mais inteligente.

No entanto, nossa consulta ainda não retornou nenhum resultado. Vamos buscar uma solução!

# 05. Usando Chaves Primárias

Aparentemente, a coluna **id_loja** da tabela **dim_loja** não é o melhor campo para fazer os cruzamentos com a tabela de vendas. Na verdade, a coluna correta é a **cod**!

Vamos então adicionar chaves primárias e estrangeiras nessas tabelas para que a Genie não precise inferir como fazer esse cruzamento!

1. Use o SQL Editor para adicionar as chaves primárias e estrangeiras nas tabelas `dim_loja` e `vendas`

``` sql
ALTER TABLE dim_loja ALTER COLUMN cod SET NOT NULL;
ALTER TABLE dim_loja ADD CONSTRAINT pk_dim_loja PRIMARY KEY (cod);
ALTER TABLE tb_vendas ADD CONSTRAINT fk_venda_dim_loja FOREIGN KEY (id_loja) REFERENCES dim_loja(cod);
```
2. Faça novamente a pergunta anterior na Genie

Pronto! Com essa informação a Genie já consegue responder a pergunta corretamente!

# 05. Usando Instruções

Como vimos, a Genie utiliza toda a documentação das tabelas para conseguir responder perguntas. No entanto, por motivos de segurança, ela não tem acesso aos dados em si!

Por isso, para complementar o conhecimento que a Genie já possui sobre nossas bases de dados, podemos também criar instruções!

**Instruções** são nada mais que um conjunto de sentenças em linguagem natural que podem explicar para a Genie informações importantes como:
- Significado de abreviações e termos técnicos comumente utilizadas na sua empresa
- Formato do dado (por exemplo, se os registros estão em maiúsculas ou minúsculas)
- Tratamentos necessários para determinados campos
- Cálculos de métricas

Vamos ver como funciona:

1. Faça a pergunta:
    - Calcule a quantidade de itens vendidos para prescrição

2. Me parece que o resultado não está correto! Na nossa base, o termo prescrição realmente não é mencionado nenhuma vez. Mas acontece que aqui consideramos como medicamentos de prescrição aqueles que não são genéricos. Por isso, adicione a seguinte instrução:
    - `* para calcular indicadores sobre prescrição use categoria_regulatoria <> 'GENÉRICO'`

<img src="../images/genie_11.png">
