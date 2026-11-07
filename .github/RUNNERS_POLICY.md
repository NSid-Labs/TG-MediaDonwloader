# GitHub Actions — política de execução NSid Labs (2026-11-07)

- Usar preferencialmente runners **self-hosted** na VPS atual (desenvolvimento/CI), com `runs-on: [self-hosted, linux, x64, vps]` quando o runner desse repositório estiver confirmado online.
- Não usar `ubuntu-latest`/GitHub-hosted sem autorização explícita, para evitar consumo de minutos pagos.
- Não criar um runner por novo projeto automaticamente: primeiro avaliar reutilização e disponibilidade de runners a nível da organização; em repositórios privados validar permissões/plano antes de alterar o âmbito.
- Manter a VPS Legacy para produção; não executar builds pesados nem desligar aplicações em produção para gerir CI.
- Android: preservar imagem com JDK 21, Android SDK e ferramentas de assinatura; nunca copiar segredos para logs.
- Workflows: usar `concurrency` com `cancel-in-progress` quando apropriado, `timeout-minutes`, cache, permissões mínimas e evitar triggers duplicados.
- Antes de transferir um repositório entre contas/organizações, inventariar Coolify, webhooks, secrets, GHCR, permissões, runners e dependências; confirmar rollback e fazer smoke test após a transferência.
- Outros agentes de IA devem ler esta política e `AGENTS.md` antes de editar CI/CD.
- Não recriar repositórios apagados pelo proprietário.
