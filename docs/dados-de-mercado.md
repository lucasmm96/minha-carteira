# Dados de Mercado

## Objetivo

Definir de forma determinística como o sistema obtém, atualiza, armazena e valida dados de mercado dos ativos.

Este documento é responsável por garantir a consistência e confiabilidade dos preços utilizados no sistema.

## Definição

Dados de mercado representam informações externas sobre ativos financeiros, sendo o principal:

* preço atual do ativo

Esses dados são utilizados para cálculo de valor atual e valorização da carteira.

## Fonte de Dados

O sistema deve utilizar:

* Yahoo Finance como fonte principal de dados

Regras:

* A integração deve ser desacoplada (abstraída), permitindo substituição futura da fonte
* O sistema não deve depender de uma única implementação rígida

## Escopo de Dados

O sistema deve:

* permitir acesso a todos os ativos disponíveis na bolsa brasileira
* realizar busca de ativos sob demanda via API

## Dados Necessários

Para cada ativo, o sistema deve obter:

* preço atual

Nenhum outro dado é obrigatório neste módulo.

## Frequência de Atualização

A atualização deve ser feita utilizando polling.

### Definição de Polling

Polling consiste em realizar requisições periódicas para obter dados atualizados.

### Regras de Atualização

* Intervalo: a cada 10 segundos
* A atualização deve ocorrer apenas quando:

  * o usuário estiver em uma tela que utiliza dados de mercado
* A atualização deve ser interrompida quando não houver necessidade

## Tipo de Atualização

* A atualização deve ser feita apenas para ativos visíveis na interface
* Não deve atualizar ativos fora do contexto atual do usuário

## Horário de Mercado

O sistema deve considerar o horário oficial da B3.

### Regras:

* Quando o mercado estiver aberto:

  * dados devem ser atualizados continuamente (polling ativo)
* Quando o mercado estiver fechado:

  * a atualização deve ser interrompida
  * o sistema deve indicar que os dados não estão sendo atualizados
  * deve exibir o horário da última atualização

## Cache

O sistema deve utilizar cache para dados de mercado.

### Regras:

* TTL (tempo de vida): 10 segundos
* O cache deve ser invalidado automaticamente após o TTL
* Durante o TTL, o sistema deve reutilizar os dados armazenados

## Histórico de Preços

O sistema deve manter um histórico local simples de preços.

### Regras:

* armazenar últimos valores recentes
* não é necessário histórico completo (time series)
* objetivo: suporte a fallback e estabilidade

## Fallback

Quando não for possível obter dados atualizados:

* utilizar o último valor disponível
* indicar discretamente que o dado pode estar desatualizado

## Tratamento de Erros

Em caso de falha na API:

* não realizar retry imediato
* tentar novamente no próximo ciclo de polling
* exibir indicador discreto de erro

## Precisão

* Os valores devem ser armazenados com precisão máxima retornada pela API
* O arredondamento deve ocorrer apenas na exibição (2 casas decimais)

## Comportamento Esperado (IA)

A IA deve:

* utilizar dados atualizados sempre que disponíveis
* respeitar o cache e o TTL
* não ignorar falhas silenciosamente
* utilizar fallback quando necessário
* não inventar valores de mercado

## Restrições

* Não realizar chamadas excessivas fora do intervalo definido
* Não atualizar dados desnecessariamente
* Não armazenar dados redundantes
* Não depender de dados não verificados

## Observações

Este documento é dependência direta de:

* carteira.md → cálculo de valor atual e valorização

Este documento define exclusivamente a obtenção e atualização de dados externos.

Deve ser tratado como fonte única de verdade para preços de ativos.
