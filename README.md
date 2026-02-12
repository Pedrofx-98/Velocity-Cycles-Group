# Análise de clientes da Empresa Velocity Cycles Group
Utilizando o banco de dados AdventureWorks2022, referente a uma empresa imaginária de fabricação e venda de bicicletas, iniciamos uma análise para entender a evolução dos clientes ao longo do tempo, principalmente entre 2011 e 2013. O objetivo inicial é fazer uma análise exploratória dos clientes que compraram os produtos da  Velocity Cycles Group, entendendo onde estão, quanto e o que compram, se houve evolução na base de novos clientes e onde está o maior impacto desta evolução.

Fazendo o download do arquivo AdventureWorksDW2022.bak e anexando-o no SQL Server, é possível executar cada consulta SQL utilizada nesta análise e obter os mesmos resultados apresentados.
<br><br><br>

## Análise exploratória de dados
<img align="right" width="400"  src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/sql_clientes.png">
Iniciamos o projeto baixando o arquivo AdventureWorksDW2022.bak e restaurando o banco de dados no SQL server. Em um segundo momento, foi analisado minunciosamente cada objeto, tabela, campo, tipos de dados e relacionamentos do modelo de dados AdventureWorks. Após identificar a tabela de clientes e vendas, desenvolvemos os scripts em SQL para explorar os dados e extrair os primeiros insights durante a análise exploratória de dados. Nessa etapa, utilizamos de diversas funções (<code>FORMAT</code>,<code>COUNT</code>, <code>DISTINCT</code>, <code>AS</code>, <code>INNER JOIN</code>, <code>GROUP BY</code>, <code>ORDER BY</code>, <code>SUM</code>, <code>MIN</code>, <code>MAX</code> e <code>AVG</code>) que auxiliaram a responder as principais demandas dos gestores da empresa, que era entender o panomara geral dos clientes, como por exemplo: <br><br>
- Clientes distintos <br>
- Clientes por país/região <br>
- Produtos mais comprados por estes clientes <br>
- Média de vendas para cada cliente <br>
- E informações pertinentes, como ticket médio, mínimo e máximo.
<br><br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/SQL/AdventureWorks%20-%20Clientes.sql" target="_blank">Clique aqui</a> e acesse o script SQL no Github.

<br><br>

## Análise de Novos Clientes
<img align="left" width="500"  src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/sql_Novos_clientes.png">
Em um segundo passo, decidimos identificar os novos clientes. Para isso, decidimos agrupar os clientes por ano e mês em uma CTE - Common Table Expression, porém é possível o mesmo resultado utilizando outras técnicas. Na CTE criada com o nome ClientesPrimeiraDataCompra, identificamos qual foi a primeira compra de cada cliente e agrupando novos clientes por ano e mês. Já com os dados agrupados, utilizamos a função de janela <code>LAG</code> para encontrar novos clientes no mesmo mês do ano anterior, também  permitindo os seguintes cálculos: <br><br>
- Novos Clientes  <br>
- Novos Clientes Ano Anterior<br>
- Variação de novos clientes entre períodos <br>
<br>
<a href="https://github.com/BruceFonseca/AdventureWorks2022/blob/main/SQL/AdventureWorks%20-%20Novos%20Clientes.sql" target="_blank">Clique aqui</a> e acesse o script SQL no Github.
<br><br>
Analisando a variação de novos clientes entre períodos, é possível identificar em 2013, um crescimento mensal muito acima da variação de 2012, sendo necessário aprofundar a análise e identificar de onde está vindo este grande crescimento de novos clientes.
