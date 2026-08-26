---
name: git-to-git
description: >
  Publica ou atualiza skills do Claude no GitHub do usuário, do zero, pelo navegador (Claude in Chrome), sem linha de comando de Git. Também conhecida como GITTOGIT — os dois nomes ativam a mesma skill. Ative SEMPRE que o usuário disser "publica isso no meu github", "sobe essa skill pro github", "cria um repositório pra essa skill", "roda a gittogit", ou algo assim. Também ativar para avaliar/curar quais skills já existentes valem publicar (ex.: "quais das minhas skills valem publicar", "quero ganhar estrelas no github"). Antes de publicar, sempre faz varredura obrigatória de dados pessoais e credenciais (ver references/privacy-scan.md), publica de forma anônima por padrão, e decide repositório novo vs. existente, licença e .gitignore sozinha.
---

# Skill: Git to Git (GITTOGIT)

## Visão geral

Esta skill pega uma skill do Claude que o usuário acabou de criar (ou já tem pronta) e publica no GitHub dele — tudo pela interface web do GitHub via Claude in Chrome, porque o usuário não usa Git por linha de comando. O usuário também se refere a ela como **GITTOGIT** — é a mesma skill, o nome é só uma marca mais memorável para o fluxo de publicação; tecnicamente ela continua registrada como `git-to-git`. Ela sempre segue esta ordem: **(opcional: curadoria do portfólio) → varredura de privacidade → decisão de repositório → licença e .gitignore → montagem dos arquivos → confirmação explícita do usuário → publicação real → verificação final**.

A skill `gitfabric` (a "fábrica de skills") usa a GITTOGIT como a etapa final do seu pipeline: GITFABRIC gera e constrói a ideia de skill nova, e entrega para a GITTOGIT publicar seguindo exatamente este mesmo processo, sem pular nenhuma etapa.

**Regra inegociável**: nunca execute a etapa de publicação real (criar repositório, fazer commit, subir arquivo) sem antes mostrar ao usuário exatamente o que vai ser publicado — nome do repositório, visibilidade (público/privado), lista de arquivos, licença escolhida — e receber uma confirmação explícita ("sim", "pode publicar", "confirmado"). Publicar conteúdo é uma ação irreversível-ish (fica no histórico do Git mesmo se apagar depois), então cada publicação exige essa confirmação, mesmo que o usuário já tenha confirmado uma publicação anterior nesta mesma conversa.

## Modo Curadoria — avaliar todas as skills do usuário para publicação

Use este modo quando o usuário pedir para avaliar/auditar as skills que ele já tem, em vez de já saber qual quer publicar (ex.: "quais das minhas skills valem publicar", "quero ganhar estrelas no github com minhas skills"). Depois desse modo, siga normalmente a partir do Passo 1 para cada skill que o usuário decidir publicar.

1. Liste todas as skills disponíveis do usuário (via `ListSkills`/`SearchSkills` se disponíveis, ou lendo o diretório local de skills sincronizadas). Ignore skills que claramente não são do próprio usuário (skills de plugins/marketplaces instalados, não autorais dele).
2. Para cada skill autoral do usuário, leia o `SKILL.md` completo (e `references/` se precisar de mais contexto) e avalie usando `references/star-appeal.md`: o que ela faz, se já é genérica/reutilizável ou hiper-pessoal, e o veredito (publicar como está / generalizar antes / manter privada / não vale a pena).
3. Apresente o resultado como uma lista curta, uma linha de veredito e justificativa por skill — não é preciso fazer isso em documento formal, a menos que o usuário peça.
4. Pergunte ao usuário quais dele quer seguir publicando. Para cada uma escolhida, se o veredito foi "generalizar antes", ofereça para fazer essa generalização primeiro (reaproveitando o mesmo processo já usado antes: extrair critérios fixos para perguntas em tempo de execução, como foi feito com a `career-search`).
5. Se houver mais de uma skill publicável, sugira a estrutura de repositório-coleção descrita em `references/star-appeal.md` (um único repositório bem organizado, com README-índice e topics no GitHub) em vez de vários repositórios soltos, e explique por que isso ajuda no alcance.
6. Depois dessa etapa, prossiga normalmente pelo Passo 1 em diante para cada skill aprovada.

## Passo 1 — Identificar o que vai ser publicado

Confirme com o usuário qual skill (pasta/arquivos) deve ser publicada, se não estiver óbvio pelo contexto da conversa. Reúna todos os arquivos que fazem parte dela: `SKILL.md`, tudo dentro de `references/`, `scripts/`, `assets/`.

## Passo 2 — Varredura obrigatória de dados pessoais

Leia **references/privacy-scan.md** e siga o processo descrito lá à risca, sem pular etapas. Resumo: leia todo arquivo, procure nome completo, e-mail, telefone, endereço, links pessoais, documentos, currículo, credenciais. Apresente os achados ao usuário e siga uma das rotas: genericizar, manter como repositório privado, ou abortar. Só avance para o Passo 3 depois que essa decisão estiver clara e, se houver genericização, os arquivos já tiverem sido reescritos sem o dado pessoal.

## Passo 3 — Decidir o repositório de destino

