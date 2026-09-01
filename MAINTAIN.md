# codex-multi-auth fork maintenance

This repository delivers and maintains our fork of
[`ndycode/codex-multi-auth`](https://github.com/ndycode/codex-multi-auth).
`/maintain` runs a maintenance cycle from this file; this file is the whole of
what that skill knows about codex-multi-auth.

> **Draft.** Scaffolded 2026-09-01 from the observed state of the fork. Every
> fact below was read off the repository; every line marked **DECISION** is
> yours to settle before the first cycle runs.

## Purpose

Keep a published `integration` branch carrying the behavior we need ahead of
upstream, rebuilt on current upstream every cycle.

**DECISION — does this fork have a reason to exist?** Two findings argue it may
not:

- **Upstream merges us.** Nine offers, eight merged, usually within days:
  #664, #665, #670, #671, #674, #676, #682, #683. Only #660
  (`fix/app-server-canonical-home`) was closed. An upstream this receptive is
  one to contribute to, not fork.
- **Nothing consumes the fork.** `codex-swap` depends on
  `codex-multi-auth@2.10.0` from **npm** — upstream's published package — not
  on this fork. The fork has no downstream binding today.

If both hold, the honest outcome is to offer the three carried commits upstream
and retire the fork rather than maintain it.

## Upstream

- Bound checkout: `fork/`. `origin` is `ndycode/codex-multi-auth`; `fork` is
  `possibilities/codex-multi-auth`.
- Contribution conventions: direct pull requests are normal and land fast.
  Offers keep `fix/`–`feat/` names; they are never renamed to `carry/`, because
  renaming a remote branch closes its request.
- Landed means current `ndycode/codex-multi-auth:main` satisfies the inventory
  entry, confirmed by reading and exercising that code.

## Branch model

- Mirror branch: `main`, an exact mirror of upstream `main`.
- Integration branch: `integration` — every carry composed together, and the
  only ref a consumer may bind.
- Carries: `carry/<feature>`, one per current inventory entry, each merged into
  Integration.
- Offers: `fix/<name>` or `feat/<name>`, cut fresh from current `origin/main`.
- Deletion marker prefix: `DELETEME/`. Creating, moving, or removing
  `DELETEME/<original-name>` requires an explicit human decision naming that
  branch. Maintenance never infers deletion from branch age, ownership,
  request state, or namespace. Every undeclared fork head remains unchanged.
- Open pull-request heads: validated. Reconciliation confirms the exact head
  of each currently open request from the fork but does not acquire ownership
  of the ref.
- `scripts/reconcile-branches.sh` is this repository's entrypoint to the
  shared branch script; it declares these values and nothing else.
- Supervision: `scripts/reconcile-branches.sh --configure-supervision`
  converges this model into the bound checkout's own `supervisor.*` git
  config, which is where advisory tools read it — `/tend` judges a worktree
  against Integration and never proposes removing a carry head's worktree.
  `--check-supervision` verifies that convergence and that this section still
  names these branches. The config is derived state, not a second declaration.
- Declared to supervision: `scripts/reconcile-branches.sh
  --configure-supervision` converges `supervisor.checkout` onto **this
  workshop** — one absolute path per bound fork, multi-valued — so a tool that
  discovers the workshop follows it to forks nested anywhere without walking
  the filesystem. It converges `supervisor.carryPrefix` (multi-valued) and
  `supervisor.carryRef` (multi-valued, exact branch names) onto each bound
  checkout. A carry that predates the naming convention is named by ref rather
  than renamed, because renaming a published branch is a publication.

## Features

Integration carries exactly three commits over upstream `3fce0cb0` (v2.10.0):

| Commit | Subject | Status |
|---|---|---|
| `a0d31eb5` | retry healthy pinned accounts within bounds | **DECISION** — shares its subject with **merged** PR #683; likely superseded. Verify against upstream and retire if landed. |
| `56ab515e` | keep pinned retry safeguards scoped and truthful | **DECISION** — offer upstream, or carry with a stated reason. |
| `d303e37c` | keep refresh diagnostics pin-scoped | **DECISION** — offer upstream, or carry with a stated reason. |

None of the three exists on any published fork ref: they are local-only. The
first cycle must publish or retire them; until then this workshop's disk is
their only copy.

Nine `fix/*` branches remain in the checkout from landed or closed offers. They
carry nothing Integration needs and are retired once their inventory entry is
confirmed landed.

## Gate

Run verbatim from the candidate worktree:

```sh
npm ci
npm run lint
npm run typecheck
npm test
```

`npm test` is `vitest run --maxWorkers=1`; the single worker is upstream's own
choice and is not relaxed here. No external proof is required: upstream runs no
hosted CI we depend on, and the fork publishes no binary.

**DECISION — unproven.** These are upstream's declared scripts, read from
`package.json`, but this gate has not yet been executed end to end. The first
cycle must run it and record the result in `SCRATCHPAD.md`.

## Consumer

**DECISION — there is no consumer today.** `codex-swap` binds upstream's npm
package. Either bind `codex-swap` to this fork's Integration, or accept that the
fork ships nothing and retire it.

## Notify

- Title: `codex-multi-auth Maintenance`
- Group: `multipass.maintain`
