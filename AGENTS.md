# Instruções para agentes

Ler [`docs/CI_CD.md`](docs/CI_CD.md) antes de modificar código, workflows, runners ou deploy. Verificar stack e infraestrutura; usar branch e PR; proteger segredos e dados; não declarar deploy concluído sem verificação. Preservar documentação e configuração específica do projeto.

## Norma CI/CD — organizações NSid (2026-11-07)

- Repositórios da **NSid-Labs** (não clínicos) e da **Nsid-Labs-Healthcare** (hospitalares) usam a VPS atual para CI; a **VPS Legacy** é dedicada à produção.
- Para projetos **privados**, preferir os runners partilhados de organização no grupo `CI-Privado`: `runs-on: [self-hosted, linux, x64, vps]`. Compilações Android exigem `runs-on: [self-hosted, linux, x64, android]`.
- Nunca criar um runner novo por repositório sem justificação técnica. Usar o pool partilhado e gerir a concorrência, limites de tempo e caches.
- Não usar `ubuntu-latest`, `ubuntu-24.04` ou GitHub-hosted em projetos privados sem autorização, pois podem consumir minutos do plano. Para repositórios **públicos**, não usar os runners privados partilhados devido ao risco de executar código não confiável.
- Ler `.github/RUNNERS_POLICY.md` antes de mexer em GitHub Actions. Preservar segredos, chaves de assinatura, permissões, GHCR, webhooks e integração Coolify.
- Nunca eliminar nem reconstruir repositórios sem indicação expressa. Para mudanças de deploy, verificar o funcionamento atual, preparar rollback e validar primeiro ambientes de testes.
- As mudanças de CI/CD devem ficar registadas no repositório para que outros agentes de IA sigam esta norma.
