# Guia rápido de escolha de licença

Use este guia para decidir a licença ao publicar uma skill. Na dúvida, MIT é a escolha segura padrão para skills
utilitárias (que é o caso mais comum deste usuário).

- **MIT** (padrão recomendado): máxima permissividade, mínima burocracia. Qualquer pessoa pode usar, copiar,
-   modificar, redistribuir e até vender, desde que mantenha o aviso de copyright e o nome do autor original. Ideal
-     para skills utilitárias pequenas, ferramentas, scripts — o objetivo é ser usada e reconhecida, não restringida.
- - **Apache 2.0**: parecida com a MIT, mas adiciona proteção explícita contra patentes. Só faz sentido se a skill
  -   envolver código mais substancial com risco real de disputa de patente — raro em skills de instrução (Markdown).
  -   - **GPL v3**: "copyleft forte" — qualquer projeto derivado que use este código também precisa ser open source sob a
      -   mesma licença. Só recomendar se o usuário explicitamente disser que quer forçar que qualquer uso futuro do seu
      -     trabalho continue aberto (ele perde a opção de alguém usar sua skill dentro de um produto fechado).
      - - **Creative Commons (CC BY 4.0)**: para conteúdo não-código (texto, documentação pura). Raramente é o caso aqui,
        -   já que skills são majoritariamente instruções versionadas como projeto.
       
        -   ## Regra de decisão
       
        -   1. Se o usuário não pedir explicitamente uma licença diferente, usar **MIT**.
            2. 2. No campo de autor da licença, usar o **handle do GitHub** do usuário (ex.: `@usuario`), não o nome civil
               3.    completo — anonimato é o padrão desta skill (ver "Modo anônimo por padrão" em `references/privacy-scan.md`). Só
               4.   usar o nome completo se o usuário pedir isso explicitamente.
               5.   3. Preencher o ano atual no texto da licença.
                    4. 4. Explicar em uma frase por que essa licença foi escolhida, para o usuário poder discordar antes de publicar.
                       5. 
