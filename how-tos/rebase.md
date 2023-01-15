# git rebase
I learned what rebasing was embarrasingly late into my carreer as a developer. But, when I finally did, it literally changed my life (well at least my working life.

The important differentiator between `git rebase` and `git merge` is how it impacts the commit history of the effected branch.


### Merging
When you look at the commit history of a branch after another branch has been merge into it (that was long-winded but I'm trying to be as clear as possible) you'll see all of the commits from both branches ordered by their commit date (as if all of these commits were made to this merged-to branch).

### Rebasing
On the otherhand, when you rebase one branch (aka the branch you're about to merge in to - well call this **Branch A**) on to another (aka the branch you're going to merge - call this **Branch B**), you are rewriting the commit history of the **Branch B** so that all of it's commits happened _after_ all of the commits on **Branch A**.

This makes for a *much* cleaner commit history and is epecially handy when you need to revert a commit that introduced a bug. It also means you'll have virtually no conflicts to resolve during your merge.
