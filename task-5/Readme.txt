Steps:

Step 1:
- created a sample txt file (using echo) and added some text to it.
- echo "Rebase is a process of moving or combining a sequence of commits to a new base commit. " > sample.txt

Output:
- Rebase is a process of moving or combining a sequence of commits to a new base commit.
(File is created) in a main branch

Step 2:
- git add . (to add those changes to the staging area. (that is index))
- git commit -m "Initially sample txt file created in the task-5 (main)" (to commit the changes to the local repository.)

Step 3:
- git checkout -b rebase_feature (to create a new branch)
- echo "In this task, there is concept of git rebasing
- rebase is a process of moving or combining a sequence of commits to a new base commit" > sample.txt
- git add .
- git commit -m "added a 1st point about rebase"

Step 4:
- echo "- it is known as fast-forward merge" >> sample.txt
- git add .
- git commit -m "added a 2nd point about rebase"

Step 5:
- git rebase -i main
- to rebase the feature branch with the main branch interactively
- opened a vim editor with the list of commits in the feature branch
(pick, reword, edit, squash, fixup, exec, drop)

- used a pick for first commit and squash for the second commit
- saved and closed the vim editor

------rebase process will be paused here------
Conflict occurs because the same line is modified in both the branches. 
- open the sample.txt file and resolve the conflict manually

Step 6:
- git add . (to add those changes to the staging area. (that is index))
- git rebase --continue (to continue the rebase process)

Step 7:
- git checkout main
- to switch back to the main branch

Step 8: 
- git merge rebase_feature

Output:
Updating 3f0cf01..2617472
Fast-forward
 task-5/sample.txt | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

Step 9:
- git push origin main
- to push the changes to the remote repository.


--Squashing--:
- It is a process of combining multiple commits into a single commit.
- git rebase -i HEAD~n (n is the number of commits you want to squash)
- When you squash commits, you essentially "merge" the changes from those commits into one
- so the history is simplified and looks cleaner. 

Eg: 
Commit 1: added a 1st point about rebase
Commit 2: added a 2nd point about rebase

```````` After Squashing ````````
Commit 1: added a 1st point about rebase
          (added a 2nd point about rebase)

