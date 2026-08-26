# Critérios de "apelo de estrela" (star appeal) no GitHub

Use estes critérios para avaliar, entre as ideias de skill propostas pelo GITFABRIC (ou entre skills já existentes), quais valem publicar e quais têm mais chance de ganhar estrelas/adoção no GitHub. Isso é uma avaliação qualitativa para orientar prioridade e não uma métrica exata.

## Sinais de alto potencial

- **Resolve um problema comum e recorrente**, não só um caso hiper-específico do usuário (ex.: "buscar vagas de emprego" tem alcance muito maior que "gerar meu currículo pessoal específico").
- **Fácil de entender em 10 segundos**: o nome e a descrição já deixam claro o que a skill faz e para quem serve.
- **Não depende de contexto/dados que só o usuário tem** — outra pessoa consegue instalar e usar sem precisar adaptar nada (ou adapta só respondendo perguntas, como uma skill genérica bem feita já faz).
- **Preenche uma lacuna** — poucas ou nenhuma skill pública faz a mesma coisa, ou faz de forma pior/mais manual.
- **Tem uma automação real por trás**, não é só um prompt bonito — quanto mais a skill economiza trabalho de verdade (navegação, geração de arquivo, cruzamento de dados), mais impressionante parece.
- **Boa apresentação**: nome memorável, descrição curta e clara, README com exemplo de uso antes/depois.

## Sinais de baixo potencial (não empurrar para publicação, ou publicar como privado)

- Skill hiper-pessoal, com lógica ou conteúdo que só faz sentido para a vida do próprio usuário e não generaliza bem mesmo depois de tentar (ex.: uma skill que monta o currículo de uma pessoa específica).
  → nesses casos, a recomendação certa costuma ser manter privada, ou publicar só a versão genérica derivada dela (se ela tiver uma versão genérica derivada de uma versão pessoal pré-preenchida, publique só a genérica).
- Skill que faz algo trivial que qualquer um resolveria com um prompt de uma linha, sem economia real de esforço.
- Skill com nome/descrição confusos ou genéricos demais para chamar atenção em uma busca ou navegação no GitHub.

## Como apresentar a avaliação ao usuário

Para cada skill avaliada, mostrar em 1-2 frases: o que ela faz, o veredito (publicar como está / generalizar antes / manter privada / não vale a pena publicar) e o motivo ligado aos critérios acima — não só "é boa" ou "é ruim", sempre explicar o porquê em termos de utilidade e alcance.

## Estrutura de repositório que ajuda no alcance

Quando o usuário tiver várias skills publicáveis, considerar propor um repositório "coleção" com um README principal em formato de índice — tabela com nome, descrição de uma linha e link para a pasta de cada skill — em vez de um repositório separado para cada skill pequena. Um repositório-coleção bem organizado tende a acumular mais estrelas do que vários repositórios soltos e pouco descobertos. Sugerir também adicionar "topics" no GitHub (ex.: `claude`, `claude-skills`, `ai-agent`, `productivity`, `automation`) na configuração do repositório para melhorar a descoberta via busca — isso é feito na página do repositório, seção "About" → engrenagem de configuração → campo de topics.
