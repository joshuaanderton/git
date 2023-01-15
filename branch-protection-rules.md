# Suggested Branch Protection Rules
**Note:** these suggestions are based on GitHub's available branch protection rules

### For main working branch (e.g. `staging` or `dev`)
- Require a pull request before merging
  - Require approvals
    - Dismiss stale pull request approvals when new commits are pushed
    - Require review from Code Owners
    - Allow specified actors to bypass required pull requests (assign 1-2 devs for security reasons)
    - Require approval of the most recent push
- Require status checks to pass before merging
  - Require branches to be up to date before merging
- Require conversation resolution before merging
- Require linear history
- Require deployments to succeed before merging
- Lock branch
- Do not allow bypassing the above settings

### For default/base branch (e.g. `master` or `main`)
- Require status checks to pass before merging
  - Require branches to be up to date before merging
- Require deployments to succeed before merging (if deployments are configured, staging deploy should bew required to pass)
- Lock branch
- Do not allow bypassing the above settings
