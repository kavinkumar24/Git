# Comprehensive Workflow with Forced Pushes and Recovery
## Steps:

_for this scenario lets take an **banking application**, in that there are many features are available like main, user-authentication, transaction, releases, etc. for this lets take only 3 branches (user-auth, transaction, releases) apart from main_
### Step 1:
- created a `dashboard.txt` in a main branch
- Added to staging Area
``` bash 
git add .
```
- Save that changes locally
```` bash 
git commit -m "Added a dashboard txt file in task-10/main branch"
````

### Step 2:
- created  a new branch called `feature/user-authentication`
```` bash 
git checkout -b feature/user-authentication 
````
- created a `user-auth.txt` file and add some more text
- totally 3 different commit made in that file
_User authentication and access control_ - Commit 1
_Two step verification added_ - Commit 2
_Added Passkey authentication option in user-auth branch_ - Commit 3

### Step 3:
- created the another branch called `bugfix/transaction-fix`
```` bash 
git checkout -b bugfix/transaction-fix 
````
- created a `transaction.txt` file and add some more text to it
```` bash 
git add . 
````
```` bash 
git commit -m <"message"> 
````
### Step 3:
- created the final branch called `release/vl .0.0`
````bash   
git checkout -b release/vl .0.0 
````
- created a two files called `release-notes.txt` and `build.txt`
- Added 2 commits in `release-notes.txt` and 3 commits in `build.txt`
```` bash 
git add . 
````
```` bash
 git commit -m <"message"> 
 ````

### Step 4:
- then in the `feature/user-authentication` branch _rebase_ the commands and perform _reword_ operation

````bash  
git rebase -i HEAD~3 
```` 
- changed the pick command to reword for changing the commit message
 ```` bash 
 git push --force origin feature/user-authentication 
 ````

### Step 5:
- In release branch there is a three commit in the build file, so under build 1 _(build 2 and 3 are squashed)_
```` bash
 git rebase -i HEAD~3 
 ```` 
```` bash
  pick
  squash 
  squash 
 ````
- Then push the changes to the remote
````bash
 git push origin release/v1.0.0 
 ````
- then I accidentally remove that commit by using 
````bash 
 git reset --hard HEAD~1 
 ````
- also pushed to the remote origin
- later find that commit is important
#### use a reflog to save that commit
````bash
 git reflog 
 ````
- after that a all the record will be shown, from that take the hash id of lost one

````bash
 git checkout -b recover-build-commits fca8c78 
````

- this command will create a new branch and recover that build commits

### Step 6:
- merge that `recover-build-commits` into a release/v1.0.0 _(By creating a pull request)_
- merge all those branches to the main by one by one

## Why Force Pushes Should Be Handled with Care
- **Risk of Overwriting Work**: Force pushing rewrites remote history, potentially overwriting others’ work.
- **Loss of Commits**: If you remove or alter commits, they can be lost unless you have a backup (like git reflog).
- **Team Conflicts**: Team members may face conflicts or errors if they pull outdated history after a force push.

## Reflog as a life saver
- **Tracks All Actions**: It records every action that changes the state of your repository, such as commits, resets, merges, and rebase operations. Even actions that discard commits (e.g., git reset, git rebase) are recorded.

- **Recovers Lost Commits**: If you lose commits due to a mistaken force push, reset, or rebase, git reflog lets you find the previous state of your branch and recover those commits.

- **Helps with Branch Recovery**: If a branch is deleted or its history is rewritten, git reflog can help you locate the previous commits and bring the branch back.
```` bash
git checkout -b recover-branch <commit-hash>
````
## Best Practices for Collaborating with Teams
- Avoid Force Pushing to Shared Branches

- Use `git push --force-with-lease`: This is a safer option than `git push --force`, as it ensures you don’t overwrite someone else’s changes.
- Communicate with the team before rewriting