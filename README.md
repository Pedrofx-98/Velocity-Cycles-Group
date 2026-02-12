# Análise de clientes da Empresa Velocity Cycles Group
Utilizando o banco de dados AdventureWorks2022, referente a uma empresa imaginária de fabricação e venda de bicicletas, iniciamos uma análise para entender a evolução dos clientes ao longo do tempo, principalmente entre 2011 e 2013. O objetivo inicial é fazer uma análise exploratória dos clientes que compraram os produtos da  Velocity Cycles Group, entendendo onde estão, quanto e o que compram, se houve evolução na base de novos clientes e onde está o maior impacto desta evolução.

Fazendo o download do arquivo AdventureWorksDW2022.bak e anexando-o no SQL Server, é possível executar cada consulta SQL utilizada nesta análise e obter os mesmos resultados apresentados.
<br><br>

## Análise exploratória de dados
<img align="right" width="400"  src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/sql_clientes.png">
Iniciei o projeto realizando o download do arquivo AdventureWorksDW2022.bak e restaurando o banco de dados no SQL Server. Em seguida, conduzi uma análise minunciosa da estrutura do banco, explorando tabelas, campos, tipos de dados e relacionamentos para entender como o modelo estava organizado e identificar as principais tabelas relacionadas a clientes e vendas. Com esse entendimento, desenvolvi os primeiros scripts em SQL durante a etapa de Análise Exploratória de Dados (EDA), com o objetivo de gerar uma visão inicial do comportamento da base de clientes e do desempenho comercial da empresa.<br>
<br>

Primeiramente, calculei o total de clientes distintos com vendas utilizando <code>COUNT</code> combinado com <code>DISTINCT</code>, aplicando <code>FORMAT</code> para padronizar a visualização do resultado. Em seguida, analisei a distribuição de clientes por país/região, realizando <code>INNER JOIN</code> entre as tabelas de vendas, clientes e geografia, consolidando as informações com <code>GROUP BY</code> e organizando os resultados com <code>ORDER BY</code>, o que permitiu identificar os mercados com maior concentração de clientes ativos.

Também explorei o comportamento de compra por produto, identificando os cinco modelos mais adquiridos por meio de TOP 5, <code>COUNT</code> e <code>GROUP BY</code>, o que trouxe uma visão clara sobre os produtos com maior volume de vendas.

Para aprofundar a análise, calculei a média de vendas por cliente a partir de uma subconsulta, onde utilizei <code>SUM</code> para consolidar o total vendido por cliente e, posteriormente, <code>AVG</code> para obter a média geral. Por fim, analisei o ticket de vendas utilizando <code>MIN</code>, <code>AVG</code> e <code>MAX</code>, identificando respectivamente o menor valor de venda, o ticket médio e o maior valor registrado. Esses cálculos auxiliaram a responder as principais demandas dos gestores da empresa, que era entender o panomara geral dos clientes, como por exemplo: <br><br>
- Clientes distintos <br>
- Clientes por país/região <br>
- Produtos mais comprados por estes clientes <br>
- Média de vendas para cada cliente <br>
- E informações pertinentes, como ticket médio, mínimo e máximo.
<br><br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/SQL/AdventureWorks%20-%20Clientes.sql" target="_blank">Clique aqui</a> e acesse o script SQL no Github.

<br>

## Análise de Novos Clientes
<img align="left" width="500"  src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/sql_Novos_clientes.png">
Na segunda etapa do projeto, o foco foi analisar a aquisição de clientes ao longo do tempo. Mais do que apenas contabilizar vendas, a proposta foi entender em que momento cada cliente passou a integrar a base e como essa entrada evoluiu mês a mês.

Para organizar essa lógica, optei por trabalhar com uma CTE (Common Table Expression), o que permitiu dividir a análise em etapas mais claras. O primeiro passo foi identificar a data da primeira compra de cada cliente por meio da função <code>MIN</code>, assegurando que cada cliente fosse considerado exatamente no período em que passou a gerar receita. A partir dessa informação, extraí o ano e o mês com <code>DATEPART (YEAR e MONTH)</code>, estruturando a base de acordo com o período de aquisição. Para manter a padronização e garantir a ordenação correta, apliquei <code>FORMAT('00')</code> ao mês.

A consolidação das informações por cliente foi feita com <code>GROUP BY</code>, enquanto a cláusula <code>HAVING</code> delimitou a análise aos clientes cuja primeira compra ocorreu entre 2011 e 2013, mantendo o recorte temporal do estudo.

Com a base já estruturada por período de entrada, passei a mensurar o volume de novos clientes por meio do <code>COUNT</code>, obtendo o total mensal de aquisições. Na sequência, incorporei uma camada comparativa com a função de janela <code>LAG</code>, associada ao <code>OVER (ORDER BY Ano, Mes)</code>, permitindo recuperar automaticamente o número de novos clientes no mesmo mês do ano anterior.

Por fim, a estrutura condicional <code>CASE</code> viabilizou o cálculo tanto da variação absoluta quanto do crescimento percentual em relação ao período anterior, enquanto o <code>ORDER BY</code> garantiu a organização cronológica do resultado final. Permitindo os seguintes cálculos:

- Novos Clientes  <br>
- Novos Clientes Ano Anterior<br>
- Variação de novos clientes entre períodos <br>

