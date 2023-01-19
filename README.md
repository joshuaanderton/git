# Git workflow for dev teams
**The following is a set of tips, settings, and tools, that make up the best team Git worklow I've used working with several different SaaS teams and dev shops.**

I want to clarify that every team is different.

### Setup
1. Assign branch protection rules
  - Assign rules to `staging` and `master` branches ([view template](branch-protection-rules.md))
2. Create and trigger GitHub Actions (via GitHub Actions, GitLab Circle CI, etc.)
  - Code Linting
  - Style & Dependency checks
  - Build
    - Triggered by:
      - Merges to `staging` branch - after approved PR is squash-and-merged in
      - Merges to `master`
  - Deploy
    - Triggered by:
      - Build passes for merge to `master`

Those steps alone will save your team a TON of grief. For example:
- Less prematurely-merged changes to `staging` (which tend to mess up everyone's productivity)
- Virtually no (if set up correctly) unwanted deploys to prod (I probably don't need to explain why...)
- Mega-readable Git history for `staging` branch (via [rebase](how-tos/rebase.md) & squash-and-merge)

## Developer Workflows
Depending on the project/task (e.g. the type or scope size of work assigned, the size of the team, etc.) one of these options may work better. Of course, all of this should be iderated on to best suite your team's needs and preferred workflow (don't keep doing what isn't working and ***don't*** stop doing what is).

#### Single-branch Developer Workflow (e.g. bug fixes or enhancements with few changes, easily-reviewable as one PR)
Once work requirements have been **_well documented_** (template coming soon...), assigned dev will:
1. Plan task in a GH issue (or similar) for clarity, or incase another dev needs to take over later
2. Branch off of `staging`
3. When work is done, prep for PR by cleaning commit history via [interactive rebase](how-tos/rebase-interactive.md) (to make code easier to review)
4. Submit Pull Request and begin code review
5. Upon approval:
  1. _Rebase on to_ `staging` and force-push (`git push -f`)
  2. PR is squash-and-merged into `staging`
  3. Delete branch
6. Testing on `staging`
7. Branch off of `staging` to address any issues (repeating **Single-branch Developer Workflow**)
8. Merge to master (and deploy to prod)

#### Multi-branch Developer Workflow (e.g. bigger projects that are not easily-reviewable as one PR)
Once work requirements have been **_well documented_** (template coming soon...), assigned dev will:
0. Break assignment into tasks in a GH Issue (or similar). Each task will have it's own working branch.
0. First working branch will branch off of `staging`, second branch off of first branch, etc.
0. When a working branch is ready for review, prep for PR by cleaning commit history via [interactive rebase](how-tos/rebase-interactive.md) (to make code easier to review)
0. Submit Pull Request and begin code review
0. Upon approval:
  0. _Rebase on to_ prior branch (or `staging` if on first branch) and force-push (`git push -f`)
  0. PR is merged (squash-and-merged for less commits in history) into prior branch (or `staging` if on first branch)
  0. Delete branch
0. Once everything is merged and deployed to `staging`, do testing
0. Branch off of `staging` to address any issues (using **Single-branch Developer Workflow**)
0. Merge to master (and deploy to prod)
