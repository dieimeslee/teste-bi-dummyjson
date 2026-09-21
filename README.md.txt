# Desafio Técnico - Analista de BI Pleno (DummyJSON)

## 1. Visão Geral da Arquitetura
- **Linguagem & Bibliotecas:** Python (requests, pandas, sqlite3) para o processo de ETL.
- **Armazenamento:** SQLite, estruturado localmente via arquivo `ecommerce_analytics.db`.
- **Camada Semântica & Visualização:** Power BI Desktop com cálculos desenvolvidos em DAX.

## 2. Processo de Extração e Tratamento (ETL)
- **Consumo de API:** Os endpoints `/products`, `/carts` e `/users` foram consumidos com paginação dinâmica (`limit` e `skip`), garantindo a extração de 100% da base.
- **Tratamento de Dados:** Normalização dos registros de carrinhos para o grão de item vendido e limpeza de dados cadastrais dos clientes.

## 3. Modelagem de Dados
Foi adotado o esquema dimensional **Star Schema**:
- `dim_products`: Atributos do produto (categoria, marca, preço de catálogo, estoque).
- `dim_users`: Dados cadastrais e demográficos (nome, idade, gênero, cidade, estado).
- `fato_vendas_itens`: Tabela fato no nível de item de pedido, contendo métricas aditivas (`quantity`, `gross_amount`, `discount_amount`, `net_amount`).

## 4. Principais Insights de Negócio
- **Concentração de Vendas:** As categorias líderes respondem por parcela majoritária do faturamento.
- **Impacto dos Descontos:** A análise demonstra que descontos acima de determinado percentual não necessariamente geram incremento proporcional de volume, apontando oportunidade de ajuste de margem.
- **Base de Clientes:** Identificada alta concentração de receita em um número reduzido de compradores, sugerindo a criação de estratégias de retenção/fidelidade.

## 5. Como Executar o Projeto
1. Executar o notebook `notebooks/pipeline_etl_analise.ipynb` para recriar a base SQLite.
2. Abrir o arquivo `bi/dashboard_ecommerce.pbix` no Power BI Desktop para navegar pelo painel.