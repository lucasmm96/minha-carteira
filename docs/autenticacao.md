# Autenticação

## Objetivo

Definir de forma determinística como o sistema gerencia identidade, acesso e isolamento de dados dos usuários.

Este documento estabelece as regras de autenticação e autorização do sistema.

## Método de Autenticação

O sistema deve utilizar:

* Login com Google (OAuth)

### Cadastro de Usuário

* O usuário deve ser criado automaticamente no primeiro login
* Não deve existir fluxo manual de cadastro

## Identificação do Usuário

### Identificador Principal

* Cada usuário deve possuir um ID interno único gerado pelo sistema

### Dados Armazenados

O sistema deve armazenar:

* Nome
* Email

## Isolamento de Dados

### Regra Principal

* Cada usuário deve acessar apenas seus próprios dados

### Escopo de Isolamento

Os seguintes dados devem ser isolados por usuário:

* Ativos
* Movimentações
* Carteira
* Ranking

### Multi-usuário

* O sistema deve suportar múltiplos usuários simultaneamente
* Os dados devem ser completamente segregados

## Sessão

### Persistência

* A sessão do usuário deve ser persistente
* O sistema deve manter o usuário autenticado entre acessos

### Renovação

* Tokens devem ser renovados automaticamente pelo provedor de autenticação

### Logout

* Deve existir logout manual
* Não é necessário logout automático por timeout

## Dispositivos

* O usuário pode acessar o sistema em múltiplos dispositivos simultaneamente
* A sessão deve ser independente por dispositivo

## Segurança

### Proteção de Rotas

* Todas as rotas do sistema exigem autenticação
* Não deve existir conteúdo público

### Dados Sensíveis

Todos os dados do sistema devem ser tratados como sensíveis:

* Carteira
* Movimentações
* Ranking
* Dados do usuário

## Recuperação de Acesso

* Não é necessário fluxo de recuperação de senha
* O acesso deve ser gerenciado exclusivamente via Google OAuth

## Integração

### Provedor de Autenticação

* Supabase Auth

### Configuração

* Deve utilizar Google OAuth configurado no Supabase

## Criação de Dados

### Inicialização

Ao criar um usuário:

* Uma carteira deve ser criada automaticamente
* O usuário deve iniciar sem ativos

## Usuário Não Autenticado

* Não deve ter acesso a nenhuma funcionalidade do sistema
* Deve ser redirecionado para login

## Comportamento da IA

A IA deve:

* acessar apenas dados do usuário autenticado
* nunca acessar dados de outros usuários
* respeitar o isolamento de dados

## Restrições

* Não permitir acesso sem autenticação
* Não compartilhar dados entre usuários
* Não expor dados sensíveis
* Não permitir bypass de autentação

## Observações

Este documento define as regras de identidade e acesso do sistema.

Ele deve ser considerado fonte única de verdade para autenticação.

## Dependências

* ativos.md
* movimentacoes.md
* carteira.md
* dados-de-mercado.md
* ranking.md
* dashboard.md
