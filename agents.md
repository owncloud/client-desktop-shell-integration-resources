# AI Agent Guidelines for Shell Integration Resources

This file provides context for AI coding agents (Claude Code, GitHub Copilot, Cursor, etc.) working in this repository.

## Repository Overview
- **Product family:** Desktop Client
- **Primary language(s):** CMake (build), SVG/PNG/ICNS (assets)
- **Build system:** CMake
- **Test framework:** None
- **CI system:** None

## Architecture & Key Paths
- `SVG/` - Source SVG icons
- `16x16/` through `1024x1024/` - Rasterized PNG icons at various resolutions
- `icns/` - macOS icon files
- `nopadding/` - Icons without padding
- `CMakeLists.txt` - CMake install configuration
- `ownCloudShellResourcesConfig.cmake.in` - CMake config template
- `COPYING` - GPL-2.0 license

## Development Conventions
- **Branching:** master
- **Commit messages:** DCO sign-off required (`git commit -s`)
- **Code style:** Not applicable (icon assets)
- **PR process:** Open a PR against master. All CI checks must pass.

## Build & Test Commands
```bash
# Build/Install
mkdir build && cd build
cmake ..
cmake --build .

# Test
Not applicable

# Lint
Not applicable
```

## Important Constraints
- All code contributions must be compatible with the **GPL-2.0** license
- Do not introduce new **copyleft-licensed dependencies** (GPL, AGPL, LGPL, MPL) without explicit discussion in an issue first. This is especially important for repos migrating to Apache 2.0.
- Do not introduce new dependencies without discussion in an issue first
- Icon changes affect both Dolphin and Nautilus integrations
- Maintain all resolution variants when changing icons


## OSPO Policy Constraints

### GitHub Actions
- **Only** use actions owned by `owncloud`, created by GitHub (`actions/*`), verified on the GitHub Marketplace, or verified by the ownCloud Maintainers.
- Pin all actions to their full commit SHA (not tags): `uses: actions/checkout@<SHA> # vX.Y.Z`
- Never introduce actions from unverified third parties.

### Dependency Management
- Dependabot is configured for automated dependency updates.
- Review and merge Dependabot PRs as part of regular maintenance.
- Do not introduce new dependencies without discussion in an issue first.

### Git Workflow
- **Rebase policy**: Always rebase; never create merge commits. Use `git pull --rebase` and `git rebase` before pushing.
- **Signed commits**: All commits **must** be PGP/GPG signed (`git commit -S -s`).
- **DCO sign-off**: Every commit needs a `Signed-off-by` line (`git commit -s`).
- **Conventional Commits & Squash Merge**: Use the [Conventional Commits](https://www.conventionalcommits.org/) format where the repository enforces it. Many repos use squash merge, where the PR title becomes the commit message on the default branch — apply Conventional Commits format to PR titles as well. A reusable GitHub Actions workflow enforces this.

## Context for AI Agents
- Match existing code style
- Do not refactor unrelated code in the same PR
- Keep PRs focused and atomic
- When modifying icons, provide all required resolutions (16x16 through 1024x1024)
- SVG sources should be kept in sync with rasterized versions
