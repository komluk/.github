# komluk

Org-wide defaults and reusable GitHub Actions.

## Reusable workflows

- [`app-ci.yml`](../.github/workflows/app-ci.yml) — single CI used by every app
  in the org: schema-vs-migrations check (Prisma / EF Core), Docker build, push
  to GHCR with an immutable `sha-<short>` tag.

  Caller stub (drop into `<app>/.github/workflows/ci.yml`):

  ```yaml
  on:
    pull_request:
    push:
      branches: [main]
  jobs:
    ci:
      uses: komluk/.github/.github/workflows/app-ci.yml@main
      with:
        app-name: my-app
        orm: prisma            # prisma | efcore | none
      secrets:
        GHCR_PAT: ${{ secrets.GHCR_PAT }}   # only if caller is outside the komluk org
  ```
