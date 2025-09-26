# Day 33 of 100days DevOps

## Task Overview
The goal of this task was to:

Fix the Git issues preventing Max from pushing his changes.

Ensure the file story-index.txt contains all 4 story titles.

Correct the typo in the story title "The Lion and the Mooose" → "The Lion and the Mouse".

Successfully push the corrected changes to the origin repository.

## Task Implementation
1. Since the remote master branch had changes from Sarah, Max needed to rebase:
```bash
git pull --rebase origin master

```
2. Open the story-index.txt and change as needed.
3. Add the chaged file 
```bash
git add story-index.txt
git rebase --continue
```
4. Finally push change to the master
```bash
git push origin master
```
