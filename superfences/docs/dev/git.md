# git Commands
## Cloning
### Clone a remote repository
`git clone SSH_OR_HTTPS_CLONE_STRING`

## Reviewing
### Check the current branch and untracked changes
`git status`

### Review uncommitted changes
`git diff FILE`

## Branching
### Create a new local branch
`git branch BRANCH_NAME`

### Change branches
`git checkout BRANCH_NAME`

### Read local branches
`git branch`

### Read remote branches
`git branch -r`

### Delete a local branch
`git branch -d BRANCH_NAME`

### Delete a remote branch
> NOTE: Before a deleting a remote branch, you should check that it has been merged back to master, main, or develop, e.g.
> `git checkout develop`
> `git merge old-branch-to-delete`
> Expected output:
> `Already up to date.`

Delete the remote branch with the below command:
`git push -d REMOTE_NAME BRANCH_NAME`
e.g.
`git push -d origin old-merged-feature`

## Committing

1. Add files to the 


## Pushing

### Push a new local branch to a remote repo
`git push --set-upstream origin BRANCH_NAME`

