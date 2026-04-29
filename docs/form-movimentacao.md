# Formulário de Movimentação

## Objetivo

Definir o comportamento do formulário de registro de movimentações.

## Campos

* ativo (seleção via busca)
* tipo (compra ou venda)
* quantidade
* preço unitário
* data

## Comportamento

### Seleção de ativo

* busca via API
* seleção obrigatória

### Preenchimento automático

* ao selecionar ativo:

  * sugerir preço atual

### Edição manual

* usuário pode editar:

  * preço
  * data

## Validação

* quantidade > 0
* preço > 0
* ativo válido
* não permitir venda acima da quantidade

## Submissão

* deve criar nova movimentação
* deve reprocessar carteira

## Edição

* deve permitir edição de movimentações existentes

## Exclusão

* deve permitir exclusão
* deve reprocessar carteira

## Comportamento da IA

* validar antes de salvar
* não permitir inconsistência
* respeitar regras de `movimentacoes.md`
