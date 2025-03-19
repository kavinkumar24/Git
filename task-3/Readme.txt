
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



