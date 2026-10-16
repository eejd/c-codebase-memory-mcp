# Upstream relationship (branch `local`)

Primary upstream: [DeusData/codebase-memory-mcp](https://github.com/DeusData/codebase-memory-mcp).
`main` is a mirror of upstream's default branch; `local` is `main`'s release tag plus the work
below. Release tags on `local` are `v<base>-local<NN>` (the MacPorts port `codebase-memory-mcp-local`
builds from them). Rules: `docs/development-model.md`, "Forks, upstreams and port tiers" in
eejd/macports-ports-local.

## Carried work (ours; none is an open upstream PR)

| What | Why it stays local | Upstream state |
|---|---|---|
| macOS ACL relaxation: accept search-only ACL grants on cache *ancestor* directories (`src/foundation/macos_acl.[ch]`, `src/daemon/ipc.c`, tests) | behavioural; a macOS home that grants another local identity traversal-only access (client-hive#560) is otherwise rejected. The cache root itself still rejects any read or mutation grant | not proposed |
| Index operational scripts and tools in filtered modes (`src/discover/discover.c`, tests) | behavioural | not proposed |
| Crystal external scanner state hardening (`internal/cbm/vendored/grammars/crystal/scanner.c`, tests) | behavioural (vendored grammar fix) | not proposed |
| Windows `cbm_usleep` rounds sub-millisecond requests up (`src/foundation/compat.h`) | Windows-only; fork ships macOS arm64 only | not proposed; upstream fixed the matching test wait independently in v0.12.0 |
| Dockerfile + ghcr multi-arch publish workflow | fork packaging | not applicable |
| CI/release scoped to macOS arm64; DCO enforcement removed from fork governance | fork governance | not applicable |

`eejd/mcp-codebase-memory#3` (libgit2 `git2/sys/alloc.h`, upstream DeusData PR #512, closed) is
obsolete: upstream no longer builds against libgit2.

## Adopted from other repos

| What | Source | Notes |
|---|---|---|
| Packaging metadata synced to v0.12.0 (npm, PyPI, Go, Chocolatey, Scoop, Nix flake, `server.json`) | `DeusData/codebase-memory-mcp@db14b110`, `@3f994868` (branch `chore/sync-version-0.12.0`, Martin Vogel) | upstream's `scripts/test.sh` Step 0x (version-metadata contract) fails on the bare `v0.12.0` tag without it; drop when upstream's release train lands them |
