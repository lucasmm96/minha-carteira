# Navegação

## Objetivo

Definir rotas e fluxo de navegação do sistema.

## Rotas

### Dashboard

```
/dashboard
```

### Detalhe do Ativo

```
/ativo/:id
```

### Nova Movimentação

```
/movimentacao/nova
```

### Edição de Movimentação

```
/movimentacao/:id
```

## Regras

* todas as rotas exigem autenticação
* usuário deve acessar apenas seus dados

## Navegação

### Sidebar

Deve conter:

* Dashboard

### Fluxos principais

#### Fluxo 1 — Visualização

```
Dashboard → Detalhe do ativo
```

#### Fluxo 2 — Registro

```
Dashboard → Nova movimentação
```

#### Fluxo 3 — Edição

```
Detalhe → Editar movimentação
```

## Comportamento da IA

* respeitar rotas
* não criar rotas adicionais
* não alterar fluxo definido
