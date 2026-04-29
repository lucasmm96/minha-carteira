# Tratamento de Erros

## Objetivo

Definir como o sistema deve lidar com falhas.

## Tipos de Erro

### API de Mercado (Yahoo)

* fallback para último valor
* retry automático no próximo ciclo

### Banco de Dados

* exibir erro ao usuário
* não perder dados

### Autenticação

* redirecionar para login

## Interface

### Estados

#### Loading

* skeleton

#### Error

* mensagem clara
* destaque visual

#### Empty

* mensagem + ação sugerida

## Regras

* não ocultar erros críticos
* não travar interface
* sempre permitir recuperação

## Logs

* erros devem ser logados

## Comportamento da IA

* não ignorar erros
* aplicar fallback quando necessário
* não inventar dados
