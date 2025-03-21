# Steps:

## Step 1:
- created a sample txt file (using echo) and added some text to it.
- `echo` "In this task, there is a concept called stashing the content, which is used to save the changes temporarily and revert back to the previous state." > sample.txt

## Step 2:
- `git add .` _(to add those changes to the staging area. (that is index))_

## Step 3:
- `git stash` _(to save the changes temporarily and revert back to the previous state)_

## Step 4:
- `git checkout rebase_feature` (to switch to the rebase_feature branch)
- created a new file called file_from_branch under the task-6 folder and add a few contents

## Step 5:
- `git add .` (to add those changes to the staging area. (that is index))
- `git commit -m "File added through rebase_feature branch"`
- `git push origin rebase_feature` (to push the changes to the remote repository)

## Step 6:
- `git checkout main`(to switch back to the main branch)
- `git merge rebase_feature`(to merge the changes from rebase_feature branch to main branch)
- `git push origin main` (to push the merged change to the remote repository)

## Step 7:
- `git stash pop` (to apply the stashed changes back to the current branch)
- `git commit -m "pop the stash"`

### Output:
```bash
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   task-6/sample.txt

Dropped refs/stash@{0} (0bee1a995184e984405c5d238458fa0ba1b2279f)
```

## Step 8: (Stash additional commands)
- `git stash list` (to list all the stashed changes)
### Output:
``` bash
stash@{0}: WIP on main: 3caca7a Readme File created with a steps of rebasing and squashing commits
```

- `git stash show -p "stash@{0}"` (to show the changes in the stash in a detailed view -p)
### Output:
``` bash
diff --git a/task-6/sample.txt b/task-6/sample.txt
new file mode 100644
index 0000000..2a1f388
Binary files /dev/null and b/task-6/sample.txt differ
```

- `git stash drop "stash@{0}"` (to remove the stashed changes from the stash list)
### Output:
```
Dropped stash@{0} (5ddc8460f2357d9d5ca5263cba903e53129899cc)
```
- `git stash clear` (to clear all the stashed changes)