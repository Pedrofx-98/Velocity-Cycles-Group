# Análise de clientes da Empresa Velocity Cycles Group
Utilizando o banco de dados AdventureWorks2022, referente a uma empresa imaginária de fabricação e venda de bicicletas, iniciamos uma análise para entender a evolução dos clientes ao longo do tempo, principalmente entre 2011 e 2013. O objetivo inicial é fazer uma análise exploratória dos clientes que compraram os produtos da  Velocity Cycles Group, entendendo onde estão, quanto e o que compram, se houve evolução na base de novos clientes e onde está o maior impacto desta evolução.

Fazendo o download do arquivo AdventureWorksDW2022.bak e anexando-o no SQL Server, é possível executar cada consulta SQL utilizada nesta análise e obter os mesmos resultados apresentados.
<br><br>

## Análise exploratória de dados
<img align="right" width="500"  src="https://github.com/BruceFonseca/AdventureWorks2022/blob/main/imagens/AdventureWorks%20-%20Clientes.png?raw=true">
Iniciamos o projeto baixando o arquivo AdventureWorksDW2022.bak e restaurando o banco de dados no SQL server. Em um segundo momento, foi analisado minunciosamente cada objeto, tabela, campo, tipos de dados e relacionamentos do modelo de dados AdventureWorks. Após identificar a tabela de clientes e vendas, desenvolvemos os scripts em SQL para explorar os dados e extrair os primeiros insights durante a análise exploratória de dados. 
As principais demandas dos gestores da empresa era entender o panomara geral dos clientes, como por exemplo: <br><br>
- Clientes distintos <br>
- Clientes por país/região <br>
- Produtos mais comprados por estes clientes <br>
- Média de vendas para cada cliente <br>
- E informações pertinentes, como ticket médio, mínimo e máximo.
<br><br>
<a href="https://github.com/BruceFonseca/AdventureWorks2022/blob/main/SQL/AdventureWorks%20-%20Clientes.sql" target="_blank">Clique aqui</a> e acesse o script SQL no Github.
