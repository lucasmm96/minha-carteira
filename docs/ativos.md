# Ativos

## Objetivo

Definir de forma determinística a estrutura, identificação e comportamento dos ativos dentro do sistema.

Este documento estabelece a entidade base utilizada por todos os módulos.

## Definição

Um ativo no sistema é a representação de um ticker da bolsa de valores brasileira.

O ativo:

* representa um instrumento financeiro real (ação ou FII)
* serve como referência para obtenção de dados externos
* não armazena dados de mercado diretamente

## Tipos de Ativos

O sistema deve suportar:

* Ações
* FIIs

Nenhum outro tipo deve ser considerado neste momento.

## Identificação

### Identificador principal

* O ativo deve ser identificado pelo seu ticker

Exemplos:

* ITSA4
* SAPR4F
* VGIR11

### Normalização

* O ticker deve ser sempre armazenado em maiúsculo
* Não deve haver distinção entre letras minúsculas e maiúsculas

### Ativos fracionários

* Ativos com sufixo "F" devem ser tratados como ativos distintos

Exemplo:

* ITSA4 ≠ ITSA4F

## Estrutura de Dados

O sistema deve armazenar localmente:

* ticker
* nome (descrição)
* tipo (ação ou FII)

## Dados Externos

Os seguintes dados NÃO devem ser armazenados no ativo:

* preço
* indicadores fundamentalistas
* volume
* dados históricos

Esses dados devem ser obtidos via `dados-de-mercado.md` e `ranking.md`.

## Origem dos Ativos

### Cadastro

* O ativo deve ser selecionado a partir de dados da API
* Não deve ser criado manualmente sem validação

### Busca

O sistema deve permitir:

* busca por nome
* busca por ticker

### Lista de Ativos

* A lista de ativos deve ser obtida sob demanda via API
* Não deve ser mantida uma lista local completa

## Validação

### Validação de ticker

* Todo ativo deve ser validado contra a API antes de ser aceito
* Não deve ser permitido cadastrar ativos inválidos

### Duplicidade

* Não deve ser permitido cadastrar o mesmo ativo mais de uma vez

## Tipo do Ativo

* O tipo do ativo deve ser definido manualmente no momento do cadastro
* O sistema não deve inferir automaticamente o tipo

## Relação com Outros Módulos

### Movimentações

* Um ativo pode existir sem movimentações
* Movimentações devem sempre referenciar um ativo válido

### Carteira

* A carteira deve considerar apenas ativos com movimentações
* Ativos sem posição não devem ser exibidos

### Dados de Mercado

* Dados de preço devem ser obtidos externamente
* O ativo não deve armazenar preços

### Ranking

* O ranking deve utilizar o ativo como referência
* Indicadores devem ser obtidos externamente

## Remoção de Ativos

* Um ativo pode ser removido do sistema
* A remoção não deve comprometer a integridade dos dados

## Exibição

O sistema deve exibir:

* ticker
* nome do ativo

## Comportamento Esperado (IA)

A IA deve:

* utilizar apenas ativos válidos
* não criar ativos arbitrariamente
* respeitar a estrutura definida
* não inferir dados inexistentes

## Restrições

* Não permitir ativos inválidos
* Não armazenar dados de mercado no ativo
* Não duplicar ativos
* Não inferir tipo automaticamente

## Observações

Este documento define a entidade base do sistema.

Ele é utilizado por:

* movimentacoes.md
* carteira.md
* dados-de-mercado.md
* ranking.md
* dashboard.md

Deve ser tratado como fonte única de verdade para definição de ativos.
