# Task32 of 100days DevOps

## Task Overview
Git rebase

## Task Implementation

1. Login to the storage server

2. CD to the specific directory

3. It should be in the feature branch, if not go the feature branch using
```bash
sudo git checkout feature
```

4. Git rebase with master branch

```bash
sudo git rebase master
```

5. Verify the rebase

```bash
git log --oneline --graph --all
```
6. Finally push the updated branch
```bash
sudo git push origin feature --force-with-lease
```
This is all about the task