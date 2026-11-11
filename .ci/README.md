The package workflow runs entirely on our Runs Spot runners with a fixed
`CI_PROVIDER=l3`. The three large build/test jobs retain their 32 CPU capacity;
WASM builds, Node test matrices, dependent packages, demo builds and artifacts
remain required by the final Check job.

Netlify deployment and npm publishing run only in the upstream repository.
Fork builds still produce and validate the website and demos without publishing
to upstream accounts.

Run `mise run setup-hooks` once, then `mise run check` before pushing. This gate
checks workflow syntax, shell commands and runner routing. The PR workflow runs
the actual package builds and tests; a local workflow check is not a package test
result.

`l3-routing.ts` is vendored from laith-page/migrate commit 208b86d, whose test
suite covers dynamic routing, reusable workflows and external CI activation.
Keep its source identity when updating the shared checker.
