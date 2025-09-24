# Task 31 of 100 days DevOps

## Task Overview 
stashed changes/restore on git repository

## Task Implementation

1. CD to the given directory

2. Check git stash list using

```bash
Sudo git stash list
```

3. Apply the specific stash (stash@{1})
```bash 
sudo git stash apply stash@{1}
```

4. Stage all chages

```bash
sudo git add . 
```

5. Commit with a message
```bash 
sudo git commit -m "Restored stash@{1} changes"

```
6. Push to the origin repo
```bash 
sudo git push origin main
```


