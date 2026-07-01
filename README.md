# Análise Exploratória e Pré-processamento para Identificação de Churn em Clientes da API PIX

![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=white)
![Scikit--learn](https://img.shields.io/badge/Scikit--learn-F7931E?logo=scikitlearn&logoColor=white)
![Data Analytics](https://img.shields.io/badge/Data%20Analytics-0052CC?logo=apache&logoColor=white)

## Resumo do Projeto

| Item | Descrição |
|---|---|
| **Tema** | Churn de clientes em uma API PIX |
| **Tipo de análise** | EDA, qualidade dos dados e pré-processamento |
| **Granularidade** | Cliente |
| **Base utilizada** | Base sintética controlada, gerada para execução do notebook |
| **Variável-alvo** | `churn` — 1 = churn, 0 = não churn |
| **Foco técnico** | Análise exploratória, Data Quality e preparação para Machine Learning |

---

## Resumo Executivo

Este projeto foi desenvolvido no contexto da Pós-Graduação em **Data Science & Analytics (PUC-Rio)**, aplicando boas práticas de análise exploratória e pré-processamento ao problema de churn em clientes de uma **API PIX**.

A proposta é identificar sinais associados à evasão de clientes a partir de variáveis de uso transacional, recorrência, valor movimentado, estabilidade operacional, tempo de relacionamento e adoção de recursos complementares.

O notebook não realiza treinamento de modelos de Machine Learning nesta versão. O foco está na estruturação analítica do problema, no diagnóstico de qualidade dos dados e na construção de um pipeline de pré-processamento reprodutível para apoiar uma futura etapa de modelagem preditiva.

---

## Arquitetura da Solução

```text
                         ┌──────────────────────────────┐
                         │ Base de Clientes API PIX      │
                         │ Arquivo local ou base sintética│
                         └───────────────┬──────────────┘
                                         │
                                         ▼
                         ┌──────────────────────────────┐
                         │ Padronização e Validação      │
                         │ Colunas | Tipos | Target      │
                         └───────────────┬──────────────┘
                                         │
                                         ▼
┌──────────────────┐   ┌──────────────────┐   ┌────────────────────────┐
│ EDA              │ → │ Data Quality      │ → │ Pré-processamento       │
│ Distribuições    │   │ Nulos e escalas   │   │ Imputação | Scaling     │
│ Boxplots | Corr. │   │ Consistência      │   │ One-Hot Encoding        │
└──────────────────┘   └──────────────────┘   └───────────┬────────────┘
                                                           │
                                                           ▼
                         ┌──────────────────────────────┐
                         │ Dataset Preparado            │
                         │ Base para Modelagem Futura   │
                         └──────────────────────────────┘
```

---

## Problema

Em produtos financeiros baseados em **API PIX**, a perda de clientes pode impactar volume transacional, faturamento, previsibilidade operacional e relacionamento comercial.

Clientes com baixa recorrência, queda de uso, maior incidência de falhas ou menor maturidade de relacionamento podem apresentar maior risco de churn. O projeto busca identificar esses sinais por meio de análise exploratória e preparação estruturada dos dados.

---

## Objetivo

Realizar uma análise exploratória e construir um pipeline de pré-processamento para apoiar a identificação de padrões associados ao churn de clientes da API PIX, preparando a base para uma futura etapa de classificação supervisionada.

---

## Questões Analíticas

O projeto buscou responder questões como:

- Clientes com menor volume transacional apresentam maior propensão ao churn?
- Clientes com maior tempo desde a última transação indicam maior risco de evasão?
- Taxas de erro e falhas operacionais estão associadas ao churn?
- Clientes com menor tempo de relacionamento apresentam maior risco?
- A adoção de webhook pode estar relacionada à retenção?
- Quais tratamentos são necessários antes de uma futura modelagem preditiva?

---

## Fonte dos Dados

O notebook foi estruturado para utilizar automaticamente um arquivo local, caso esteja disponível no ambiente. Na ausência desse arquivo, é gerada uma **base sintética controlada** com estrutura compatível ao problema de churn em clientes de API PIX.

Na execução analisada, foi utilizada a base sintética gerada automaticamente, com:

- **800 clientes**
- **15 colunas**
- variável-alvo `churn`
- atributos transacionais, financeiros, operacionais e cadastrais

Principais atributos:

- `tempo_base_meses`
- `transacoes_30d`
- `valor_total_30d`
- `dias_desde_ultima_transacao`
- `taxa_erro_30d`
- `qtd_falhas_30d`
- `ticket_medio_30d`
- `possui_webhook`
- `status_cliente`
- `churn`

---

## Tecnologias Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Pipeline
- ColumnTransformer
- SimpleImputer
- MinMaxScaler
- StandardScaler
- OneHotEncoder

---

## Competências Técnicas Aplicadas

- Análise Exploratória de Dados (EDA)
- Data Quality
- Pré-processamento de dados
- Tratamento de valores nulos
- Normalização e padronização
- Codificação de variáveis categóricas
- Construção de pipelines com Scikit-learn
- Interpretação analítica orientada a negócio
- Preparação de base para Machine Learning
- Comunicação de hipóteses e resultados

---

## Principais Entregas

- Estruturação do problema de churn no contexto de API PIX;
- Definição de hipóteses analíticas;
- Carga automática de dados ou geração de base sintética controlada;
- Padronização de nomes de colunas;
- Análise da distribuição da variável-alvo;
- Estatísticas descritivas dos atributos numéricos;
- Visualizações com histogramas, boxplots e matriz de correlação;
- Diagnóstico de valores nulos;
- Normalização e padronização dos atributos numéricos;
- Pipeline reprodutível de pré-processamento com variáveis numéricas e categóricas.

---

## Principais Análises

A base analisada possui 800 clientes e distribuição praticamente balanceada da variável-alvo:

- `churn = 0`: 404 clientes;
- `churn = 1`: 396 clientes.

Foram identificados valores nulos em três atributos, todos com 2% de ausência:

- `segmento`
- `ticket_medio_30d`
- `taxa_erro_30d`

As hipóteses analisadas indicaram sinais coerentes com o problema de churn:

- clientes em churn apresentaram maior média de dias desde a última transação;
- clientes em churn apresentaram maior taxa média de erro;
- clientes em churn apresentaram maior média de falhas operacionais;
- clientes em churn apresentaram menor tempo médio de relacionamento;
- clientes sem churn apresentaram maior adoção de webhook.

O pipeline final de pré-processamento gerou uma matriz com **800 registros** e **29 atributos transformados**, pronta para uma futura etapa de modelagem.

---

## Qualidade dos Dados

Durante o notebook foram aplicadas etapas de qualidade e consistência, incluindo:

- padronização dos nomes das colunas;
- validação da presença da variável-alvo `churn`;
- identificação de variáveis numéricas e categóricas;
- diagnóstico de valores ausentes;
- imputação por mediana para variáveis numéricas;
- imputação por moda para variáveis categóricas;
- escalonamento com MinMaxScaler e StandardScaler;
- codificação One-Hot Encoding para variáveis categóricas.

Essas etapas tornam o fluxo mais organizado, reprodutível e adequado para evolução futura em Machine Learning.

---

## Limitações

A análise foi realizada com uma base sintética controlada, criada para permitir a execução completa do notebook na ausência de dados brutos reais. Portanto, os resultados devem ser interpretados como evidências exploratórias e validação do fluxo analítico, não como conclusões produtivas sobre clientes reais.

Além disso, esta versão não inclui treinamento de modelos de Machine Learning, concentrando-se em EDA, qualidade dos dados e pré-processamento.

---

## Possíveis Evoluções

- Substituir a base sintética por dados reais e históricos da API PIX;
- Criar novas features de recência, frequência e valor;
- Treinar modelos de classificação supervisionada;
- Comparar Logistic Regression, Random Forest e XGBoost;
- Avaliar métricas como recall, precision, F1-score e AUC;
- Tratar eventual desbalanceamento da variável-alvo em dados reais;
- Aplicar explicabilidade para identificar os fatores mais relevantes de churn;
- Construir dashboard de monitoramento de risco por cliente.

