Curso: INTRODUÇÃO AO DATA SCIENCE 
Atividade: desafio extra do curso
Data: 03/05/2026
● Autor / Aluno: Henrique Takashi Tamaki






● Guia Rápido — Execução e Visualização do Projeto

Informações do projeto

-Arquivo principal: `Desafio_extra2_Henrique_Tamaki.ipynb`
-Repositório GitHub: https://github.com/henriquetamaki-max/Trilha_analise_dados.git
-Notebook no Google Colab: https://colab.research.google.com/drive/16gKGgmnHvZmUXkT4b4_FKubxHGlc1E9C?usp=sharing
-Dashboard (Looker Studio): https://datastudio.google.com/s/lnKD84Ug4OE

Executar diretamente no Google Colab

Esta é a forma mais rápida, pois não exige instalação local.

1. Acesse o link do notebook: https://colab.research.google.com/drive/16gKGgmnHvZmUXkT4b4_FKubxHGlc1E9C?usp=sharing
2. Faça login em uma conta Google.
3. No menu superior, clique em Arquivo → Salvar uma cópia no Drive para poder editar e executar.
4. Para rodar todo o pipeline, clique em Ambiente de execução → Executar tudo (`Ctrl+F9`).
5. Para revisar a análise exploratória, navegue diretamente até a seção 3. Análise Exploratória pelo índice lateral do Colab.
6. Os arquivos gerados (`Local_Superstore.csv`, `Local_Superstore_EDA.csv` e os gráficos `.png`) ficam disponíveis no painel Arquivos (`/content/`).

> Observação: o dataset é baixado automaticamente via `kagglehub` (`vivek468/superstore-dataset-final`). Caso o Colab solicite autenticação Kaggle, basta seguir o prompt exibido.

Estrutura do notebook

O notebook está organizado em quatro seções, que devem ser executadas em sequência:

1. Importação e compreensão dos dados — carregamento via KaggleHub e exploração inicial.
2. Tratamento e preparação dos dados — conversão de tipos, padronização de colunas e tratamento de outliers (IQR).
3. Análise Exploratória — agrupamentos, rankings, análises temporais e investigação da relação Desconto × Lucro. *(ponto de partida sugerido para revisão dos insights)*

Visualização do Dashboard (Looker Studio)

Para consultar os indicadores e gráficos interativos, basta abrir o link:

https://datastudio.google.com/s/lnKD84Ug4OE

O dashboard apresenta os principais KPIs (vendas, lucro, margem, ticket médio), além de visualizações por categoria, região, segmento e evolução temporal. Não é necessário clonar o repositório nem executar o notebook para visualizá-lo.



● Descrição das etapas
1.Importação e compreensão dos dados:
○ Carregamento do dataset em ambiente de análise (ex.: Google Colab);
○ Exploração inicial da estrutura dos dados.


Arquivo:Desafio_extra2_Henrique_Tamaki.ipynb
Link GitHub:https://github.com/henriquetamaki-max/Trilha_analise_dados.git
Link Google Colab:https://colab.research.google.com/drive/16gKGgmnHvZmUXkT4b4_FKubxHGlc1E9C?usp=sharing
Indice Colab: 1. Importação e compreensão dos dados
 

2. Tratamento e preparação dos dados:
○ Verifi cação e tratamento de valores nulos ou duplicados;
○ Conversão de tipos de dados (datas e valores numéricos);
○ Organização e padronização das colunas;
○ Identifi cação e tratamento de possíveis outliers.


Arquivo:Desafio_extra2_Henrique_Tamaki.ipynb
Link GitHub:https://github.com/henriquetamaki-max/Trilha_analise_dados.git
Link Google Colab:https://colab.research.google.com/drive/16gKGgmnHvZmUXkT4b4_FKubxHGlc1E9C?usp=sharing
Indice Colab: 2. Tratamento e preparação dos dados


3. Análise exploratória:
○ Aplicação de filtros, ordenações e agrupamentos (GroupBy);
○ Análise das variáveis relevantes do dataset;
○ Geração de visualizações gráficas para apoiar a interpretação dos dados;
○ Investigação de relações entre variáveis (ex.: desconto vs lucro).


