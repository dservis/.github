# .github

Arquivos padrão da organização **dservis**. O que está aqui é herdado
automaticamente por todo repositório da organização que não definir o seu próprio.

## Conteúdo

```
.github/
├── workflows/
│   ├── dotnet-ci.yml           # CI reutilizável para soluções .NET
│   └── flutter-ci.yml          # CI reutilizável para apps Flutter
├── PULL_REQUEST_TEMPLATE.md    # corpo padrão de todo pull request
└── ISSUE_TEMPLATE/
    ├── config.yml              # configuração do seletor (nome reservado)
    ├── 01-bug.yml              # 🐛 Bug
    ├── 02-feature.yml          # ✨ Feature
    ├── 03-task.yml             # 🛠️ Task
    └── 04-config-change.yml    # ⚙️ Config
```

## Como a herança funciona

- Vale apenas para repositórios da organização **sem** pasta `.github/ISSUE_TEMPLATE` própria.
- A herança é **tudo ou nada**: se um repositório definir qualquer template ou
  `config.yml` próprio, nenhum arquivo daqui é usado naquele repositório.
- Este repositório precisa permanecer **público** para que a herança funcione,
  mesmo que os repositórios que a consomem sejam privados.

## Workflows reutilizáveis

Um repositório consome o CI da organização em poucas linhas:

```yaml
jobs:
  ci:
    uses: dservis/.github/.github/workflows/dotnet-ci.yml@v1
    permissions:
      contents: read
```

| Workflow | O que faz | Inputs principais |
|---|---|---|
| `dotnet-ci.yml` | restore, build com `ContinuousIntegrationBuild`, testes (TRX publicado), falha em pacote NuGet vulnerável | `working-directory`, `solution`, `test-filter`, `fail-on-vulnerable` |
| `flutter-ci.yml` | `dart format`, `flutter analyze --fatal-infos`, testes com cobertura, APK de release opcional | `build-android`, `api-base-url`, `channel`, `flutter-version`, `check-format` |

**Versionamento.** Consuma sempre por tag (`@v1`), nunca por `@main`: uma
mudança aqui quebraria todos os repositórios de uma vez. Mudança compatível
move a tag `v1`; mudança incompatível cria `v2`.

**Acesso.** Este repositório é público, então qualquer repositório da
organização (inclusive privado) pode chamar os workflows. Se ele virar privado,
habilite Settings → Actions → General → *Access* → "Accessible from repositories
in the organization".

**Permissões.** Os workflows pedem só `contents: read`. O chamador precisa
declarar `permissions` no mínimo igual, como no exemplo acima.

## Labels

As labels declaradas nos templates precisam **existir no repositório onde a issue
é aberta**, senão são silenciosamente ignoradas. GitHub não tem label de organização.

Labels usadas: `bug`, `enhancement`, `task`, `config`, `triage`.
`bug` e `enhancement` já vêm por padrão; as outras três precisam ser criadas.

```bash
for repo in $(gh repo list dservis --limit 200 --json name -q '.[].name'); do
  gh label create task    -R "dservis/$repo" -c "0E8A16" -d "Trabalho técnico sem mudança visível" --force
  gh label create config  -R "dservis/$repo" -c "5319E7" -d "Mudança de configuração ou infraestrutura" --force
  gh label create triage  -R "dservis/$repo" -c "D4C5F9" -d "Aguardando triagem" --force
done
```

## Como alterar um template

Edite o `.yml` e abra PR. A mudança passa a valer para toda a organização assim
que entrar na `main` — não há build nem publicação.