1. Se o Claude in Chrome ainda não tiver as ferramentas carregadas (aparecem "deferred", sem schema), carregue-as em UMA chamada de ToolSearch: `ToolSearch` com query `"select:mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__computer,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__get_page_text,mcp__claude-in-chrome__find,mcp__claude-in-chrome__tabs_create_mcp,mcp__claude-in-chrome__tabs_close_mcp,mcp__claude-in-chrome__form_input"`
2. Chame `tabs_context_mcp` e abra uma aba nova para `github.com`. Confirme que o usuário está logado (se não estiver, peça para ele logar manualmente — nunca digite usuário/senha por ele).
3. Navegue até a lista de repositórios do usuário (`github.com/<usuario>?tab=repositories`) e use `get_page_text` para ler nomes, descrições e tópicos dos repositórios existentes.
4. Compare o assunto da skill nova com os repositórios existentes (por palavras-chave: tema, tipo de skill, descrição). Se houver um repositório claramente compatível (ex.: um repositório tipo "claude-skills" ou "minhas-skills" que já reúne skills variadas, ou um repositório específico do mesmo tema), proponha adicionar a skill nova como uma subpasta dele. Caso contrário, proponha criar um repositório novo.
5. Apresente a recomendação ao usuário com a justificativa ("encontrei o repositório X, que já tem skills parecidas, vou adicionar lá" ou "não achei nada parecido, vou criar um repositório novo chamado Y") e espere confirmação ou ajuste antes de continuar.

## Passo 4 — Preparar licença, README e .gitignore (apenas para repositório novo)

- **Licença**: siga `references/licenses.md`. Padrão MIT, com o nome do usuário e o ano atual, a menos que ele peça outra. Explique em uma frase por que essa foi a escolha.
- **README.md**: escreva um README curto e direto — o que a skill faz, quando ela é ativada, como instalar (baixar o `.skill` e usar o botão "Salvar skill", ou clonar o repositório se for uma coleção), e um exemplo de uso. Nunca inclua dados pessoais aqui — ele passa pela mesma varredura do Passo 2.
- **.gitignore**: monte um `.gitignore` enxuto adequado ao conteúdo (arquivos de sistema como `.DS_Store`, configurações de editor, arquivos temporários, e sempre incluir `.env` e padrões de credenciais mesmo que não existam ainda, como prevenção).

Se for adicionar a um repositório existente, pule este passo (a menos que o repositório não tenha licença/README ainda, caso em que vale oferecer para criar).

## Passo 5 — Mostrar o plano e confirmar

Antes de tocar em qualquer botão de criação/commit no GitHub, resuma para o usuário em texto simples:
- Nome do repositório (novo ou existente)
- Visibilidade: público ou privado (e por quê)
- Lista final de arquivos que serão publicados
- Licença escolhida (se repositório novo)
- Descrição do repositório (curta, no estilo já combinado nesta conversa — utilitária e direta)

Espere uma confirmação explícita do usuário. Se ele pedir ajustes, aplique e mostre o plano atualizado antes de publicar.

## Passo 6 — Publicar via Claude in Chrome

Tudo pela interface web do GitHub (não usar comandos Git):

**Repositório novo:**
1. Navegar para `github.com/new`.
2. Preencher nome e descrição do repositório.
3. Selecionar visibilidade (Public/Private) conforme decidido no Passo 2/5.
4. Marcar "Add a README file" (ou pular se você for subir o seu próprio README.md customizado depois).
5. No dropdown de `.gitignore`, pode escolher "None" e depois criar o arquivo manualmente com o conteúdo do Passo 4 (mais controle sobre o conteúdo exato).
6. No dropdown de licença, escolher a licença decidida no Passo 4.
7. Clicar em "Create repository".
8. Depois de criado, usar "Add file" → "Create new file" para adicionar cada arquivo de texto (SKILL.md, references/*.md, README.md se não foi criado no passo 4, .gitignore se não escolhido no dropdown) — no campo de nome do arquivo, digitar o caminho completo com `/` (ex.: `nome-da-skill/SKILL.md`) para o GitHub criar a pasta automaticamente. Colar o conteúdo, escrever uma mensagem de commit curta e clicar em "Commit changes".

**Repositório existente:**
1. Navegar até o repositório escolhido.
2. Usar "Add file" → "Create new file", digitando o caminho `nome-da-skill/SKILL.md` (e os demais arquivos da mesma forma) para criar a skill como uma subpasta nova dentro do repositório.
3. Se o repositório tiver um README principal que lista as skills disponíveis, editar esse README para incluir a nova entrada (nome + descrição curta + link para a pasta).

## Passo 7 — Verificar e reportar

Depois de publicar, navegue até a página final do repositório/pasta e use `get_page_text` para confirmar que os arquivos estão lá com o conteúdo certo. Informe ao usuário o link direto do repositório (e da pasta, se foi adicionado a um existente) para ele conferir.

## Coisas que esta skill NUNCA faz

- Nunca digita usuário/senha do GitHub pelo usuário — login é sempre manual, feito por ele.
- Nunca publica sem a varredura de privacidade completa do Passo 2.
- Nunca publica sem a confirmação explícita do Passo 5, mesmo que o usuário pareça claramente satisfeito com publicações anteriores na mesma conversa.
- Nunca cria repositório público quando a varredura encontrou dado pessoal não resolvido — nesse caso, cria como privado ou aborta, conforme decidido com o usuário.
- **Nunca publica API keys, tokens, senhas ou qualquer credencial**, em nenhuma circunstância — isso é bloqueio automático, não uma decisão do usuário (ver "Chaves e credenciais" em `references/privacy-scan.md`).
- **Por padrão, publica de forma anônima**: usa o handle do GitHub em vez do nome completo, não inclui e-mail pessoal nem outros dados identificáveis, a menos que o usuário peça explicitamente para ser identificável (ver "Modo anônimo por padrão" em `references/privacy-scan.md`).
