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
* total de proventos acumulados

## Cálculo de Quantidade

A quantidade atual deve ser calculada com base em movimentacoes.md:

```id="quantidade_calc"
quantidade = soma(compras) - soma(vendas)
```

## Cálculo de Preço Médio

O preço médio deve seguir exatamente as regras definidas em movimentacoes.md.

## Cálculo de Valor Investido

O valor investido deve ser:

```id="investido_calc"
valor_investido = soma(compras) - soma(vendas)
```

Observação:

* Este valor representa o capital atualmente alocado no ativo
* Não representa custo histórico total

## Preço Atual

O preço atual deve:

* ser obtido de fonte externa (dados de mercado)
* ser atualizado em tempo real quando o mercado estiver aberto
* parar de atualizar quando o mercado estiver fechado

O sistema deve:

* indicar quando o mercado estiver fechado
* exibir o horário da última atualização

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

## Proventos

O sistema deve:

* calcular o total de proventos acumulados por ativo
* considerar todos os proventos desde a primeira compra

Regras:

* proventos NÃO devem alterar:

  * valor investido
  * valorização
* proventos devem ser exibidos apenas como informação adicional

## Consolidação da Carteira

O sistema deve calcular:

* total investido
* total atual
* lucro/prejuízo total (R$)
* lucro/prejuízo total (%)

### Fórmulas

```id="total_investido"
total_investido = soma(valor_investido de todos os ativos)
```

```id="total_atual"
total_atual = soma(valor_atual de todos os ativos)
```

```id="lucro_total"
lucro_total = total_atual - total_investido
```

```id="lucro_percentual"
lucro_percentual = (lucro_total / total_investido) * 100
```

## Alocação

O sistema deve calcular:

### Por tipo

* % em ações
* % em FIIs

### Por ativo

* % de cada ativo na carteira

### Base de cálculo

Todas as proporções devem ser baseadas em:

```id="base_alocacao"
valor_atual
```

## Ordenação

A ordenação padrão dos ativos deve ser:

* por nome (ordem alfabética)

## Destaque de Ativos

O sistema deve destacar ativos com base em:

* maior valorização percentual (%)

## Dados Faltantes

Caso o preço atual não esteja disponível:

* utilizar o último valor conhecido
* indicar discretamente que o dado pode estar desatualizado

## Precisão

Todos os valores devem ser exibidos com:

* 2 casas decimais

## Reprocessamento

A carteira deve ser recalculada:

* sempre do zero
* com base nas movimentações ordenadas

## Comportamento Esperado (IA)

A IA deve:

* recalcular todos os valores corretamente
* não armazenar dados derivados
* respeitar todas as fórmulas
* não incluir proventos na valorização
* não inferir dados não definidos

## Restrições

* Não armazenar dados calculados
* Não misturar proventos com valorização
* Não utilizar valores fora das regras definidas
* Não alterar lógica de cálculo

## Observações

Este documento depende diretamente de:

* movimentacoes.md → origem dos dados
* dados-de-mercado.md → preço atual

Este documento define exclusivamente o estado atual da carteira.

Deve ser tratado como fonte única de verdade para cálculos de posição e valorização.
