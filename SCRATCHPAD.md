# Maintenance scratchpad

This is current state for `/maintain`. The skill updates or removes stale
entries on every maintenance cycle and appends one compact history entry.

## Baseline

- Last completed maintenance: **none**. This workshop was scaffolded
  2026-09-01 and no cycle has run.
- Delivered upstream base: `3fce0cb0e819d947266011a5f235ade53631f13c`
  (`ndycode/codex-multi-auth:main`, "docs(release): write the v2.10.0 notes
  and changelog entry").
- Audited-upstream frontier: **none**. No audit has been performed.
- Local integration: `d303e37c51b88c7e98033b39499431745557f70a`.
- Published integration: `7712608351782f9772aea1d4d0e52b1334e25707` —
  **behind local**. The three carried commits below exist on no published ref.

## Carry heads

None declared. Integration carries three commits directly, with no
`carry/<feature>` branch for any of them — a departure from the branch model
that the first cycle must resolve:

- `a0d31eb5` retry healthy pinned accounts within bounds
- `56ab515e` keep pinned retry safeguards scoped and truthful
- `d303e37c` keep refresh diagnostics pin-scoped

## Fork namespace

Nine `fix/*` heads remain from landed or closed offers. They are undeclared
and reconciliation leaves them unchanged.

## Offers

Eight merged upstream (#664, #665, #670, #671, #674, #676, #682, #683); one
closed (#660, `fix/app-server-canonical-home`). None open.

## Notes that can change a later decision

- **No consumer binds this fork.** `codex-swap` depends on
  `codex-multi-auth@2.10.0` from npm — upstream's package.
- `a0d31eb5` shares its subject with merged PR #683 and may be superseded.
- The gate in `MAINTAIN.md` has never been executed.

## History

- **2026-09-01** — Workshop scaffolded; fork moved from `~/src/codex-multi-auth`
  to `fork/`. No maintenance cycle run.
