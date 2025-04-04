
# Steps
## Step 1:
- created a sample txt file (using echo) and added some text to it. - main branch
- `echo` "In this tasks, there is a concept of merge conflict resolving." > sample.txt

### Output:
``` bash
- In this tasks, there is a concept of merge conflict resolving.
(File is created)
```

## Step 2:
`- git add .`
- to add those changes to the staging area. (that is index)

## Step 3:
- `git commit -m "Initially sample txt file added under task-4 in main branch"`
- to commit the changes to the local repository.

## Step 4:
- `git checkout -b feature-branch` (to create a new branch)
- `echo` "In this tasks, there is a concept of merge conflict resolving and git diff, git status" > sample.txt

### Output:
``` bash
- In this tasks, there is a concept of merge conflict resolving and git diff, git status
(File is modified in locally)
```

## Step 5:
`- git add .`
- to add those changes to the staging area. (that is index)

## Step 6:
- `git commit -m "Sample txt file also added in the feature-branch"`
- to commit the changes to the local repository.

## Step 7:
- `git checkout main`
- to switch back to the main branch

## Step 8:
- `git merge feature-branch`
- to merge the changes from feature-branch to main branch
During that time there is a conflict occurs because the same line is modified in both the branches.

### Output:
``` bash
Auto-merging task-4/sample.txt
CONFLICT (add/add): Merge conflict in task-4/sample.txt
Automatic merge failed; fix conflicts and then commit the result.
```

## Step 9:
- open the sample.txt file and resolve the conflict manually
- In this tasks, there is a concept of merge conflict resolving.
- In this tasks, there is a concept of merge conflict resolving and git diff, git status

## Step 10:
- `git add .`
- to add those changes to the staging area. (that is index)

## Step 11:
- `git commit -m "Resolved merge conflict between main and feature-branch"`
- to commit the changes to the local repository.

## Step 12:
- `git log --oneline`
### Output
``` bash
cf2c7bc (HEAD -> main) Resolved merge conflict between main and feature-branch
ab1d345 (feature-branch) Sample txt file also added in the feature-branch
1cf7622 Initially sample txt file added under task-4 in main branch
3511988 (origin/main) Readme file updated with the steps remaining
adb2e6a Revert "Added a few more text regarding revert and reset"
3ea9b24 Added a few more text regarding revert and reset
065c4e7 readme text file included - about creation and restoring contents in file
a7446dd Initially a sample text file is created
```


## Step 13:
- `git push origin main`
- to push the changes to the remote repository.

## Step 14:
- `git diff main..feature-branch`
- to check the difference between the main and feature-branch

### Output:
``` bash
diff --git a/task-4/Readme.txt b/task-4/Readme.txt
deleted file mode 100644
index ec10c72..0000000
--- a/task-4/Readme.txt
+++ /dev/null
@@ -1,71 +0,0 @@
-Step 1:
-- created a sample txt file (using echo) and added some text to it. - main branch
-- echo "In this tasks, there is a concept of merge conflict resolving." > sample.txt
-
```
