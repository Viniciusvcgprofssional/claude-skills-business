# Varredura de dados pessoais — regras obrigatórias

Esta é a etapa mais importante da skill. NUNCA pule ou abrevie esta varredura, mesmo que o usuário pareça com
pressa. O objetivo é impedir que dados pessoais do usuário vazem para um repositório público sem ele perceber.

## O que procurar em TODOS os arquivos que serão publicados

Leia cada arquivo (SKILL.md, arquivos em references/, scripts/, assets/, qualquer .md/.txt/.json/.js/.py) e procure:

- **Nome completo** do usuário (e variações/apelidos usados nas conversas)
- - **E-mail** (qualquer string com `@` e domínio)
  - - **Telefone** (sequências numéricas no formato de telefone, com ou sem DDD/código de país)
    - - **Endereço físico** (rua, bairro, cidade+estado combinados de forma identificável, CEP)
      - - **Links pessoais identificáveis**: perfil de LinkedIn pessoal, redes sociais, portfólio com nome próprio na URL
        - - **Documentos**: CPF, RG, passaporte, matrícula universitária, credenciais de certificado com ID
          - - **Currículo/histórico pessoal**: formação específica, empregador específico, trajetória de carreira nomeada
            - - **Chaves, tokens, senhas, credenciais de API** (mesmo de teste) — isso é ainda mais crítico, tratar como bloqueio
              -   automático, nunca publicar de jeito nenhum, nem com aviso
             
              -   ## O que fazer quando encontrar algo
             
              -   1. **Liste tudo o que encontrou**, arquivo por arquivo, trecho por trecho, para o usuário ver exatamente o que
                  2.    seria exposto.
                  3.2. **Nunca decida sozinho publicar dados pessoais.** Sempre apresente as opções ao usuário e espere confirmação
                       explícita antes de prosseguir:
                       - **(a) Genericizar** — reescrever o trecho removendo o dado pessoal, transformando-o em um exemplo genérico ou
                         em uma pergunta que a skill faz ao usuário em tempo de execução (o padrão usado nas skills que já viraram
                         genéricas antes). Esta é a opção recomendada por padrão para skills que fazem sentido ser públicas/reutilizáveis.
                       - **(b) Manter privado** — se o dado pessoal for essencial ao propósito da skill (ex.: uma skill "só minha", como
                         uma versão pré-preenchida com o perfil do próprio usuário), o repositório deve ser criado como **privado** no
                         GitHub, nunca público. Deixe claro para o usuário que "privado" no GitHub ainda significa que o dado sai da
                         máquina local e vai para os servidores do GitHub — não é a mesma coisa que manter só localmente, mas não é
                         visível para terceiros.
                       - **(c) Abortar** — se o usuário não tiver certeza, não publique nada; pergunte de novo depois.
                    3. **Chaves/tokens/senhas**: se encontrar qualquer coisa parecida com credencial (mesmo de teste), remova
                    4.    automaticamente do conteúdo a publicar e avise o usuário — não é uma decisão dele, é bloqueio automático. Se a
                    5.   skill genuinamente precisar de uma variável de credencial, documente isso como `[SUA_CHAVE_AQUI]` ou instrução
                    6.      de variável de ambiente, nunca com o valor real.
               
                    7.  ## Nunca pressupor
               
                    8.  Não assuma que porque uma skill "parece genérica" ela está limpa — sempre rode a varredura completa, arquivo por
                    9.  arquivo, mesmo em skills que você mesmo acabou de generalizar nesta conversa. É comum esquecer um trecho de exemplo
                    10.  com dado real (por exemplo, um e-mail de contato deixado "só de exemplo" que na verdade é o e-mail real do usuário).
               
                    11.  ## Chaves e credenciais — bloqueio automático, sem exceção
               
                    12.  API keys, tokens e senhas NUNCA vão para um repositório, público ou privado, nem com aviso, nem com confirmação do
                    13.  usuário — isso não é uma decisão dele, é uma regra fixa desta skill. Antes de qualquer publicação, procure em TODO
                    14.  o conteúdo (SKILL.md, references/, scripts/, assets/, exemplos de configuração) por padrões como:
               
                    15.  - Prefixos comuns de chave: `sk-`, `sk-ant-`, `sk-proj-`, `AKIA`, `ghp_`, `gho_`, `github_pat_`, `AIza`, `xox[baprs]-`
                         - - Blocos longos alfanuméricos/base64 (20+ caracteres) próximos de palavras como `key`, `token`, `secret`, `password`,
                           -   `senha`, `apikey`, `api_key`, `auth`, `credential`
                           -   - Blocos `-----BEGIN PRIVATE KEY-----` ou similares
                               - - URLs com credenciais embutidas (`https://usuario:senha@...`)
                                 - - Arquivos `.env`, `.env.local`, `credentials.json` ou similares que porventura tenham sido incluídos por engano na
                                   -   lista de arquivos a publicar — remova-os da lista automaticamente, nunca pergunte se pode subir
                                  
                                   -   Se encontrar qualquer coisa desse tipo: remova do conteúdo antes de mostrar o plano de publicação ao usuário, avise
                                   -   que removeu e por quê, e substitua por um placeholder claro (`[SUA_CHAVE_AQUI]`) ou por instrução de variável de
                                   -   ambiente (`os.environ["NOME_DA_VARIAVEL"]`). Sempre adicionar/reforçar no `.gitignore` os padrões `.env`, `.env.*`,
                                   -   `*.key`, `*credentials*`, `*secret*` para reduzir o risco de isso acontecer de novo em publicações futuras no mesmo
                                   -   repositório.
                                  
                                   -   ## Modo anônimo por padrão
                                  
                                   -   A menos que o usuário diga explicitamente o contrário, trate "anonimato" como configuração padrão de toda
                                   -   publicação feita por esta skill:
                                  
                                   -   - **Autoria em LICENSE/README**: use o nome de usuário do GitHub (o handle, ex.: `@usuario`) em vez do nome civil
                                       -   completo do usuário nos créditos de autoria. Só usar o nome completo se o usuário pedir isso explicitamente.
                                       -   - **E-mail de contato**: não incluir e-mail pessoal em nenhum arquivo público. Se a skill precisar de um contato,
                                           -   sugerir usar as "Issues" do próprio repositório do GitHub como canal, em vez de e-mail direto.
                                           -   - **Nenhuma pista de identidade real** (localização exata, empregador, universidade, telefone) deve aparecer em
                                               -   conteúdo que vai para um repositório público, mesmo que pareça inofensivo — trate isso com o mesmo rigor da
                                               -     varredura de dados pessoais acima.
                                               - - Se o usuário quiser deliberadamente ser identificável (ex.: um portfólio pessoal onde a marca é o próprio nome),
                                                 -   isso é uma decisão dele, não um padrão — pergunte e confirme antes de usar dados reais em qualquer publicação.
                                                 -   
