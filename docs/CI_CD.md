# Padrão de CI/CD e runners — NS Labs

> Política de desenvolvimento para agentes de IA e colaboradores. Este documento descreve o padrão desejado; **não comprova que o runner, os secrets ou o deploy estejam configurados neste repositório**.

## Leitura obrigatória antes de alterar código
1. Ler `AGENTS.md` (se existir), `README.md`, `docs/DEPLOY.md` e workflows atuais. Preservar instruções específicas do projeto.
2. Identificar linguagem, gestor de pacotes, comandos reais de lint/test/build, serviços, base de dados, branch principal e destino de deploy. Nunca copiar um workflow de outra stack sem adaptar.
3. Registar em PR o que foi verificado e o que permanece por configurar.

## GitHub Actions / runners
- Preferir runner **self-hosted** dedicado, com labels `self-hosted`, `linux`, `x64`, `vps`, **apenas após confirmar** que está online, autorizado e com ferramentas necessárias.
- Usar `runs-on: [self-hosted, linux, x64, vps]` apenas se essas labels estiverem efetivamente disponíveis. Se não estiverem, não ativar um workflow que ficará eternamente em fila.
- Pipeline mínimo em pull requests: checkout, instalação com lockfile, lint, testes e build; adaptar à stack. Usar permissões mínimas, versões de actions fixadas, cache apropriada e timeouts.
- Em `main`, após validações, construir artefacto/imagem versionada e efetuar deploy via integração autenticada com **Coolify**, apenas para projetos cujo destino esteja confirmado.
- Nunca expor secrets em logs, commitar tokens, nem dar acesso de produção a workflows de PRs externos. Não executar código não confiável num runner persistente com credenciais.
- Deploy de produção: controlar concorrência, exigir health check, prever rollback e não apagar volumes/dados. Preferir separação entre runner de build e executor de deploy.
- Projetos Android: preservar keystore e assinatura; build APK/AAB e testes apropriados; **não** tratar como aplicação web Coolify.
- Projetos arquivados, experimentais ou sem deploy: CI apenas, salvo decisão explícita.

## Contrato de entrega para qualquer IA
- Trabalhar em branch e PR, sem push direto para `main`, salvo instrução expressa do proprietário.
- Documentar no PR: comandos executados, resultados, workflow alterado, requisitos de runner, secrets necessários (nomes, nunca valores), configuração Coolify, rollback e eventuais pendências.
- Não afirmar que o deploy foi feito sem confirmação de execução e health check.
- Se o runner ou integração Coolify não estiverem disponíveis, entregar configuração segura e identificar bloqueio; não inventar sucesso.

## Novo projeto
Usar `NunoSid/projeto-padrao` como referência, adaptar workflows à tecnologia e preencher `docs/CI_CD.md` com comandos reais, labels disponíveis, variáveis, ambiente de staging/produção e processo de recuperação.
