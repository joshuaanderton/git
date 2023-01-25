# Git workflow for dev teams
**The following is a set of tips, settings, and tools, that make up the best team Git worklow I've used working with several different SaaS teams and dev shops.**

Those steps alone will save your team a TON of grief. For example:
- Less prematurely-merged changes to `staging` (which tend to mess up everyone's productivity)
- Virtually no (if set up correctly) unwanted deploys to prod (I probably don't need to explain why...)
- Mega-readable Git history for `staging` branch (via [rebase](how-tos/rebase.md) & squash-and-merge)

Depending on the project/task (e.g. the type or scope size of work assigned, the size of the team, etc.) one of these options may work better. Of course, all of this should be iderated on to best suite your team's needs and preferred workflow (don't keep doing what isn't working and ***don't*** stop doing what is).

## Branch Protection Rules
Before you start implementing a new workflow, I'd recommend assigning protection rules to `staging` and `master` branches ([view templates](branch-protection-rules.md))

## Single-branch Developer Workflow

**Example:**
Bug fixes or enhancements with few changes, easily-reviewable as one PR.

Once work requirements have been **_well documented_** ([view template](templates/requirements.md)), assigned dev will:
1. Plan task in a GH issue (or similar) for clarity, or incase another dev needs to take over later
2. Branch off of `staging`
3. When work is done, prep for PR by cleaning commit history via [interactive rebase](how-tos/rebase-interactive.md) (to make code easier to review)
4. Submit Pull Request and begin code review
5. Upon approval:
- _Rebase on to_ `staging` and force-push (`git push -f`)
- PR is squash-and-merged into `staging`
- Delete branch
6. Testing on `staging`
7. Branch off of `staging` to address any issues (repeating **Single-branch Developer Workflow**)
8. Merge to master (and deploy to prod)

## Multi-branch Developer Workflow

**Example:**
Bigger projects that should be broken up into multiple code reviews.

Once work requirements have been **_well documented_** (template coming soon...), assigned dev will:
1. Break assignment into tasks in a GH Issue (or similar). Each task will have it's own working branch.
2. First working branch will branch off of `staging`, second branch off of first branch, etc.
3. When a working branch is ready for review, prep for PR by cleaning commit history via [interactive rebase](how-tos/rebase-interactive.md) (to make code easier to review)
4. Submit Pull Request and begin code review
5. Upon approval:
- _Rebase on to_ prior branch (or `staging` if on first branch) and force-push (`git push -f`)
- PR is merged (squash-and-merged for less commits in history) into prior branch (or `staging` if on first branch)
- Delete branch
6. Once everything is merged and deployed to `staging`, do testing
7. Branch off of `staging` to address any issues (using **Single-branch Developer Workflow**)
8. Merge to master (and deploy to prod)
