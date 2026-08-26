---
name: instagram-brand
description: >
  Prepara posts para o Instagram profissional do usuário, promovendo seu trabalho (skills do Claude, projetos no
    GitHub, conteúdo de economia/dados) com uma identidade visual padronizada, espelhada no tom do LinkedIn dele, e
      revelando o mínimo possível de dado pessoal. Ative quando o usuário disser algo como "prepara um post pro
        instagram", "faz um post divulgando minha skill/repositório", "cria o conteúdo pro perfil profissional", ou
          pedir para manter a estética do Instagram consistente com o LinkedIn. A skill monta o post inteiro (imagem/texto,
            legenda, hashtags) pelo navegador (Claude in Chrome), mas o clique final de publicar/postar é SEMPRE feito
              manualmente pelo usuário — nunca por esta skill.
              ---

              # Skill: Instagram Brand

              ## Visão geral

              Esta skill transforma uma conquista técnica (skill nova publicada, repositório no GitHub, marco de estudo/projeto
              em economia) em um post pronto para o Instagram profissional do usuário, seguindo uma identidade visual fixa e
              consistente — para que o perfil pareça uma marca, não posts avulsos. A referência de tom e visual é o LinkedIn do
              usuário: profissional, direto, orientado a competência técnica, com o mínimo de exposição pessoal possível.

              **Regra inegociável**: esta skill prepara o conteúdo (imagem, legenda, hashtags) e deixa tudo pronto na tela do
              Instagram (via `web.instagram.com` ou o compositor que o usuário preferir), mas **nunca clica em "Compartilhar"/
              "Publicar"**. Esse clique final é sempre do usuário. Isso vale mesmo que ele peça explicitamente para "publicar
              direto" — nesse caso, explique a regra e deixe tudo pronto para ele só conferir e clicar.

              ## Passo 1 — Calibrar a identidade visual (uma vez, depois revisitar quando pedido)

              Se `references/visual-identity.md` ainda não tiver sido preenchido com decisões reais do usuário (só tem os
              padrões genéricos), calibre antes do primeiro post:

              1. Pergunte o link do LinkedIn do usuário (se ainda não souber) e, com o Claude in Chrome, abra o perfil público
                 dele para observar: cor dominante da foto de capa/banner, tom da bio (formal? direto? bem-humorado?), tipo de
                    conteúdo que ele já posta lá.
                    2. Extraia dali uma paleta de 2-3 cores e um tom de voz, e proponha ao usuário um resumo curto ("vou usar azul
                       petróleo + branco + um dourado de destaque, tom direto e técnico, sem emojis em excesso — parece com o que você
                          tem no LinkedIn?").
                          3. Depois de aprovado, grave essa decisão em `references/visual-identity.md`, substituindo os placeholders.
                          4. Revisite esse passo só se o usuário pedir para mudar a identidade visual — não recalibrar a cada post.

                          ## Passo 2 — Verificação de exposição pessoal (obrigatória, todo post)

                          Antes de montar qualquer post, releia `references/privacy-checklist.md` e aplique a cada peça de conteúdo
                          (imagem, legenda, bio, destaques):

                          - Nunca incluir sobrenome completo, endereço, telefone, e-mail pessoal, número de matrícula/RG/CPF, rotina diária,
                            localização em tempo real, ou fotos que exponham ambiente doméstico/documentos.
                            - Nome de exibição: usar primeiro nome + handle do GitHub/Instagram, nunca o nome civil completo, a menos que o
                              usuário peça explicitamente o contrário.
                              - Instituição (ex.: universidade) pode aparecer de forma genérica ("estudante de Economia") sem precisar do campus
                                ou turma específicos, a menos que o usuário quera destacar isso.
                                - Se o conteúdo do post vier de uma skill/repositório que já passou pela varredura da `git-to-git`
                                  (`references/privacy-scan.md` daquela skill), não repita a varredura de código — foque só no que vai aparecer
                                    visualmente no post (imagem, legenda, bio).

                                    ## Passo 3 — Montar o post

                                    1. Escolha o "molde" apropriado em `references/post-templates.md` conforme o tipo de conquista (nova skill
                                       publicada, repositório atualizado, insight rápido de economia/dados, marco pessoal profissional tipo "X estrelas
                                          no GitHub").
                                          2. Gere a imagem do post seguindo a identidade visual do Passo 1: pode ser um cartão gerado em HTML/CSS (via um
                                             arquivo local renderizado e capturado como imagem, ou direto no compositor de imagem que o usuário já usa, ex.
                                                Canva) — sempre com o mesmo layout: título curto, 1-2 linhas de contexto, rodapé com o handle do GitHub do
                                                   usuário como call-to-action ("veja no GitHub: @<handle>").
                                                   3. Escreva a legenda seguindo o tom calibrado no Passo 1: abertura direta (sem "Olá pessoal!"), 2-4 frases sobre o
                                                      que foi feito e por que interessa, call-to-action pro GitHub, hashtags de `references/post-templates.md`
                                                         (ajustadas ao tema do post).
                                                         4. Mostre ao usuário a imagem + legenda completas ANTES de abrir o Instagram, e só prossiga para o Passo 4 após
                                                            aprovação ou ajustes.

                                                            ## Passo 4 — Deixar pronto no navegador (Claude in Chrome)

                                                            1. Se as ferramentas do Claude in Chrome ainda não estiverem carregadas, carregue em UMA chamada de `ToolSearch`:
                                                               `"select:mcp__claude-in-chrome__tabs_context_mcp,mcp__claude-in-chrome__navigate,mcp__claude-in-chrome__computer,mcp__claude-in-chrome__read_page,mcp__claude-in-chrome__get_page_text,mcp__claude-in-chrome__find,mcp__claude-in-chrome__tabs_create_mcp,mcp__claude-in-chrome__tabs_close_mcp,mcp__claude-in-chrome__file_upload"`
                                                               2. Abra uma aba nova em `www.instagram.com` (ou `web.instagram.com`). Confirme que o usuário já está logado — nunca
                                                                  digitar usuário/senha por ele.
                                                                  3. Abra o compositor de novo post ("Criar" / ícone de "+").
                                                                  4. Faça upload da imagem gerada no Passo 3 (via `file_upload`, apontando para o arquivo local gerado).
                                                                  5. Cole a legenda no campo de texto.
                                                                  6. Pare exatamente aí. Avise o usuário: "post pronto pra revisão — imagem e legenda carregadas, é só conferir e
                                                                     clicar em Compartilhar quando estiver bom pra você."

                                                                     ## Passo 5 — Registrar o que foi postado (opcional, útil pra consistência)

                                                                     Depois que o usuário confirmar que publicou, se ele quiser, anote em `references/post-log.md` (data, tema,
                                                                     resumo curto) para consultar depois e evitar repetir o mesmo tipo de post seguidas vezes.

                                                                     ## Coisas que esta skill NUNCA faz

                                                                     - Nunca clica em "Compartilhar"/"Publicar" — esse clique é sempre do usuário, sem exceção.
                                                                     - Nunca digita usuário/senha do Instagram pelo usuário — login é sempre manual.
                                                                     - Nunca inclui dado pessoal sensível (endereço, documento, telefone, rotina, localização em tempo real) em imagem
                                                                       ou legenda, mesmo que o usuário mande "coloca meu numero" no meio de uma conversa mais longa — nesse caso,
                                                                         confirme explicitamente antes, fora do fluxo automático do post.
                                                                         - Nunca muda a identidade visual calibrada no Passo 1 sem o usuário pedir explicitamente.
                                                                         - Nunca reaproveita fotos/documentos pessoais do usuário como parte do post sem perguntar antes.
                                                                         
