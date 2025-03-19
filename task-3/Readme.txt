
Step 1:
- created a sample txt file (using echo) and added some text to it.
- echo "This is a sample text file and in this folder we are going to learn about checkout, revert, reset" > sample.txt

Output:
- This is a sample text file and in this folder we are going to learn about checkout, revert, reset
(File is created)

Step 2:
- git add .
- to add those changes to the staging area. (that is index)

Step 3:
- git status
- to check the status of the files which are modified, added, deleted etc.,
- as it is firs changes under task-3 folder, it will show all the files as untracked.

Output:
  changes to be committed:
  new file:   task-3/sample.txt


Step 4:
- git commit -m "Initially a sample text file is created"
- to commit the changes to the local repository.

Step 5:
- git push origin main
- to push the changes to the remote repository. 

Step 6: 
- after that modify the sample.txt file and add some more text to it.
- echo "This is a sample text file and in this folder we are going to learn about checkout, revert, reset and restore" > sample.txt

Output:
- This is a sample text file and in this folder we are going to learn about checkout, revert, reset and restore
(File is modified in locally)

Step 7:
- git checkout -- .\task-3\sample.txt
- to discard the changes made to the file, and point to the last commit so for done

(or)
- git restore .\task-3\sample.txt
- to restore the file to the last commit 

both the checkout and restore command will do the same operation, checkout is a multi-purpose command and restore is a new command introduced to perform the same operation.

Output:
- This is a sample text file and in this folder we are going to learn about checkout, revert, reset
(File is reverted to the last commit)

Step 8:
- add some more text to the sample.txt file.
- echo "This is a sample text file and in this folder we are going to learn about checkout, revert, reset or restore

revert - to revert the changes made to the file, and point to the last commit so for done
reset - to reset the changes made to the file, and point to the last commit so for done" > sample.txt

Output:
- This is a sample text file and in this folder we are going to learn about checkout, revert, reset or restore
revert - to revert the changes made to the file, and point to the last commit so for done
reset - to reset the changes made to the file, and point to the last commit so for done
(File is modified in locally)

Step 9:
- git add . (stage the changes to the index area) 
- git commit -m "Added more text to the sample.txt file" (commit the changes to the local repository)
- git push origin main (push the changes to the remote repository)

Step 10:
- git log --oneline
- to check the commit history of the repository.

Output:
3ea9b24 (HEAD -> main, origin/main) Added a few more text regarding revert and reset
065c4e7 readme text file included - about creation and restoring contents in file
a7446dd Initially a sample text file is created

Step 11:
- now  3ea9b24 commit is the latest commit, and we need to revert the changes made in this commit.
- git revert 3ea9b24
- to revert the changes made in the commit 3ea9b24
- this will reflect in local working directory

Output:
- This is a sample text file and in this folder we are going to learn about checkout, revert, reset
(File is reverted to the last commit)

Step 12:
- git push origin main
- to push the changes to the remote repository. (to make a change in the remote repository)


Step 13:
- add a reset command uses in the sample.txt file.
- echo "This is a sample text file and in this folder we are going to learn about checkout, revert, reset
reset - to reset the changes made to the file, and point to the last commit so for done" > sample.txt

- git add . (stage the changes to the index area)
- git commit -m "added a reset command uses in a sample txt file" (commit the changes to the local repository)



Step 14:
- git log --oneline
- to check the commit history of the repository.

Output:
66aa390 (HEAD -> main) added a reset command uses in a sample txt file
adb2e6a (origin/main) Revert "Added a few more text regarding revert and reset"
3ea9b24 Added a few more text regarding revert and reset
065c4e7 readme text file included - about creation and restoring contents in file
a7446dd Initially a sample text file is created

Step 15:
- now 66aa390 commit is the latest commit, and we need to reset the changes made in this commit.
- git reset adb2e6a
- to reset the changes made in the commit 66aa390

Output:
Unstaged changes after reset:
M       task-3/sample.txt

Step 16:
- git status

Output:
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   task-3/Readme.txt
        modified:   task-3/sample.txt

Step 17:
- git add . and git commit -m "Added a reset content in the sample.txt"
- git log --oneline

Output:
cab4c0d (HEAD -> main) Added a reset content in the sample.txt
adb2e6a (origin/main) Revert "Added a few more text regarding revert and reset"
3ea9b24 Added a few more text regarding revert and reset
065c4e7 readme text file included - about creation and restoring contents in file
a7446dd Initially a sample text file is created

Step 18:
- git reset --soft adb2e6a
- (--soft) will reset the changes made in the commit cab4c0d and keep the changes in the staging area.
- git status

Output:

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   task-3/sample.txt

Step 19:
- git add . and git commit -m "Reset text is added to the sample.txt"
- git log --oneline

Output:
237f9c4 (HEAD -> main) Reset text is added to the sample.txt
adb2e6a (origin/main) Revert "Added a few more text regarding revert and reset"
3ea9b24 Added a few more text regarding revert and reset
065c4e7 readme text file included - about creation and restoring contents in file
a7446dd Initially a sample text file is created

- git reset --hard adb2e6a
- (--hard) will reset the changes made in the commit 237f9c4 and discard the changes in the working directory.

Output:
HEAD is now at adb2e6a Revert "Added a few more text regarding revert and reset"

-- Reset have a three tags (soft, mixed, hard)
-- soft - will reset the changes made in the commit and keep the changes in the staging area.
-- mixed - will reset the changes made in the commit and keep the changes in the working directory.
-- hard - will reset the changes made in the commit and discard the changes in the working directory.

if we use only reset without any tags, it will consider as mixed reset.

-- Revert 
-- Revert is used to revert the changes made in the commit and create a new commit with the changes reverted.
-- Revert will not delete the commit history, it will create a new commit with the changes reverted.    