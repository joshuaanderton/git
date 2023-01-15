# Git Workflow for SaaS teams...
**The following is a set of tips, settings, and tools, that make up the best team Git worklow I've used working with several different SaaS teams and dev shops.**

I want to clarify that every team is different.

### Setup
1. Assign branch protection rules
  - Assign rules to `staging` and `master` branches ([view template](/joshuaanderton/git/blob/master/branch-protection-rules.md))
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
- Mega-readable Git history for `staging` branch (via [rebase](/joshuaanderton/git/blob/master/how-tos/rebase.md) & squash-and-merge)

### Developer Workflow
Once work requirements have been **_well documented_** (template coming soon...), assigned dev will:
1. Break task/project into small working branches
2. First working branch will branch off of staging, second branch off of first branch, etc.
3. When work is finished, last branch will be _rebased on to_ prior branch and then _merged in to_ it (continue this back to first branch)
4. Prep for PR:
  - Commit history cleaned up via interactive rebase (to make code easier to review)
5. Pull Request is created
6. Branch off of PR branch to make any suggested changes
7. Upon approval, PR is squash-and-merged into `staging`
8. Testing on staging
9. Merge to master (and deploy to prod)


**Every single pull request** - be that a bug/hot fix, a new feature, enhancements/refactoring, etc. - should be broken up into small, easily-reviewable working branches.

It's *highly recommended* that PRs are first planned/broken up and documented somewhere other devs can view and comment on (e.g. GitHub Issues). This is especially valuable for bigger projects which require multiple working branches
