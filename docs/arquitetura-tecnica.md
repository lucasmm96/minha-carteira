# Arquitetura Técnica

## Objetivo

Definir de forma determinística a stack tecnológica, padrões de implementação, organização de código e boas práticas do sistema MinhaCarteira.

Este documento deve guiar tanto desenvolvedores quanto IA na implementação do sistema.

## Stack Tecnológica

### Frontend

* React
* Vite

### Linguagem

* TypeScript (modo strict obrigatório)

### Backend

* Supabase (Backend as a Service)

### Banco de Dados

* PostgreSQL (via Supabase)

### Autenticação

* Supabase Auth com Google OAuth

### Estilização

* Tailwind CSS

### Validação

* Zod

### Testes

* Vitest

## Arquitetura de Código

### Estratégia Geral

O sistema deve seguir uma arquitetura híbrida com foco em domínio.

* A lógica deve ser organizada por domínio (principal)
* A estrutura deve manter camadas simples para entrega

### Domínios do Sistema

O código deve ser organizado nos seguintes domínios:

* ativos
* carteira
* movimentacoes
* ranking

### Estrutura de Camadas

```id="estrutura_camadas"
pages → hooks → services → api
              ↓
            domain
```

### Responsabilidades

#### pages

* composição de interface
* não conter lógica de negócio

#### hooks

* controle de estado
* integração com React Query
* orquestração de dados para UI

#### services

* orquestra chamadas externas
* integra domínio + API
* contém lógica leve (não regras puras)

#### api

* comunicação com:

  * Supabase
  * Yahoo Finance
* não conter lógica de negócio

#### domain

* regras puras do sistema
* funções determinísticas

Exemplos:

* cálculo de preço médio
* cálculo de valorização
* cálculo de ranking

## Gerenciamento de Estado

### Estado Global

* Context API

### Data Fetching (OBRIGATÓRIO)

* React Query

### Regras

* Toda requisição externa deve usar React Query
* Não utilizar fetch manual em componentes
* Cache deve ser gerenciado pela biblioteca

## Integração com API

### Estrutura

```id="estrutura_api"
api/
  supabase.ts
  yahoo.ts
```

### Regras

* Nunca acessar API diretamente em componentes
* Nunca acessar API diretamente em hooks
* Toda integração deve passar por services

## Domínio

### Camada de Domínio

Deve ser:

* simples
* baseada em funções
* sem complexidade desnecessária

### Regras

* Funções puras sempre que possível
* Sem dependência de frameworks
* Sem acesso direto a API ou banco

## Banco de Dados

### Acesso

* via Supabase (camada api)
* sem repository pattern neste momento

### Regras

* nunca acessar banco diretamente em hooks ou componentes
* toda operação passa por services

## Tipagem e DTOs

### DTOs

* obrigatórios
* utilizados para dados externos

### Tipagem

* strict obrigatório
* proibido uso de `any`

### Validação

* Zod obrigatório para:

  * entrada de dados
  * respostas de API

## UI e Componentização

### Componentes

* pequenos e reutilizáveis
* separar:

  * componentes de layout
  * componentes de domínio

### Design System

* seguir `frontend.md`
* utilizar tokens definidos

## Autenticação

### Implementação

* Supabase Auth
* login exclusivo via Google

### Proteção de Rotas

* implementar guard de rota (obrigatório)
* nenhuma página acessível sem autenticação

## Estrutura de Pastas

```id="estrutura_pastas"
src/
  components/
  pages/
  hooks/
  services/
  api/
  context/
  domain/
    ativos/
    carteira/
    movimentacoes/
    ranking/
```

## Testes

### Estratégia

* Vitest

### Prioridade

* funções de domínio
* services

## Boas Práticas

### Obrigatórias

* tipagem estrita
* funções puras quando possível
* separação de responsabilidades
* evitar duplicação

### Proibido

* lógica de negócio em componentes
* acesso direto à API em componentes
* uso de `any`
* código não tipado

## Regras para IA

### Uso

A IA deve:

* seguir rigorosamente este documento
* respeitar a arquitetura definida
* não criar padrões alternativos

### Geração de Código

A IA pode:

* gerar código completo
* gerar partes específicas

Sempre respeitando:

* separação de camadas
* organização por domínio
* tipagem

## Observações

Este documento deve ser utilizado em conjunto com:

* ativos.md
* movimentacoes.md
* carteira.md
* dados-de-mercado.md
* ranking.md
* dashboard.md
* autenticacao.md

## Conclusão

Esta arquitetura foi projetada para:

* simplicidade
* manutenção
* escalabilidade progressiva

Sem introduzir complexidade desnecessária.
