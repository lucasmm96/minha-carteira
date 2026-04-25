# Dados de Mercado

## Objetivo

Definir de forma determinística como o sistema obtém, atualiza, armazena e valida dados de mercado dos ativos.

Este documento é responsável por garantir a consistência e confiabilidade dos preços utilizados no sistema.

## Definição

Dados de mercado representam informações externas sobre ativos financeiros, sendo o principal:

* preço atual do ativo

## Fonte de Dados

* Yahoo Finance

## Escopo de Dados

* acesso a todos ativos
* busca sob demanda

## Dados Necessários

### Dados em tempo real

* preço atual

### Dados históricos (OBRIGATÓRIO)

O sistema deve suportar consulta de dados históricos de preço.

#### Regras:

* Deve permitir acesso a preços passados (mínimo necessário para cálculo de crescimento)
* Deve suportar pelo menos:

  * preço atual
  * preço de 3 anos atrás (para ranking de FIIs)
* Pode utilizar dados históricos da API do Yahoo Finance

## Frequência de Atualização

* polling a cada 10 segundos
### Regras de Atualização
* A atualização deve ocorrer apenas quando:
  * o usuário estiver em uma tela que utiliza dados de mercado
* A atualização deve ser interrompida quando não houver necessidade

## Tipo de Atualização

* apenas ativos visíveis

## Horário de Mercado

* seguir horário da B3

## Cache

* TTL: 10 segundos

## Histórico de Preços (Local)

* manter histórico simples
* objetivo: fallback

## Fallback

* usar último valor

## Tratamento de Erros

* retry no próximo ciclo

## Precisão

* precisão máxima interna
* arredondamento só na UI

## Comportamento da IA

* utilizar dados atualizados sempre que disponíveis
* respeitar o cache e o TTL
* não ignorar falhas silenciosamente
* utilizar fallback quando necessário
* não inventar dados

## Restrições

* Não realizar chamadas excessivas fora do intervalo definido
* Não atualizar dados desnecessariamente
* Não armazenar dados redundantes
* Não depender de dados não verificados

## Observações

* necessário para carteira.md e ranking.md
