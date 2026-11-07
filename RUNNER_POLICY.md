# CI/CD infrastructure policy

**vps_legacy** is production only: Coolify, apps and databases; no builds or GitHub runners.
**vps_atual** is development: AI suite, staging, GitHub self-hosted runners and Android builds, with resource and concurrency limits.

GitHub personal-account runners are repository-scoped, not automatically shared across repositories. Centrally manage registrations without creating one permanent runner container per new repository. AI agents must inspect workflows and runner labels before changes; do not silently use GitHub-hosted ubuntu-latest. Validate replacement runner, successful CI and absence of active jobs before retiring Legacy runners. Build on development and deploy remotely to production. Restrict untrusted PRs.

Canonical policy: https://github.com/NunoSid/projeto-padrao/blob/main/RUNNER_POLICY.md
Migration is in progress until verified.
