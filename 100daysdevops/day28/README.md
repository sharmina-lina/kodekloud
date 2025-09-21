# Task 28

## Task Overview
There are two branches in this repository, master and feature. One of the developers is working on the feature branch and their work is still in progress, however they want to merge one of the commits from the feature branch to the master branch, the message for the commit that needs to be merged into master is Update info.txt. Accomplish this task for them, also remember to push your changes eventually.

## Solution

### Step 1:
login to the storage server first
```ssh natasha@ststor01```

### step 2:
cd to the desired repo 
```cd /usr/src/kodekloudrepos/news``

### 3:
Check git status
```sudo git status``
if this is in feature branch then go the next step or checkout to the feature branch
```sudo git checkout feature``

### 4:
Check the commit history

```sudo git log --oneline```

### 5:
Switch to the master branch
```sudo git checkout master```

### 6:
Cherry-pick the required commit
```sudo git cherry-pick 98754b9```
I fount this number in step 4

### 7:
Push the change to the remote
```sudo git push origin master```

Using this the specific commit from feature branch marged to the master branch