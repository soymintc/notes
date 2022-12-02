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
