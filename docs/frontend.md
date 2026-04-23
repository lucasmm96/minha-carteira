# Frontend - Padrão de Interface

## Objetivo

Definir de forma determinística o padrão visual, estrutural e comportamental do frontend do sistema MinhaCarteira.

Este documento deve ser seguido rigorosamente por qualquer implementação (humana ou IA).
Nenhuma decisão visual ou estrutural deve ser tomada fora deste padrão.

## Arquitetura

* Tipo: SPA (Single Page Application)
* Framework: React
* Estilização: Tailwind CSS
* Gráficos: Recharts
* Plataforma: Web App (PWA)
* Abordagem: Mobile First
* Responsividade: Obrigatória

## Layout Geral

O sistema deve utilizar layout baseado em dashboard.

### Regiões obrigatórias

* Sidebar (navegação lateral)
* Topbar (ações globais)
* Content (conteúdo principal)

## Grid System

* Sistema: 12 colunas
* Unidade base: 8px

### Breakpoints

| Nome | Largura  |
| ---- | -------- |
| sm   | ≥ 640px  |
| md   | ≥ 768px  |
| lg   | ≥ 1024px |
| xl   | ≥ 1280px |
| 2xl  | ≥ 1536px |

---

## Design Tokens (OBRIGATÓRIO)

### Primary (Brand - Azul)

* Primary: `#2563EB`
* Primary Hover: `#1D4ED8`
* Primary Active: `#1E40AF`
* Primary Light: `#3B82F6`

### Background

* Background Primary: `#0F172A`
* Background Secondary: `#1E293B`
* Background Card: `#111827`
* Background Hover: `#1F2937`

### Texto

* Text Primary: `#F9FAFB`
* Text Secondary: `#9CA3AF`
* Text Muted: `#6B7280`
* Text Disabled: `#4B5563`


### Bordas

* Border Default: `#374151`
* Border Light: `#4B5563`


### Estados

* Success: `#22C55E`
* Warning: `#F59E0B`
* Error: `#EF4444`
* Info: `#3B82F6`


### Data Visualization (Gráficos)

* Blue: `#3B82F6`
* Green: `#22C55E`
* Yellow: `#F59E0B`
* Purple: `#8B5CF6`
* Pink: `#EC4899`


## Tipografia

* Fonte: Inter (fallback: system-ui)

### Tamanhos

| Tipo  | Tamanho |
| ----- | ------- |
| H1    | 24px    |
| H2    | 20px    |
| H3    | 18px    |
| Body  | 14px    |
| Small | 12px    |

### Peso

* Regular: 400
* Medium: 500
* SemiBold: 600


## Espaçamento

Sistema baseado em múltiplos de 8px:

* 4px → micro
* 8px → base
* 16px → padrão
* 24px → seção
* 32px → bloco


## Componentes


### Sidebar

#### Estrutura

* Largura:

  * Expandida: 240px
  * Colapsada: 72px

#### Comportamento

* Fixa à esquerda
* Deve suportar colapso
* Em mobile: virar drawer

#### Item ativo

* Background: `#1E293B`
* Borda esquerda: `#2563EB`
* Texto: `#F9FAFB`


### Topbar

#### Estrutura

* Altura: 64px

#### Elementos obrigatórios

* Campo de busca
* Notificações
* Avatar usuário

#### Estilo

* Background: `#0F172A`
* Border bottom: `#374151`
* Shadow:
  `0 1px 3px rgba(0,0,0,0.3)`


### Cards

#### Propriedades

* Background: `#111827`
* Border radius: 12px
* Padding: 16px
* Border: `1px solid #374151`

#### Sombra

`0 4px 12px rgba(0,0,0,0.3)`


### Tabelas

#### Regras obrigatórias

* Header fixo
* Hover linha:

  * Background: `#1E293B`
* Paginação obrigatória
* Ordenação obrigatória


### Botões

#### Primary

* Background: `#2563EB`
* Hover: `#1D4ED8`
* Texto: branco

#### Secondary

* Background: `#1E293B`
* Border: `#374151`


### Inputs

* Background: `#1E293B`
* Border: `#374151`
* Focus:

  * Border: `#2563EB`
  * Ring: `#2563EB`


## Gráficos (Recharts)

### Tipos obrigatórios

* LineChart
* BarChart
* AreaChart
* PieChart (Donut)

### Regras

* Tooltip obrigatório
* Legenda obrigatória
* Cores devem usar Design Tokens


## Responsividade

### Mobile (<768px)

* Sidebar → Drawer
* Grid → 1 coluna
* Cards empilhados


### Tablet

* Grid → 2 colunas


### Desktop

* Grid → até 4 colunas


## Interações

* Transition padrão:
  `transition: all 0.2s ease`

* Hover obrigatório em elementos interativos


## Estados de Interface

### Loading

* Skeleton obrigatório


### Empty

* Mensagem clara
* Ícone ilustrativo


### Error

* Mensagem + destaque visual


## PWA

### Requisitos obrigatórios

* Instalável
* Manifest.json configurado
* Service Worker ativo
* Cache mínimo da interface


## Restrições

* NÃO usar cores fora dos tokens
* NÃO usar valores arbitrários
* NÃO duplicar componentes
* NÃO quebrar responsividade
* NÃO misturar padrões visuais


## Estrutura de Componentes (React)

```
src/
  components/
    ui/
    layout/
    charts/
  pages/
  hooks/
  services/
```

## Convenções

* Componentes: PascalCase
* Hooks: useNome
* Classes Tailwind padronizadas
* Reutilização obrigatória

## Observação Final

Este documento é a fonte única de verdade para o frontend.

Qualquer implementação deve seguir EXATAMENTE estas definições.