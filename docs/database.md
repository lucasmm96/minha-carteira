# Banco de Dados

## Objetivo

Definir de forma determinística a estrutura de dados do sistema MinhaCarteira.

Este documento estabelece:

* tabelas
* campos
* relações
* regras de integridade
* políticas de acesso

## Tecnologia

* PostgreSQL (via Supabase)
* Modelo relacional

## Usuários

### Origem

* Supabase Auth

### Identificação

* user_id = auth.uid

### Observação

* Não deve existir tabela adicional de usuários
* Dados do usuário são gerenciados exclusivamente pelo Supabase Auth

## Tabelas

## 1. ativos

### Objetivo

Representar os ativos financeiros do usuário.

Cada usuário possui sua própria lista de ativos.

### Estrutura

```sql id="ativos_table"
id UUID PRIMARY KEY
user_id UUID NOT NULL
ticker TEXT NOT NULL
nome TEXT NOT NULL
tipo TEXT NOT NULL -- 'acao' | 'fii'
criado_em TIMESTAMP NOT NULL DEFAULT now()
```

### Regras

* ticker deve ser armazenado em maiúsculo
* tipo deve ser validado ('acao', 'fii')
* não permitir duplicidade por usuário

### Constraints

```sql
UNIQUE (user_id, ticker)
```

### Índices

* index(user_id)
* index(ticker)

## 2. movimentacoes

### Objetivo

Registrar todas as operações de compra e venda.

### Estrutura

```sql id="movimentacoes_table"
id UUID PRIMARY KEY
user_id UUID NOT NULL
ativo_id UUID NOT NULL
tipo TEXT NOT NULL -- 'compra' | 'venda'
quantidade INTEGER NOT NULL
preco_unitario NUMERIC NOT NULL
data DATE NOT NULL
criado_em TIMESTAMP NOT NULL DEFAULT now()
```

### Relações

```sql
FOREIGN KEY (ativo_id) REFERENCES ativos(id)
```

### Regras

* quantidade deve ser positiva
* preco_unitario deve ser positivo
* tipo deve ser válido ('compra', 'venda')

### Índices

* index(user_id)
* index(ativo_id)
* index(data)

## 3. market_data_cache

### Objetivo

Armazenar dados de mercado temporários para:

* fallback
* redução de chamadas à API
* melhoria de performance

### Importante

* NÃO é fonte de verdade
* NÃO deve ser usado para lógica principal
* apenas suporte técnico

### Estrutura

```sql id="market_data_cache_table"
ticker TEXT PRIMARY KEY
preco NUMERIC NOT NULL
timestamp TIMESTAMP NOT NULL
```

### Regras

* dados podem ser sobrescritos
* deve respeitar TTL definido na aplicação

## Relações Gerais

* um usuário possui vários ativos
* um ativo possui várias movimentações
* movimentações pertencem a um único ativo

## Carteira

* NÃO deve existir tabela de carteira
* deve ser calculada dinamicamente a partir de:

  * movimentacoes
  * dados de mercado

## Segurança (RLS)

### Ativação

* Row Level Security deve estar ativado em todas as tabelas

### Regras

#### ativos

```sql id="rls_ativos"
user_id = auth.uid()
```

#### movimentacoes

```sql id="rls_movimentacoes"
user_id = auth.uid()
```

#### market_data_cache

* acesso liberado (dados públicos)

## Integridade

### Banco de Dados

* uso de constraints obrigatórias:

  * NOT NULL
  * UNIQUE
  * FOREIGN KEY

### Aplicação

* validação com Zod obrigatória

## Índices

Índices obrigatórios:

* user_id (todas as tabelas com usuário)
* ticker (ativos e cache)
* data (movimentacoes)

## Auditoria

* histórico baseado apenas em movimentações
* não implementar log adicional neste momento

## Escopo

* manter modelo simples
* evitar complexidade desnecessária
* preparado para evolução futura

## Dependências

* ativos.md
* movimentacoes.md
* carteira.md
* dados-de-mercado.md
* ranking.md
* autenticacao.md

## Conclusão

Este modelo garante:

* integridade de dados
* isolamento por usuário
* consistência com o domínio
* simplicidade de manutenção

Sem comprometer a escalabilidade futura.
