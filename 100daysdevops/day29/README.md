# Task 29 of 100daysofdevops

## Task Overview


## Implementation

1. 
Login to the storage server using user max


CD to the directory story-blog

check ```git status``` and ```git log```

2. Login to Gitea UI as Max

Username: max

Password: Max_pass123

3. Create Pull Request

Go to the repository → Pull Requests → New Pull Request

Source branch: story/fox-and-grapes

Destination branch: master

PR title: Added fox-and-grapes story

Submit the PR.

4. Assign Reviewer

Open the newly created PR → Reviewers → Add tom as reviewer.

5. Review & Merge as Tom

Logout from Max.

Login as Tom:

Username: tom

Password: Tom_pass123

Open PR titled Added fox-and-grapes story

Review and Approve

Merge the PR into master.

6. Validation

Confirm the story is now in master:

git checkout master
git pull
cat <story-file>  # verify contents


