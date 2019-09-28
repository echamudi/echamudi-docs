# Git
## Retrieving deleted or reseted repo
```
git reflog
git checkout -b recovered_test2 <COMMIT e.g. f5c02b8>
```
## Git Branching Model
### Merge to master
```
git checkout master
git merge --no-ff develop -m "Merge from develop"
git checkout develop
```
