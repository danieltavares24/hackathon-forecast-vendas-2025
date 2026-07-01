# Hackathon Forecast Big Data 2025
Previsão de Vendas no Varejo com LightGBM

| Resultado | Valor |
|---|---|
| Colocação final | 17º lugar |
| Melhor WMAPE | 0.671013 |
| Modelo principal | LightGBM |
| Granularidade | Semanal por PDV e SKU |

Desafio técnico de previsão de demanda para reposição de produtos 
no varejo, com histórico de vendas de 2022 e previsão para janeiro 2023.

---

## Objetivo

Desenvolver um modelo de previsão de vendas semanais por Ponto de Venda 
(PDV) e SKU para apoiar o varejo na reposição de produtos, prevendo 
as cinco semanas de janeiro de 2023 com base no histórico de 2022.

---

## Metodologia

### Pré-processamento
Unificação dos dados de transações, produtos e PDVs com agregação 
diária para granularidade semanal.

### Engenharia de Features

| Feature | Descrição |
|---|---|
| Lag 1-4 semanas | Vendas das semanas anteriores |
| Janela móvel | Média, desvio padrão, mínimo e máximo das últimas 4 semanas |
| Features de data | Mês, semana do ano, flags de início e fim de mês |
| Popularidade | Média de vendas por produto e por PDV |

### Modelagem
Modelo principal: LightGBM com Gradient Boosting.

Validação temporal com as últimas 5 semanas de 2022 simulando 
o cenário real de previsão.

### Filtro de Submissão
Previsões geradas apenas para produtos ativos com vendas nos 
últimos 18 dias de 2022, reduzindo ruído e atendendo ao limite 
de 1,5 milhão de linhas da plataforma.

---

## Decisões Técnicas

**LightGBM:** escolhido pela eficiência em grandes volumes de dados 
e velocidade de treinamento superior ao XGBoost.

**Feature de Popularidade:** diferenciação entre SKUs de alto giro 
e cauda longa por PDV — uma das features de maior impacto no modelo.

**Filtro de Atividade:** estratégia de limpeza de ruído focando 
o modelo onde a probabilidade de venda era real.

---

## Stack Tecnológica

- **Linguagem:** Python
- **Modelo:** LightGBM
- **Manipulação de dados:** Pandas, NumPy
- **Formato de submissão:** Parquet

---

## Estrutura do Repositório

hackathon-forecast-vendas-2025/
├── Hackathon_Forecast_Big_Data_2025.ipynb  # Notebook completo da solução
├── hackathon_forecast_big_data_2025.py     # Script para execução local
├── submissao.parquet                       # Arquivo de submissão gerado
├── requirements.txt                        # Dependências do projeto
└── README.md

---

## Como Reproduzir

```bash
pip install -r requirements.txt
```

Abra o notebook no Google Colab ou Jupyter, faça upload dos arquivos:
- transacoes_2022.parquet
- cadastro_produtos.parquet
- cadastro_pdvs.parquet

Execute todas as células em ordem. O arquivo submissao.parquet 
será gerado ao final.

---

© 2026 Daniel Tavares de França | Visão Computacional & Machine Learning