Arquivo:Desafio_extra2_Henrique_Tamaki.ipynb
Link GitHub:https://github.com/henriquetamaki-max/Trilha_analise_dados.git
Link Google Colab:https://colab.research.google.com/drive/16gKGgmnHvZmUXkT4b4_FKubxHGlc1E9C?usp=sharing
Indice Colab: 3. Analise Exploratoria


● Principais decisões tomadas durante o tratamento dos dados

O dataset utilizado foi o Sample - Superstore (9.994 linhas × 21 colunas), carregado via KaggleHub no Google Colab com encoding latin-1 para correção de caracteres especiais. Na fase de avaliação inicial, constatou-se que o dataset estava íntegro: nenhum valor nulo e nenhuma linha duplicada, o que dispensou imputação ou remoção por duplicidade. A partir disso, as decisões de preparação foram:

Conversão de tipos: as colunas Order Date e Ship Date foram convertidas de object para datetime64, e as colunas numéricas (Sales, Quantity, Discount, Profit) foram garantidas em tipos numéricos com pd.to_numeric para permitir cálculos confiáveis.

Padronização de colunas: todos os nomes foram convertidos para snake_case (minúsculas, sem espaços e com hífens substituídos por underscore), e os campos textuais tiveram espaços extras removidos via strip(), garantindo consistência nos agrupamentos.

Criação de colunas derivadas: foi criada a coluna dias_para_entrega (ship_date − order_date) e, posteriormente, a coluna pct_lucro (profit / sales), ambas fundamentais para análises de eficiência logística e rentabilidade.

Tratamento de outliers (método IQR): aplicado sobre sales, quantity, discount e profit. A decisão foi remover apenas os outliers extremos de sales e profit, mantendo discount e quantity originais por serem categóricos/discretos por natureza. O resultado foi um dataset limpo (df_clean) com 7.874 linhas, equivalente à remoção de 21,2% dos registros — preservando o comportamento típico do negócio sem ruído de transações atípicas.

Enriquecimento temporal: criação das colunas ano, mes e ano_mes para suportar análises de sazonalidade e evolução. O dataset final foi exportado em Local_Superstore_EDA.csv (25 colunas).



● Principais insights obtidos a partir da análise exploratória e/ou do dashboard

Dashboard Looker Studio: https://datastudio.google.com/s/lnKD84Ug4OE


Composição do faturamento: Office Supplies lidera em volume de pedidos (5.281) e em margem média (16,7%), enquanto Furniture é a categoria de pior desempenho relativo (margem de apenas 11,4%), puxada para baixo por sub-categorias deficitárias.

Sub-categorias problemáticas: Binders (-18,5%) e Tables (-3,2%) operam com margem média negativa, indicando que descontos agressivos estão corroendo o resultado. Em contraponto, Labels (42,9%), Paper (42,3%) e Envelopes (42,0%) são as mais rentáveis e merecem foco de expansão.

Disparidade regional: a região West concentra a maior receita (US$ 209k) e melhor margem (24,8%), enquanto Central apresenta margem média negativa (-4,4%) — claro alerta para revisão da política comercial naquela região.

Relação Desconto × Lucro: a correlação de Pearson revelou tendência negativa entre desconto e lucro. Faixas de desconto acima de 20% já produzem lucro médio negativo, e descontos a partir de 30% geram prejuízo consistente. Esse é o achado mais acionável da análise: existe um teto saudável de desconto em torno de 20%.

Segmento mais rentável: apesar de Consumer gerar maior receita absoluta (US$ 298k), o segmento Home Office apresenta a maior margem média (17,2%), sugerindo oportunidade de priorização estratégica.

Sazonalidade: as vendas crescem ano a ano, com picos consistentes no 4º trimestre (especialmente novembro e dezembro), refletindo o efeito de fim de ano. O lucro acompanha o crescimento das vendas, mas com volatilidade mensal causada pelos descontos.

Política de descontos para grandes clientes: a análise mostrou correlação muito fraca entre volume de compras e desconto recebido, indicando que os melhores clientes não recebem necessariamente os maiores descontos — há espaço para uma política de fidelização mais estruturada.

Logística: o tempo médio de entrega é de 4 dias (mín. 0, máx. 7), com Standard Class dominando o volume (4.719 pedidos) e mantendo margem saudável de 14,7%, sinalizando boa eficiência operacional padrão.


