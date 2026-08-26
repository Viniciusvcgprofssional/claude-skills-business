---
name: spreadsheet-sanity-check
description: >
  Audita uma planilha (CSV/XLSX) antes de ela ser usada para decisão ou análise: aponta valores ausentes, tipos de
  coluna inconsistentes, duplicatas, outliers óbvios e problemas comuns de fórmula, com um relatório claro do que
  checar antes de confiar nos números. Ative quando o usuário disser "confere essa planilha antes de eu usar",
  "essa base de dados está certa?", "dá uma olhada nesses dados antes de eu analisar", ou anexar uma planilha
  pedindo verificação.
---

# Skill: Spreadsheet Sanity Check

## Visão geral

Spreadsheet Sanity Check resolve um problema comum antes de qualquer análise séria: decisões erradas frequentemente
vêm de planilhas com problemas silenciosos — uma coluna que devia ser numérica virou texto em algumas linhas, uma
data duplicada, um outlier que na verdade é erro de digitação. A skill faz uma auditoria de primeira camada, sem
tentar fazer a análise de negócio no lugar do usuário — o objetivo é garantir que os dados estão limpos o
suficiente para confiar neles.

## Passo 1 — Carregar e mapear a planilha

Leia a planilha/CSV e identifique colunas, tipos aparentes de cada uma, e o número de linhas.

## Passo 2 — Rodar a checagem de sanidade

Para cada coluna, verifique:
- **Valores ausentes**: quantas linhas faltam e se seguem algum padrão (ex.: sempre a mesma coluna, período
  específico).
- **Tipo inconsistente**: coluna que deveria ser numérica/data mas tem células com texto ou formato diferente.
- **Duplicatas**: linhas inteiras repetidas, ou uma chave que deveria ser única (ex.: ID, CPF, e-mail) aparecendo
  mais de uma vez.
- **Outliers óbvios**: valores muito fora da faixa do resto da coluna (ex.: idade de 300 anos, valor negativo onde
  não devia existir).
- **Erros de fórmula visíveis**: células com erro (#DIV/0!, #REF!, #N/A) se a planilha for XLSX com fórmulas.

## Passo 3 — Relatório claro, sem alarmismo

Apresente os achados por severidade (crítico / atenção / observação), com o número de linhas afetadas e um exemplo
concreto de cada problema — não só "há inconsistências", mostrar qual linha e qual valor.

## Passo 4 — Sugerir, não decidir

Para cada problema, sugerir a correção mais provável (ex.: "essas 4 linhas com data em formato texto provavelmente
deveriam ser convertidas") mas deixar a decisão final (remover, corrigir, ignorar) com o usuário — a skill nunca
altera os dados originais sem confirmação.

## Passo 5 — Entregar versão corrigida (opcional)

Se o usuário aprovar as correções sugeridas, gerar uma cópia corrigida da planilha ao lado da original, nunca
sobrescrevendo o arquivo original sem pedido explícito.

## Coisas que esta skill nunca faz

- Nunca sobrescreve a planilha original sem confirmação explícita do usuário — sempre gera uma cópia corrigida ao
  lado.
- Nunca faz a análise de negócio (ex.: "esses dados mostram que as vendas caíram") — só garante que os dados estão
  limpos o suficiente para essa análise ser confjC�vel.
- Nunca remove uma linha ou valor por conta própria — sempre lista o problema e espera decisão do usuário.
