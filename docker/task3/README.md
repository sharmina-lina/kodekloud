# Docker Task 3

## Task Overview
Delete the kke-container on App Server 3 in Stratos DC.

## Implementation details

### Step 1:
Login to the app sesrver 3

### Step 2:
Run the command to stop the container
```docker stop kke-container```
then run command to delete the container
```docker rm kke-container```

kke-container removed successfully.
we can check using ```docker ps```