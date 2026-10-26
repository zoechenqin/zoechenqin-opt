# Dependency Report

## Source
- Repository: https://github.com/codimango/aai-labs-scenelab
- Base commit: b76081c803fc72e5df29f85753ffaba591409ae8
- Source handoff: docker_clone_required (public repo cloned in Dockerfile)

## Base image
`public.ecr.aws/docker/library/node:20-bookworm-slim`
- Basis: `.nvmrc` declares Node 20; `package.json` engines field confirms `>=20`.

## System packages (apt)
| Package | Reason |
|---------|--------|
| git | Required for repo clone in Dockerfile |
| findutils | Provides `find`; used in trajectory |
| grep | Used extensively in trajectory for searching color codes |
| procps | Provides `ps`/`pkill`; listed in apt_package_hints |

## Node / pnpm
| Tool | Version | Source |
|------|---------|--------|
| Node.js | 20 (bookworm-slim) | `.nvmrc` |
| pnpm | 9.15.0 | `packageManager` field in `package.json` |

Installed via `corepack enable && corepack prepare pnpm@9.15.0 --activate`.
Dependencies installed with `pnpm install --frozen-lockfile` from the committed `pnpm-lock.yaml`.

## Trajectory-derived additions
None. The Muse session used only coreutils (grep, cat, ls, head, sort, wc, xargs, uniq) and pnpm, all of which are either present in the base image or installed via apt/corepack above. No additional packages were added from trajectory evidence.

## Excluded
- No Python packages (python3 listed in apt_package_hints but not observed as required in session).
- No playwright/browser dependencies (playwright is a devDependency but was not invoked during the session).
