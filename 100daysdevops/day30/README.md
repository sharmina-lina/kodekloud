# DevOpes task : day 30

## Task overview
Reverse the commit history from git repo except 1st two commit.

### Task Implementation
1. Go to the specific directory using cd

2. Check the git Branch using 
```bash 
sudo git branch 
```
This should be master if not then chnage to master

3. Check the log history of commit
```bash 
sudo git log --oneline
```
4. Check with specific hash number to get the file name

```bash 
sudo git show --name-only 2bbdfed
```
2bbdfed is the hash number of specific commit

5. Create a new branch and switch to that branch
```bash 
sudo git checkout --orphan newbranch
```
take the hashnumber of the specific commit

6. Remove everything first
```bash 
sudo git rm -rf .
```
7. Then commit to an empty repo
```bash
sudo git commit --allow-empty -m "Initial commit"
```
 
8. Restore data.txt from the commit
```bash
sudo git show 2bbdfed:cluster.txt | sudo tee cluster.txt > /dev/null
sudo git show 2bbdfed:info.txt | sudo tee info.txt > /dev/null

```
'abc1234' is the hash number of previous commit

9.  Stag and commit file
```bash
git add cluster.txt info.txt
git commit -m "add data.txt file"

```

10. Replace the old branch with new one
```bash
git branch -M master
git push origin master --force

```

This is alla bout the task


