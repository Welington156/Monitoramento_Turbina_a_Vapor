# Projeto Power BI: Monitoramento de Sistemas de Turbina a Vapor

## 🚀 Visão Geral

Este repositório apresenta um projeto completo em Power BI para monitoramento e análise de sistemas de turbina a vapor, focando nas linhas de admissão, extração, sangria e exaustão. O objetivo é demonstrar boas práticas de ETL no Power Query, modelagem de dados em star schema, criação de métricas avançadas em DAX e construção de dashboards interativos com foco em storytelling.

## 🛠️ ETL no Power Query

Importação: Carregamento do CSV bruto.

Renomeação de Colunas: Padronização dos nomes para Date, BLS1P_A, BLS1P_B, etc.

Tratamento de Tipos: Conversão de Date para datetime e demais para número.

Limpeza: Preenchimento de nulos, remoção de outliers (valores negativos ou fora de curva).

Unpivot: Transformação de colunas de sensores em Attribute + Value para facilitar análise.

Tabelas Auxiliares: Criação de DimDate (calendário) e Dim_Sensor (metadados).

Detalhes do M Code estão em powerquery/ETL_Steps.md.

## 🗄️ Modelagem em Star Schema

Fatos (Fatos_Leituras): contém Date, SensorID e Value.

DimDate: calendário com Ano, Mês, Dia, Hora.

Dim_Sensor: descrição, unidade e categoria de cada sensor.

Relacionamentos:

DimDate[Date] (1) → (N) Fatos_Leituras[Date]

Dim_Sensor[SensorID] (1) → (N) Fatos_Leituras[SensorID]

O diagrama está em model/star_schema_diagram.png.

## 📊 Métricas e Análises em DAX

KPIs básicos: média, máximo, mínimo e contagem de leituras.

Análise de correlação:

Medidas de covariância e desvio padrão.

Cálculo de correlação (Pearson) entre quaisquer dois sensores via parâmetros "What-If".

Detecção de anomalias: Z-score para sinalizar valores fora de ±2 desvios-padrão.

Exemplos de fórmulas:

Média Valor = AVERAGE(Fatos_Leituras[Value])

Correlação XY = DIVIDE(
  [CovarXY],
  [StdevX] * [StdevY]
)

## 📈 Dashboard e Storytelling

O Power BI contém três páginas principais:

Visão Geral: KPIs e séries temporais das variáveis selecionadas.

Correlação: scatter plot interativo e card com valor de correlação entre sensores.

Anomalias: gráfico de linhas destacando pontos fora do padrão e tabelas de alertas.

Cada página possui slicers por intervalo de data e filtros por área (admissão, extração, sangria, exaustão).

Algumas screenshots estão em dashboard/screenshots/.
