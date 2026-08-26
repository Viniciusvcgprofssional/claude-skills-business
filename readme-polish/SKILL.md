---
name: readme-polish
description: >
  Audita um README.md existente e reescreve seguindo boas práticas de projetos GitHub bem recebidos — estrutura
  clara, seção de instalação, exemplo de uso antes/depois, badges relevantes — sem alterar o código ou o
  funcionamento do projeto. Ative quando o usuário disser "melhora meu README", "meu repositório não chama
  atenção", "revisa a apresentação desse projeto no GitHub", ou colar/anexar um README para revisão.
---

# Skill: README Polish

## Visão geral

README Polish resolve um problema muito comum: o código é bom, mas o README não vende o projeto em 10 segundos de
leitura, que é o tempo real que a maioria das pessoas dá antes de decidir se fica ou sai. A skill audita o README
atual, aponta o que está fraco ou faltando, e entrega uma versão reescrita — sem inventar funcionalidades que o
projeto não tem.

## Passo 1 — Ler o README e (se possível) o projeto

Leia o README atual e, se o usuário der acesso ao repositório, dê uma olhada rápida na estrutura de pastas e no
arquivo de entrada principal para confirmar que a descrição bate com o que o projeto realmente faz. Nunca invente
recursos que não existem no código só para o README parecer mais impressionante.

## Passo 2 — Auditar contra o checklist de qualidade

Avalie o README atual em `references/readme-checklist.md` e aponte, em bullets curtos, o que está faltando ou fraco
(ex.: sem seção de instalação, sem exemplo de uso, título genérico demais, sem indicação clara do problema que o
projeto resolve).

## Passo 3 — Reescrever

Produza a versão nova seguindo a estrutura recomendada: título + uma frase de valor, badges relevantes (se
aplicável — build, licença, versão), o problema que o projeto resolve, instalação, exemplo de uso com um
antes/depois quando fizer sentido, e uma seção de licença/contribuição enxuta no final. Mantenha o tom do autor
original quando ele já tiver um tom definido (técnico, descontraído etc.) em vez de forçar um tom genérico.

## Passo 4 — Mostrar antes/depois

Sempre entregue as duas versões lado a lado (ou a versão nova com um resumo do que mudou e por quê), para o usuário
decidir se aceita a reescrita inteira ou só partes dela.

## Passo 5 — Publicar só com aprovação

Se o usuário pedir para já aplicar o novo README no repositório, siga o processo de publicação segura da skill
`git-to-git` (GITTOGIT) — nunca sobrescreve o README publicado sem a confirmação explícita de lá.

## Coisas que esta skill nunca faz

- Nunca inventa funcionalidades, métricas de uso ou badges que não são reais só para o README parecer melhor.
- Nunca troca o idioma do README sem o usuário pedir (mantém português se o original for português, etc.).
- Nunca sobrescreve o README publicado no GitHub sem confirmação explícita, mesmo que o usuário tenha aprovado o
  conteúdo — a confirmação de publicação é sempre um passo separado.
