# Day 34 of 100 Days devops

## Task Overview
The Nautilus application development team is working with a Git repository located at `/opt/demo.git`.  
A clone of this repository is available under `/usr/src/kodekloudrepos/demo` on the Storage server in Stratos DC.  

The requirement is:
- Merge the `feature` branch into `master`.
- Set up a Git hook so that whenever changes are pushed to the `master` branch, a release tag is created with the format:

## Task Implementation
1. Login to the storage server with the user natasha
2. CD to the specific folder where git is cloned
3. check git branch using
```bash 
sudo git branch
```
It is supposed to the feature. if not checkout to the feature branch


6. Create the post update hook
as I am in demo directory so cd /.git/hooks
then create the hook
```bash
cd /.git/hooks
sudo vi post-update
```
add the below content
```
#!/bin/bash
# post-update hook for auto tagging release

BRANCH=$(git rev-parse --abbrev-ref HEAD)

if [ "$BRANCH" = "master" ]; then
    DATE=$(date +%F)
    TAG="release-$DATE"

    if ! git rev-parse "$TAG" >/dev/null 2>&1; then
        git tag "$TAG"
        git push origin "$TAG"
    fi
fi

```

7. Make this executibale
```bash 
sudo chmod +x post-update
```

8. Now go back to the working repo (/usr/src/kodekloudrepos/demo) and push something to master:
```
cd cd /usr/src/kodekloudrepos/demo

sudo git marge origin/feature

sudo git push origin master

```


9. Verify if the tag created
```bash
sudo git fetch --tags
sudo git tag -l | grep release-
```
