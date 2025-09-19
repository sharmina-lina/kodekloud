## Task Overview
The Nautilus developers are engaged in active development on one of the project repositories located at /usr/src/kodekloudrepos/ecommerce. During testing, several test branches were created, and now they require cleanup. Here are the requirements provided to the DevOps team:



On the Storage server in Stratos DC, delete a branch named xfusioncorp_ecommerce from the /usr/src/kodekloudrepos/ecommerce Git repository.

## Solution
First login to the storage server
 ``ssh natasha@ststor01 ``

CD to the specific folder 
``cd /usr/src/kodekloudrepos/ecommerce``

Check git branch
``sudo git branch``

if this is other than master then move to the master branch
``sudo git checkout master``

delete git branch
```sudo git -d xfusioncorp_ecommerce ```

Task is done
