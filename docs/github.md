# Github
Personal cheatsheet

## Copy file from another branch to a path of current branch
```
git checkout <other-branch-name> -- path/to/your/folder
```

## Switch to a branch in repo (`origin` here)
```
git switch -c branch_name origin/branch_name
```

## Make github shut up about credentials for a while
- Use `git config --global` if you want this to be applied to `~/.gitconfig` instead of `.git/config` (`--local` is the default).
- Another option is to use `--system` but you need admin privileges
```
git config credential.helper store # write on disk
git config credential.helper cache # cache your info
git config credential.helper 'cache --timeout=600' # set a cache timeout (sec)
```

# Reverting to a previous branch without committing
- Source: https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit
- This will revert everything from the HEAD back to the commit hash, meaning it will recreate that commit state in the working tree **as if** every commit after `0766c053` had been walked back. You can then commit the current tree, and it will create a brand new commit essentially equivalent to the commit you "reverted" to.
- (The `--no-commit` flag lets git revert all the commits at once- otherwise you will be prompted for a message for each commit in the range, littering your history with unnecessary new commits.)
- This is a safe and easy way to rollback to a previous state. No history is destroyed, so it can be used for commits that have already been made public.
```
git revert --no-commit 0766c053..HEAD
git commit
```

# Purging sensitive files from history
First install `git-filter-repo`
```bash
git-filter-repo --path /paths/to/results --invert-paths -f  # without -f will get no-fresh-clone error
git remote set origin http://url/of/origin  # somehow remote seems to be removed
git push origin this_branch -f
```
