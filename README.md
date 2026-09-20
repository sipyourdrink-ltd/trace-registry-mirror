# trace-registry-mirror

Read-only mirror of [agentrust-io/trace-registry](https://github.com/agentrust-io/trace-registry), operated by Sip Your Drink Ltd, the maintainers of [Bernstein](https://github.com/sipyourdrink-ltd/bernstein). We are independent of OPAQUE Systems.

| | |
|---|---|
| Mirrored branch | [`main`](https://github.com/sipyourdrink-ltd/trace-registry-mirror/tree/main), byte-identical to canonical `main` |
| Head to compare | `https://api.github.com/repos/sipyourdrink-ltd/trace-registry-mirror/commits/main` |
| Sync | every 6 hours, fast-forward only |
| Security contact | forte@bernstein.run |
| Mirroring since | 2026-09-20 |

## Why this branch exists

`main` must never carry a commit the canonical repository does not have, otherwise its head cannot equal canonical's and a fast-forward is no longer possible. So the sync job lives here, on `mirror-ops`, and `main` is left untouched by us. This branch is the default only because GitHub runs scheduled workflows from the default branch.

## What the sync does

1. Fetches canonical `main`.
2. Checks that canonical `main` descends from the mirror's `main`. If it does not, the job fails and the mirror stays where it was. A red run here means canonical history was rewritten, or this mirror was tampered with; either way the two heads are the evidence.
3. Fast-forwards and pushes.

It pushes with a token scoped to this one repository, because the default Actions token may not push commits that touch `.github/workflows/`, and canonical `main` does change its workflows (10 of its last 50 commits did).

## What this mirror does not do

It accepts no anchoring pull requests, validates no producer keys and runs none of the canonical pipelines. It holds a copy, so that a rewrite of published history has somewhere to be caught.

GitHub pauses scheduled workflows in a repository with no activity for 60 days. If canonical is quiet that long the schedule needs re-enabling by hand; the head comparison above shows a stale mirror as stale, not as in sync.
