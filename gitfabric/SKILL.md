---
name: gitfabric
description: >
  Fábrica de ideias de novas skills do Claude, pensadas para ganhar alcance/estrelas no GitHub e, no longo prazo, abrir espaço para doações via GitHub Sponsors. Gera propostas de skills novas (nome, o que faz, por que teria apelo), espera aprovação do usuário, monta a skill aprovada, e entrega para a skill `git-to-git` (também conhecida como GITTOGIT) publicar. Ative quando o usuário disser "ligar a fábrica git", "cria uma skill nova pra mim", "que skill eu deveria publicar em seguida", ou pedir ideias de skills para crescer o portfólio no GitHub. Honestidade importante: isto é uma skill (um conjunto de instruções que o Claude segue), não um novo tipo de agente/subagente — "fábrica" é o nome do fluxo, não uma automação literal fora do controle do usuário.
---

# Skill: GITFABRIC

## Visão geral

GITFABRIC é o nome dado ao fluxo de "fábrica de skills": gerar ideias de skills novas com potencial real de alcance no GitHub, escolher a melhor com o usuário, construir a skill, e entregar para a `git-to-git`/GITTOGIT publicar. O objetivo final declarado pelo usuário é crescer estrelas/alcance no GitHub e, com o tempo, abrir caminho para doações (GitHub Sponsors).

**O que isso é, de verdade**: uma sequência de passos que este Claude segue nesta conversa, usando as ferramentas já disponíveis (não um agente novo rodando sozinho, não um serviço em background). Cada etapa importante ainda passa por aprovação do usuário — a "fábrica" acelera a geração de ideias e a montagem do conteúdo, mas não publica nada sem confirmação explícita (essa regra vem de `git-to-git` e continua valendo aqui, sem exceção).

## Passo 1 — Entender o que já existe

Antes de propor qualquer ideia nova, mapeie o portfólio atual para não repetir tema nem sugerir algo que já existe:

1. Liste as skills do usuário já publicadas (repositórios `claude-skills-academic`, `claude-skills-business`, `claude-skills-personal`, `Career-Search`, `economic-software` — ou pergunte se surgiu algum novo repositório).
2. Note os temas já cobertos (produtividade acadêmica, publicação segura no GitHub, branding no Instagram, busca de emprego, ferramentas econômicas) para evitar sobreposição.

## Passo 2 — Gerar propostas de skill

Gere de 3 a 5 ideias de skills novas, cada uma avaliada com os critérios de `references/star-appeal.md` (mesmo arquivo de critérios usado pela `git-to-git` para avaliar apelo de estrela). Para cada ideia, apresente em 2-3 frases:

- Nome proposto (curto, memorável).
- O que a skill faz (o problema real que resolve).
- Por que tem potencial de alcance (conecte com os sinais de `star-appeal.md`: problema comum, fácil de entender, não depende de dados só do usuário, preenche uma lacuna).
- Nível de esforço estimado para construir (rápido / médio / grande).

Priorize ideias que:
- generalizam bem (não são hiper-pessoais);
- conectam com a área do usuário (economia, produtividade, uso do Claude) sem se limitar só a isso — skills fora da área dele também valem se tiverem apelo amplo;
- ainda não têm equivalente óbvio e popular disponível.

Registre as ideias propostas em `references/idea-bank.md` (mesmo as não escolhidas, para não repetir depois).

## Passo 3 — Escolher e aprovar

Pergunte ao usuário qual ideia (ou ideias) ele quer seguir. Não avance para construção sem essa escolha explícita — a fábrica gera opções, quem decide o que entra em produção é sempre o usuário.

## Passo 4 — Construir a skill escolhida

1. Escreva o `SKILL.md` completo (frontmatter `name`/`description` + corpo com passos claros), seguindo o mesmo padrão de qualidade das skills já publicadas (ver exemplos em `git-to-git`, `instagram-brand`, etc.: visão geral, passos numerados, "coisas que a skill nunca faz" quando fizer sentido).
2. Se a skill precisar de arquivos de referência (`references/*.md`), crie-os também.
3. Mostre o conteúdo completo ao usuário antes de seguir para a publicação.

## Passo 5 — Entregar para GITTOGIT publicar

Depois que o usuário aprovar o conteúdo da skill nova, siga o processo completo da skill `git-to-git` (GITTOGIT) do zero — varredura de privacidade, decisão de repositório, licença/README/.gitignore se for repositório novo, e principalmente o passo de confirmação explícita antes da publicação real. GITFABRIC não pula nenhuma dessas etapas: ela só acelera a parte de "ter uma ideia boa e construir o conteúdo".

## Passo 6 — Registrar no histórico da fábrica

Depois que a skill nova for publicada com sucesso, anote em `references/pipeline-log.md` (data, nome da skill, repositório de destino) para acompanhar o ritmo de produção e evitar repetir temas em ciclos futuros.

## O gatilho "ligar a fábrica git"

Quando o usuário disser algo como "ligar a fábrica git", rode o pipeline completo GITFABRIC → GITTOGIT nesta ordem: Passo 1 → Passo 2 → Passo 3 (espera aprovação) → Passo 4 → Passo 5 (espera confirmação de publicação, regra da `git-to-git`) → Passo 6. Isso significa que "ligar a fábrica" inicia o fluxo, mas ele ainda para em dois pontos para o usuário decidir: qual ideia construir, e se pode publicar de fato.

## Coisas que esta skill NUNCA faz

- Nunca publica uma skill nova sem o usuário aprovar a ideia primeiro (Passo 3) e sem a confirmação explícita de publicação da `git-to-git` (Passo 5) — mesmo com o gatilho "ligar a fábrica git".
- Nunca pula a varredura de privacidade da `git-to-git` para ideias novas que acabaram de ser construídas.
- Nunca se descreve como um agente novo ou automação fora do controle do usuário — é sempre uma skill que este Claude segue dentro da conversa atual.
- Nunca reaproveita ideias já descartadas pelo usuário sem avisar que ela já foi proposta antes (ver `references/idea-bank.md`).
