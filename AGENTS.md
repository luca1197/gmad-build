# gmad-build — Agent Instructions

## Project Overview
This is a CI/CD automation repo. It has **no application source code** — its sole purpose is to build [`Facepunch/gmad`](https://github.com/Facepunch/gmad) for Linux on a schedule and publish the binary as a GitHub release.

## Structure
```
.github/workflows/build.yml   ← The only meaningful file to edit
.gitmodules                   ← Declares the two submodules
gmad/                         ← Submodule: Facepunch/gmad (source)
bootil/                       ← Submodule: garrynewman/bootil (dependency)
```

## Key Facts
- **Build system**: `premake4` + `make` (Linux only — build cannot run on Windows/macOS)
- **Submodules** are updated automatically by the workflow itself (it commits & pushes updated submodule pointers)
- **Release tag** is always `latest` (rolling release, not versioned)
- **Trigger**: Cron schedule and manual `workflow_dispatch`

## Constraints
- Do not add source files to `gmad/` or `bootil/` — they are git submodules managed upstream
- The workflow requires `contents: write` permission to push submodule updates and create releases
