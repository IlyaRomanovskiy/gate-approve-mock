# gate-approve-mock

Rehearsal sandbox for **environment-gated deploy waves** in GitHub Actions.
Nothing real is deployed — every "deploy" is an echo with a short sleep.

## What it shows

The workflow **Batch Deploy Gate Mock** mirrors a batch-deploy shape:

`Plan → Approve server 1 (pause) → deploys to server 1 → Approve server 2 (pause) → deploys to server 2 → Report`

Each **Approve server N** job carries `environment: batch-gate-test`. If that
environment has a *required reviewers* rule, the run pauses there until a reviewer
clicks **Approve** in the run UI ("Review deployments"). **Reject stops the wave** —
later jobs stay skipped, the Report still runs.

## Setup (once)

1. Repo **Settings → Environments → New environment** → name: `batch-gate-test`.
2. Tick **Required reviewers**, add the reviewers, **Save protection rules**.

## Run

Actions → **Batch Deploy Gate Mock** → Run workflow: pick 1–2 apps and 1–2 servers,
untick `dry_run`. Scenarios worth trying: approve both waves; reject the second wave;
leave the pause hanging and watch the run stay "Waiting".
