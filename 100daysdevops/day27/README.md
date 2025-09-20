# Git Revert Task

## Task Description
Inside the Git repository located at `/usr/src/kodekloudrepos/cluster`, the latest commit (`HEAD`) needed to be reverted back to the previous commit.  
The previous commit was the initial commit of the repository.

A new revert commit was created with the commit message written in all lowercase as:

## Steps Performed

1. Navigate to the repository:
   ```bash
   cd /usr/src/kodekloudrepos/cluster

2. Check commit history to identify the latest commit:
```
sudo git log --oneline
```
3. Revert the latest commit:
```
sudo git revert HEAD --no-edit
```
4. Update the commit message to the required format:
```
sudo git commit --amend -m "revert cluster"
```