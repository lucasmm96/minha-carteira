# Movimentações

## Objetivo

Definir de forma determinística como o sistema registra, interpreta e processa movimentações de ativos.

Este documento é responsável por definir o comportamento do histórico financeiro do sistema.

## Definição

Movimentação é o registro de uma operação de compra ou venda de um ativo na carteira do usuário.

Uma movimentação representa uma mudança na quantidade de um ativo.

## Tipos de Movimentação

* Compra
* Venda

Nenhum outro tipo deve ser considerado neste documento.

## Estrutura de Dados

Cada movimentação deve conter obrigatoriamente:

* data: data da operação (formato YYYY-MM-DD)
* tipo: "compra" ou "venda"
* ativo_id: identificador interno do ativo (referência ao banco de dados)
* descricao: nome descritivo do ativo
* preco_unitario: valor unitário do ativo no momento da operação
* quantidade: número inteiro de unidades negociadas

## Regras Gerais

* Toda movimentação deve estar associada a um ativo existente
* Quantidade deve ser sempre um número inteiro positivo
* Preço unitário deve ser um número positivo
* Movimentações devem ser ordenadas por:
  1. data (ascendente)
  2. ordem de inserção (em caso de empate)
* Toda movimentação deve referenciar um ativo via ativo_id
* Dados como ticker e nome devem ser obtidos via relacionamento com o ativo

## Regras de Compra

Ao registrar uma compra:

* A quantidade do ativo deve aumentar
* O preço médio deve ser recalculado utilizando média ponderada

### Fórmula do Preço Médio

```id="pm_formula"
novo_preco_medio =
((preco_medio_atual * quantidade_atual) + (preco_unitario * quantidade_compra))
/ (quantidade_atual + quantidade_compra)
```

## Regras de Venda

Ao registrar uma venda:

* A quantidade do ativo deve diminuir
* O preço médio NÃO deve ser alterado
* Não deve ser realizado cálculo de lucro ou prejuízo neste momento

## Regras de Integridade

* Não é permitido vender mais do que a quantidade disponível
* A quantidade total de um ativo nunca pode ser negativa
* O sistema deve validar todas as movimentações antes de aplicar alterações

## Regra de Zeragem de Posição

Quando a quantidade de um ativo atingir zero:

* O preço médio deve ser resetado
* Uma nova compra deve iniciar um novo cálculo de preço médio

## Cálculo de Quantidade

A quantidade total de um ativo deve ser:

```id="quantidade_formula"
quantidade_total = soma(compras) - soma(vendas)
```

## Edição e Exclusão

O sistema deve permitir:

* edição de movimentações existentes
* exclusão de movimentações

Regras:

* Após edição ou exclusão, todos os cálculos devem ser reprocessados
* A ordem cronológica deve ser mantida
* A consistência dos dados deve ser garantida

## Impacto na Carteira

Movimentações são a única fonte de verdade para:

* quantidade de ativos
* preço médio

Outros dados, como:

* valor atual
* valorização
* lucro/prejuízo

devem ser calculados em outros módulos (ex: carteira.md)

## Comportamento Esperado (IA)

A IA deve:

* processar movimentações em ordem cronológica
* recalcular corretamente o preço médio após cada compra
* nunca alterar preço médio em vendas
* nunca permitir inconsistências (quantidade negativa)
* respeitar integralmente as regras definidas neste documento

## Restrições

* Não armazenar valores derivados (ex: valor total investido)
* Não calcular lucro/prejuízo neste módulo
* Não inferir dados não fornecidos
* Não alterar regras de cálculo

## Observações

Este documento define exclusivamente o comportamento de movimentações.

Outros conceitos relacionados devem ser definidos em:

* carteira.md → cálculo de posição e valorização
* dados-de-mercado.md → preço atual dos ativos
* comportamento-do-sistema.md → lógica global do sistema

Este documento deve ser tratado como fonte única de verdade para o histórico de operações.
