# Comportamento do Sistema

## Objetivo

Definir o comportamento global, propósito e regras de funcionamento do sistema MinhaCarteira.

Este documento deve ser utilizado como base para tomada de decisão por IA e implementação do sistema.

## Propósito

O sistema MinhaCarteira tem como objetivo:

* Registrar e controlar ativos financeiros de renda variável (FIIs e Ações)
* Centralizar informações da carteira do usuário
* Exibir dados e análises de forma estruturada
* Apoiar o processo de decisão do usuário

O sistema NÃO deve tomar decisões automaticamente.
A decisão final de compra ou venda é sempre do usuário.

## Escopo

O sistema opera exclusivamente com:

* Ativos de renda variável listados na bolsa brasileira

  * FIIs
  * Ações

O sistema deve trabalhar apenas com:

* Ativos presentes na carteira do usuário

## Papel do Sistema

O sistema deve:

* Registrar movimentações (compra e venda)
* Consolidar posição da carteira
* Exibir métricas e dados relevantes
* Apresentar rankings informativos
* Exibir proporção entre classes de ativos
* Fornecer visualizações (dashboard)

O sistema NÃO deve:

* Executar operações automaticamente
* Sugerir ações de forma imperativa
* Tomar decisões pelo usuário

## Papel do Usuário

O usuário é responsável por:

* Escolher quais ativos adicionar à carteira
* Registrar movimentações
* Interpretar os dados apresentados
* Decidir o que comprar ou vender

## Modelo de Decisão

O processo de decisão do usuário é suportado por dois fatores principais:

### 1. Proporção da Carteira

O sistema deve exibir:

* Percentual investido em FIIs
* Percentual investido em Ações

A proporção é apenas informativa.

O sistema NÃO deve impor regras de balanceamento.

### 2. Ranking de Ativos

O sistema deve possuir:

* Ranking de FIIs
* Ranking de Ações

Regras:

* Rankings devem ser independentes
* Devem considerar apenas ativos da carteira do usuário
* Devem ser calculados com base em `ranking.md`
* Devem ser exibidos de forma clara e ordenada

Objetivo do ranking:

* Indicar quais ativos apresentam melhores indicadores no momento atual

O ranking é apenas informativo.

## Estratégia Implícita

O sistema deve refletir a seguinte estratégia:

* Equilíbrio entre renda e qualidade
* Avaliação baseada em múltiplos indicadores (valuation, crescimento, eficiência, endividamento)
* Reinvestimento de proventos definido manualmente pelo usuário

## Frequência de Uso

O sistema deve ser utilizado de forma:

* Sob demanda
* Principalmente em momentos de decisão de investimento

O sistema não precisa operar em tempo real contínuo para o usuário.

## Dados de Mercado

O sistema deve:

* Ter acesso a dados públicos de ativos da bolsa brasileira
* Permitir busca e seleção de ativos

Ao adicionar um ativo:

* O sistema deve sugerir o preço atual automaticamente
* O sistema deve permitir edição manual de:

  * preço
  * data

Isso permite:

* Registro histórico
* Correção de dados

## Integridade dos Dados

O sistema deve garantir:

* Cada usuário acessa apenas seus próprios dados
* Dados não são compartilhados entre usuários
* Consistência entre movimentações e carteira

## Comportamento Esperado (IA)

A IA que utilizar este sistema deve:

* Interpretar os dados como apoio à decisão
* Nunca assumir controle da decisão do usuário
* Respeitar as regras definidas neste documento
* Utilizar o ranking apenas como referência

## Restrições

* Não automatizar decisões de investimento
* Não inferir comportamento do usuário além do definido
* Não utilizar dados externos não especificados
* Não alterar regras de ranking definidas externamente

## Observações

Este documento define o comportamento global do sistema.

Outros documentos complementares:

* `ranking.md` → definição do ranking
* `movimentacoes.md` → regras de registro
* `carteira.md` → cálculo de posição
* `dados-de-mercado.md` → origem e atualização de dados
* `autenticacao.md` → controle de acesso
* `frontend.md` → regras de design

Este documento deve ser considerado a fonte única de verdade para o comportamento do sistema.
