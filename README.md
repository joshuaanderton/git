# Git Workflow for SaaS teams...
**The following is a set of tips, settings, and tools, that make up the best team Git worklow I've used working with several different SaaS teams and dev shops.**

### Setup
1. Configure branch protection rules
2. Implement Build step
  - Triggered by `staging` branch pushes
    - Failed build blocks staging deploy + squash-and-merge to master
  - Triggered by squash-and-merge to `master`
    - Failed build blocks production deploy (yay!)

Those two steps alone will save your team a TON of grief. For example:
- Less prematurely-merged changes to `staging` (which tend to mess up everyone's productivity)
- Virtually no (if set up correctly) unwanted deploys to prod (I probably don't need to explain why...)
- Mega-readable Git history for `staging` branch (via rebase & squash-and-merge)

### Workflow
- Requirements documented (view template)
- Work planned out and broken into working branches (view template)
- 

**Every single pull request** - be that a bug/hot fix, a new feature, enhancements/refactoring, etc. - should be broken up into small, easily-reviewable working branches.

It's *highly recommended* that PRs are first planned/broken up and documented somewhere other devs can view and comment on (e.g. GitHub Issues). This is especially valuable for bigger projects which require multiple working branches