# Dashboard

## Objetivo

Definir de forma determinística quais informações devem ser exibidas ao usuário e como devem ser organizadas na interface principal do sistema.

O dashboard é a principal visão do sistema e deve consolidar todas as informações relevantes da carteira de forma clara e estruturada.

## Estrutura Geral

O dashboard deve ser composto por uma única página contendo todas as informações.

* Estrutura fixa
* Sem modularidade dinâmica
* Todas as seções devem ser exibidas sempre que houver dados disponíveis

## Ordem das Seções

A ordem das seções deve ser fixa e seguir a sequência abaixo:

1. Resumo da carteira
2. Gráficos
3. Alocação
4. Ranking
5. Lista de ativos
6. Destaques

## 1. Resumo da Carteira

Deve ser exibido no topo do dashboard.

### Informações obrigatórias

* Valor total da carteira
* Valor total investido
* Lucro/prejuízo total (R$)
* Lucro/prejuízo total (%)

### Variação diária

Deve ser exibida.

#### Cálculo

```id="variacao_diaria"
variacao_diaria = preco_atual - preco_fechamento_anterior
```

#### Requisitos

* O sistema deve obter o preço de fechamento do dia anterior
* Deve indicar visualmente:

  * positivo (alta)
  * negativo (queda)

## 2. Gráficos

### Tipos obrigatórios

* Gráfico de pizza (alocação)
* Gráfico de barras (comparações)
* Gráfico de linha (evolução da carteira)

### Evolução da Carteira

Deve ser baseada em:

* histórico de movimentações
* histórico de preços

#### Regra

O valor da carteira ao longo do tempo deve considerar:

* quantidade de ativos em cada momento
* preço do ativo naquele momento

## 3. Alocação

Deve apresentar:

### Por tipo

* percentual em ações
* percentual em FIIs

### Por ativo

* percentual individual de cada ativo

### Base de cálculo

```id="alocacao_base"
valor_atual
```

## 4. Ranking

Devem ser exibidos dois rankings:

* Ranking de ações
* Ranking de FIIs

### Forma de exibição

* Tabela
* Cards

### Conteúdo

* Nome do ativo
* Score numérico
* Posição no ranking

### Quantidade

* Todos os ativos da carteira

## 5. Lista de Ativos

Deve ser exibida em formato de tabela.

### Dados exibidos

* Nome
* Quantidade
* Preço médio
* Valor atual

### Interação

* Clique em um ativo deve abrir tela de detalhes

## 6. Destaques

Deve apresentar:

* Melhor ativo
* Pior ativo

### Critério

* Baseado em valorização percentual (%)

## Atualização

O dashboard deve ser atualizado automaticamente.

### Regras

* Utilizar polling (10 segundos)
* Atualizar apenas quando:

  * o usuário estiver visualizando o dashboard
* Utilizar dados de `dados-de-mercado.md`

## Estados

### Sem dados

Quando não houver ativos:

* Exibir mensagem
* Sugerir ação (ex: adicionar ativo)

## Responsividade

* Deve seguir regras definidas em `frontend.md`
* Deve apresentar as mesmas informações em mobile e desktop

## Comportamento Esperado (IA)

A IA deve:

* respeitar a ordem das seções
* não omitir informações obrigatórias
* utilizar exclusivamente dados definidos em outros documentos
* não inventar métricas ou indicadores

## Restrições

* Não alterar cálculos definidos em outros documentos
* Não reorganizar seções
* Não ocultar dados relevantes
* Não adicionar elementos não definidos

## Dependências

* carteira.md → dados da carteira
* movimentacoes.md → histórico
* dados-de-mercado.md → preços
* ranking.md → classificação
* frontend.md → layout e design

## Observações

Este documento define exclusivamente a estrutura e conteúdo do dashboard.

Ele deve ser tratado como fonte única de verdade para a interface principal do sistema.
