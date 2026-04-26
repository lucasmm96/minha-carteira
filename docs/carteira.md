# Carteira

## Objetivo

Definir de forma determinística como o sistema calcula e representa o estado atual da carteira do usuário.

Este documento é responsável por transformar o histórico de movimentações em informações consolidadas e atualizadas.

## Definição

A carteira representa o estado atual dos ativos do usuário.

A carteira NÃO armazena dados próprios.
Todos os valores devem ser derivados de:

* movimentacoes.md
* dados de mercado (preço atual)

## Estrutura da Carteira

A carteira deve ser organizada em:

* Ações
* FIIs

Cada grupo deve conter apenas ativos com quantidade maior que zero.

Ativos com quantidade zero:

* devem permanecer no sistema
* NÃO devem ser exibidos na carteira principal

## Estrutura por Ativo

Para cada ativo, o sistema deve calcular:

* ativo
* descricao
* tipo (ação ou FII)
* quantidade atual
* preco medio
* valor investido
* preco atual
* valor atual
* valorizacao (R$)
* valorizacao (%)

## Cálculo de Quantidade

```id="quantidade_calc"
quantidade = soma(compras) - soma(vendas)
```

## Cálculo de Preço Médio

O preço médio deve seguir exatamente as regras definidas em movimentacoes.md.

## Cálculo de Valor Investido

```id="investido_calc"
valor_investido = soma(compras) - soma(vendas)
```

### Observação Importante

* Este valor representa o capital atualmente alocado no ativo
* NÃO representa o custo histórico total investido
* NÃO deve ser interpretado como custo médio clássico de mercado

## Preço Atual

* Obtido via dados-de-mercado.md

## Cálculo de Valor Atual

```id="valor_atual_calc"
valor_atual = quantidade * preco_atual
```

## Cálculo de Valorização

### Em valor (R$)

```id="valorizacao_rs"
valorizacao = valor_atual - valor_investido
```

### Em percentual (%)

```id="valorizacao_pct"
valorizacao_percentual = (valorizacao / valor_investido) * 100
```

## Consolidação da Carteira

O sistema deve calcular:

* total investido
* total atual
* lucro/prejuízo total (R$)
* lucro/prejuízo total (%)

## Alocação

* % em ações
* % em FIIs
* % por ativo

Base:

```id="base_alocacao"
valor_atual
```

## Ordenação

* por nome (alfabética)

## Destaque de Ativos

* baseado em valorização (%)

## Dados Faltantes

* usar último valor disponível
* indicar discretamente possível desatualização

## Precisão

* 2 casas decimais

## Reprocessamento

* sempre recalcular do zero

## Comportamento Esperado (IA)

* não armazenar dados derivados
* respeitar fórmulas
* não inferir dados

## Restrições

* não armazenar dados calculados
* não alterar lógica

## Observações

Dependências:

* movimentacoes.md
* dados-de-mercado.md

Este documento define exclusivamente o estado atual da carteira.
