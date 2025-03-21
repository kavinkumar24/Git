# Steps:

## Step 1:
- created a main.txt and login_feature.txt file and added some text to it.

## Step 2:
- `git checkout -b "validation_feature"`
- to create a new branch

## Step 3:
- created a **password_validation** and **age_validation** files as a seperate commit

## Step 4:
- `git checkout main`
- to switch back to the main branch

## Step 5:
- `git cherry-pick <commit-hash-of-password_validation>`
- to pick the commit from **validation_feature** branch to main branch
- that **password_validation** module only extract from the **validation_feature** branch to **main** branch 
  without merging the entire branch

## Step 6:
- `git push origin main` (to reflect in a remote repository)