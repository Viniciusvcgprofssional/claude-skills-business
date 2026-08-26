---
name: content-repurposer
description: >
  Pega um conteúdo já pronto (post de LinkedIn, artigo, texto longo) e gera variações curtas para outras redes
  (Instagram, X/Twitter, thread), mantendo a mesma mensagem central e o mesmo tom de voz, sem nunca publicar
  sozinha. Ative quando o usuário disser "transforma esse post em versões pra outras redes", "resume isso pro
  Instagram", "faz uma thread a partir desse texto", ou colar um conteúdo pedindo adaptação para outro formato.
---

# Skill: Content Repurposer

## Visão geral

Content Repurposer resolve o trabalho repetitivo de reescrever a mesma ideia em formatos diferentes para redes
diferentes — um post de LinkedIn vira uma legenda de Instagram, um artigo vira uma thread, um texto longo vira um
resumo de poucas linhas — sem perder a mensagem central nem trocar o tom de voz do autor. Ela nunca publica nada
sozinha: gera o conteúdo, mostra pro usuário, e quem publica é sempre a pessoa, em cada rede, manualmente ou via
skill própria de cada rede (como a `instagram-brand`, quando o destino for Instagram).

## Passo 1 — Entender a mensagem central

Leia o conteúdo original e identifique: a ideia principal (uma frase), o tom (formal, técnico, descontraído etc.) e
qualquer chamada para ação que ele já tenha (link, convite a comentar, etc.).

## Passo 2 — Perguntar o destino

Confirme para qual(is) formato(s) o usuário quer a adaptação (legenda de Instagram, thread de X, resumo curto,
e-mail newsletter etc.) — não gera todos os formatos possíveis por padrão, só os pedidos, para não desperdiçar
esforço com o que a pessoa não vai usar.

## Passo 3 — Adaptar preservando a mensagem

Para cada formato pedido, reescreva respeitando o limite de tamanho e o costume da rede (thread quebrada em partes
numeradas, legenda de Instagram com quebra de linha e call-to-action no fim, etc.), mas sem adicionar afirmações
que não estavam no conteúdo original.

## Passo 4 — Verificação de privacidade (quando o destino for uma rede pessoal)

Se o destino for uma rede onde o usuário mantém perfil profissional com exposição mínima de dados pessoais (como o
padrão já definido na skill `instagram-brand`), aplique o mesmo checklist dela antes de entregar o texto final.

## Passo 5 — Entregar, nunca publicar

Mostre todas as versões geradas lado a lado com o formato de destino de cada uma. A skill nunca clica em publicar,
compartilhar ou agendar em nenhuma rede — isso é sempre ação do usuário.

## Coisas que esta skill nunca faz

- Nunca publica ou agenda nada em nenhuma rede social — apenas gera o texto para o usuário revisar e publicar.
- Nunca adiciona informação, estatística ou afirmação que não estava no conteúdo original.
- Nunca ignora o checklist de privacidade da `instagram-brand` quando o destino for essa rede.
