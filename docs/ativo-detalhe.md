# Detalhe do Ativo

## Objetivo

Definir a estrutura e comportamento da tela de detalhes de um ativo.

## Acesso

* Deve ser acessado ao clicar em um ativo no dashboard

## Informações Exibidas

### Dados principais

* ticker
* nome
* tipo

### Dados da posição

* quantidade atual
* preço médio
* valor investido
* valor atual
* valorização (R$)
* valorização (%)

## Gráficos

### Histórico de preço

* gráfico de linha
* baseado em dados históricos

### Evolução da posição

* valor do ativo ao longo do tempo
* baseado em:

  * movimentações
  * histórico de preços

## Histórico de Movimentações

* lista completa de movimentações do ativo
* ordenação:

  * data
  * ordem de inserção

## Ações do Usuário

* adicionar movimentação
* editar movimentação
* excluir movimentação

## Atualização

* deve seguir regras de `dados-de-mercado.md`

## Comportamento da IA

* não inferir dados
* utilizar apenas dados definidos
* respeitar regras de cálculo

## Dependências

* carteira.md
* movimentacoes.md
* dados-de-mercado.md
