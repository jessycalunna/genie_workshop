<img src="../images/header.jpg">

# 01. Criar o Genie Space

1. No menu principal (à esquerda), clique em `New` > `Genie space`

<img src="../images/genie_01.png"><br><br>

# 02. Configure o Genie
    - Defina o nome do Genie Space como `Assistente de Vendas`
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

Note que, apesar de o Genie identificar as tabelas que utilizaria para trazer esse resultado, ele não foi capaz de responder à pergunta. Por quê?

1. No menu `Catalog` > `<nome-do-catalogo>` > `<nome-do-schema>` > `dim_loja`, verifique o nome da coluna que apresenta o nome da loja
<img src="../images/genie_10.png">