Analisando a variação de novos clientes entre períodos, foi possível identificar em 2013, um crescimento mensal muito acima da variação de 2012, sendo necessário aprofundar a análise e identificar de onde está vindo este grande crescimento de novos clientes.
<br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/SQL/AdventureWorks%20-%20Novos%20Clientes.sql">Clique aqui</a> e acesse o script SQL no Github.
<br><br>

## Variação de novos clientes entre períodos
<img align="right" width="500" height="500" src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/sql_Novos%20Clientes%20Delta%202013.png">
Na terceira etapa de análise, visualizando a variação de novos clientes, quando comparados com o mesmo período/mês do ano anterior, decidi agrupar esta variação por região/país para identificar se houve crescimento. 
Filtrei apenas o ano de 2013, pois foi o período com maiores taxas de crescimentos de novos clientes, o que permitiu concluir que: <br><br>
- Canadá teve o maior crescimento percentual entre todos os países - aproximadamente 623%. <br>
- Estados Unidos teve o maior crescimento cumulativo de clientes - aproximadamente 5050. <br>
- Apenas os Estados Unidos tiveram um crescimento maior que todos países da Europa juntos, sendo a América do Norte o principal mercado de atuação da empresa.
- Todos países europeus dobraram ou superaram sua base de novos clientes. <br>
- Austrália, apesar de não ter um crescimento comparável com Europa e América do Norte, aumentou sua base de novos clientes em quase 50%, sendo um ótimo resultado em 2013. <br>

<br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/SQL/AdventureWorks%20-%20Novos%20Clientes%20Delta%202013.sql" target="_blank">Clique aqui</a> e acesse o script SQL no Github.

## Conclusão técnica SQL
Com o SQL, podemos analisar, extrair, manipular e exibir os dados de uma base de dados de uma forma simples e rápida, apenas conectando direto na fonte dos dados. Porém, não é uma ferramenta dinâmica em com abordagem visual, pois cada vez que pricisa ver os dados de uma forma diferente, precisa reescrever o comando SQL para extrair os dados da forma que gostaria, porem os dados sempre serão exibidos em formato de tabela, deixando sua análise menos dinamica do que um dashboard, por exemplo.

A minha conclusão é que o SQL é sempre uma linguagem muito importante e deve ser utilizada para analisar um banco de dados antes de escolher outra ferramenta para análise dos dados, como o Power BI por exemplo. Ou seja, validar as informações no SQL e depois consider outras ferramentas de acordo com a necessidade da empresa ou projeto que estiver atuando é uma excelente decisão para quem trabalha com dados.

Assim como eu mencionei no projeto MaxOil Solutions, não existe uma ferramenta melhor que a outra, existe ferramentas adequadas as necessidades apresentadas em cada projeto de dados.

<a href="https://github.com/Pedrofx-98/MaxOilSolutions" target="_blank">Clique aqui</a> caso queira acessar mais informações do projeto MaxOil Solutions no Github.

## Dashboard Power BI
<img align="right" width="500"  src="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/Dashboard.png">
Seguindo a idéia de melhorar a ferramenta para uma análise dinâmica e visual de informações, desenvolvi um dashboard focado na análise dos clientes novos e recorrentes da mesma base de dados AdventureWorks2022 utilizada em todo o projeto.
Como o Power BI permite análises dinâmicas e visuais de forma simples, escrevendo menos código DAX e permitindo o usuário total interação com a ferramenta, fiz uma análise exploratória na quantidade e receita entre Clientes novos e recorrentes.<br>
Com esta análise, cheguei as seguintes conclusões:<br>
 - A maioria dos clientes a partir de 2013 é novo. <br>
 - Além da quantidade de clientes novos, a receita trazida por clientes novos também é a maior fatia do total.<br>
 - Os clientes novos não são a maioria para todos países e períodos. Por isso o Power BI é uma ferramenta de extrema importância, pois permite o usuário final fazer seus filtros e ter análises de forma dinâmica.
<br><br>

<p>
Acesse o dashboard interativo desenvolvido para a empresa <strong>Velocity Cycles Group</strong>:
<br>
<a href="https://app.powerbi.com/view?r=eyJrIjoiYmNkMTgxMzctMDk2MC00MjRjLWE1ZDctZDliMDUyZGEyYTU0IiwidCI6IjY1OWNlMmI4LTA3MTQtNDE5OC04YzM4LWRjOWI2MGFhYmI1NyJ9" target="_blank">
Visualizar Dashboard no Power BI Service
</a>
</p>

<p>
O arquivo completo do projeto (.pbix) está disponível no GitHub:
<br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/PowerBI/Velocity%20Cycles%20Group.pbix">
Acessar Projeto no GitHub
</a>
</p>

<p>
Informações técnicas adicionais:
<br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/Medidas.png" target="_blank">
Tabela de Medidas Desenvolvidas em DAX
</a>
<br>
<a href="https://github.com/Pedrofx-98/Velocity-Cycles-Group/blob/main/Figures/diagrama.png" target="_blank">
Diagrama do Modelo de Dados e Relacionamentos
</a>
</p>

## Ferramentas e linguagens utilizadas
<div style="display: inline_block">
    <img align="center" alt="SQL" height="40" width="40" src="https://github.com/BruceFonseca/ferramentas/blob/main/logo.png?raw=true">
    <img align="center" alt="Power BI" height="40" width="40" src="https://github.com/BruceFonseca/ferramentas/blob/main/1200px-New_Power_BI_Logo.svg.png?raw=true">
</div>
