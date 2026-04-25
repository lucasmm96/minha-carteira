# Ranking

## Princípios gerais

* Todos os indicadores devem ser obtidos via API do Yahoo Finance
* Quando não disponíveis diretamente, devem ser calculados a partir de:
  * incomeStatement
  * balanceSheet
  * cashflow
  * price data
* Indicadores inconsistentes ou ausentes devem ser ignorados no score final
* Normalização recomendada: percentil por indicador

# AÇÕES

## Valuation

* Dividend Yield
  * Fórmula: `dividendYield` (direto da API)
* P/L
  * Fórmula: `trailingPE`
* P/VP
  * Fórmula: `priceToBook`
* EV/EBITDA
  * Fórmula: `enterpriseToEbitda`
* P/S (substitui P/SR)
  * Fórmula: `priceToSalesTrailing12Months`

## Eficiência

* Margem Bruta
  * Fórmula: `grossMargins`
* Margem Operacional (substitui M. EBIT)
  * Fórmula: `operatingMargins`
* Margem Líquida
  * Fórmula: `profitMargins`

## Endividamento

* Dívida / Patrimônio
  * Fórmula: `debtToEquity`
* Dívida / EBITDA (quando disponível)
  * Fórmula: `totalDebt / ebitda`

## Rentabilidade

* ROE
  * Fórmula: `returnOnEquity`

* ROA
  * Fórmula: `returnOnAssets`

## Crescimento (aproximado)

* Crescimento Receita
  * Fórmula: `revenueGrowth`
* Crescimento Lucro
  * Fórmula: `earningsGrowth`

# FIIs (adaptado)

## Valuation

* Dividend Yield
  * Fórmula: `dividendYield`

* P/VP
  * Fórmula: `priceToBook`

## Liquidez

* Volume médio
  * Fórmula: `averageVolume`

## Crescimento (proxy)

* Crescimento preço (proxy de CAGR)
  * Fórmula:
    `(preço atual / preço 3 anos atrás)^(1/3) - 1`

# SCORE FINAL

## Pesos sugeridos

Ações:
* Valuation: 30%
* Eficiência: 25%
* Rentabilidade: 20%
* Endividamento: 15%
* Crescimento: 10%

FIIs:
* Valuation: 40%
* Liquidez: 20%
* Crescimento: 40%

## Cálculo
1. Normalizar cada indicador (percentil)
2. Inverter indicadores negativos (ex: dívida)
3. Aplicar pesos
4. Somar

Score final:
`Score = Σ (peso × indicador_normalizado)`
