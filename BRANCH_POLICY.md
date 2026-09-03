# SlncTrZ Repository Branch Policy

## Canonical branch

For new and actively maintained original repositories, `main` is the canonical development history and should be the GitHub default branch.

- Start feature/fix branches from `main`.
- Merge completed work back into `main`.
- Keep `main` pushable, testable, and representative of the real development history.
- Publish releases with `v*` tags from the canonical history.
- Do not create a disconnected squash-only release history: it hides real development ancestry and breaks contribution attribution.

## Temporary branches

Feature, fix, experiment, and agent work branches are temporary. Once integrated and no longer needed, they should be deleted or archived rather than becoming permanent parallel histories.

## Legacy repositories

Repositories that already use `master` may remain on `master` until a deliberate migration can be completed safely. Migration should include CI/docs/default-branch references in the same change. Do not rename a branch merely for cosmetic consistency while the worktree is dirty or deployment automation still depends on the old name.

## Forks

Forks may retain the upstream project's branch convention when that reduces merge/rebase friction. `Odysseus`, for example, follows its upstream `dev` workflow and is not required to conform to the original-repository rule.

## Git transport

Development hosts with the owner's GitHub SSH key should use SSH origins (`git@github.com:SlncTrZ/<repo>.git`) so fetch/push behavior is consistent and does not depend on an interactive HTTPS credential helper.

## Contribution graph

GitHub contribution attribution depends on commits being pushed and reachable from the repository's default branch (or otherwise qualifying under GitHub's contribution rules). Local-only commits and long-lived work on a non-default branch may therefore be absent from the profile snake until they are pushed/integrated or that branch becomes the GitHub default.
