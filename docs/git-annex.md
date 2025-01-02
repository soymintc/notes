# `git-annex`
Personal cheatsheet

## Remove corrupted data
```bash
git annex drop --force $FILE --from $REPO
rm $FILE
git annex sync
```
