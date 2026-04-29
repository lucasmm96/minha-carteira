# Ranking

## Objetivo

Definir de forma determinística como o sistema classifica os ativos da carteira do usuário com base em indicadores fundamentalistas.

O ranking tem caráter exclusivamente informativo e serve como apoio à decisão do usuário.

## Princípios Gerais

* O ranking deve considerar apenas ativos presentes na carteira do usuário
* Devem existir dois rankings independentes:
  * Ações
  * FIIs
* O ranking não deve tomar decisões, apenas ordenar ativos
* O cálculo deve utilizar exclusivamente dados disponíveis via Yahoo Finance API
* Indicadores indisponíveis devem ser ignorados (não substituídos por valores arbitrários)

## Fonte de Dados

Os dados devem ser obtidos via Yahoo Finance API.

Quando necessário, devem ser derivados de:

* incomeStatement
* balanceSheet
* cashflow
* price data

## Normalização

Todos os indicadores devem ser normalizados antes da agregação.

### Método

* Utilizar normalização por percentil dentro do conjunto de ativos comparados

## Direção dos Indicadores

Os indicadores devem ser classificados como:

### Positivos (quanto maior, melhor)

* Dividend Yield
* Margens
* ROE / ROA
* Crescimento

### Negativos (quanto menor, melhor)

* P/L
* P/VP
* EV/EBITDA
* Dívida

Indicadores negativos devem ser invertidos após normalização.

# Ranking de Ações

## Indicadores

### Valuation

* Dividend Yield
  Fonte: `dividendYield`

* P/L
  Fonte: `trailingPE`

* P/VP
  Fonte: `priceToBook`

* EV/EBITDA
  Fonte: `enterpriseToEbitda`

* P/S
  Fonte: `priceToSalesTrailing12Months`

### Eficiência

* Margem Bruta
  Fonte: `grossMargins`

* Margem Operacional
  Fonte: `operatingMargins`

* Margem Líquida
  Fonte: `profitMargins`

### Endividamento

* Dívida / Patrimônio
  Fonte: `debtToEquity`

* Dívida / EBITDA (quando disponível)
  Fórmula: `totalDebt / ebitda`

### Rentabilidade

* ROE
  Fonte: `returnOnEquity`

* ROA
  Fonte: `returnOnAssets`

### Crescimento

* Crescimento de Receita
  Fonte: `revenueGrowth`

* Crescimento de Lucro
  Fonte: `earningsGrowth`

## Pesos

* Valuation: 30%
* Eficiência: 25%
* Rentabilidade: 20%
* Endividamento: 15%
* Crescimento: 10%

# Ranking de FIIs

## Indicadores

### Valuation

* Dividend Yield
  Fonte: `dividendYield`

* P/VP
  Fonte: `priceToBook`

### Liquidez

* Volume médio
  Fonte: `averageVolume`

### Crescimento (Proxy)

* Crescimento de preço (aproximação de CAGR)

Fórmula:

```id="fii_cagr"
(preco_atual / preco_3_anos_atras)^(1/3) - 1
```

## Pesos

* Valuation: 40%
* Liquidez: 20%
* Crescimento: 40%

# Cálculo do Score

## Etapas obrigatórias

1. Coletar todos os indicadores disponíveis
2. Remover indicadores ausentes para cada ativo
3. Normalizar cada indicador (percentil)
4. Inverter indicadores negativos
5. Aplicar pesos por categoria
6. Somar os resultados

## Fórmula Final

```id="score_final"
Score = Σ (peso_categoria × média_indicadores_categoria)
```

## Tratamento de Dados Ausentes

* Indicadores ausentes devem ser ignorados
* O score deve ser calculado apenas com os indicadores disponíveis
* Não preencher valores ausentes artificialmente

## Ordenação

* Os ativos devem ser ordenados por score final (maior para menor)

## Comportamento Esperado

O sistema deve:

* recalcular o ranking sempre que houver atualização de dados
* manter consistência entre execuções
* garantir que ativos comparados pertencem ao mesmo grupo (Ação ou FII)

## Comportamento da IA

A IA deve:

* utilizar o ranking apenas como referência
* não tomar decisões automáticas com base no ranking
* não alterar pesos ou fórmulas
* respeitar a separação entre ranking de ações e FIIs

## Restrições

* Não utilizar dados fora do Yahoo Finance
* Não inferir indicadores inexistentes
* Não misturar ativos de tipos diferentes
* Não alterar pesos sem definição explícita

## Observações

* Este ranking é uma aproximação do modelo utilizado por plataformas como Status Invest, adaptado às limitações da API do Yahoo Finance.
* Ele deve ser interpretado como ferramenta de apoio e não como decisão final.
* Este documento deve ser considerado a fonte única de verdade para classificação de ativos.

## Limitações

* O ranking pode apresentar baixa precisão quando o número de ativos comparados for pequeno
* Recomenda-se interpretar o ranking com cautela em carteiras com poucos ativos

