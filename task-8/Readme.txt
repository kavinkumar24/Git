location of Hooks folder -> ./git/hooks

in this by default we have some sample files, we can use those files to create our own hooks.
Types of Hooks
- Client-side Hooks
    1. pre-commit
    2. prepare-commit-msg
    3. commit-msg
    4. post-commit
    5. pre-rebase
    6. post-checkout
    7. post-merge

- Server-side Hooks
    1. pre-receive
    2. update
    3. post-receive

- In this I used 2 commit hooks
    1. pre-commit
    2. commit-msg

- pre-commit 
    - This hook is called before obtaining the proposed commit message and before the commit is made.
    - It is used to inspect the snapshot that is about to be committed, to see if it passes the pre-commit hook.
    - If the pre-commit hook returns a non-zero status(1), the commit is aborted.
    - This hook is used to check the code before committing the code.
    - In this I used this hook to check the Api key in the file, if it is empty then it will not allow to commit the code, and also checked to avoid the empty files being committed.

- commit-msg
    - This hook is called after obtaining the proposed commit message.
    - It is used to check the commit message before committing the code.
    - If the commit message is not in the proper format then it will not allow to commit the code.
    - In this I used this hook to check the commit message, if it is not in the length of 4 then it will not allow to commit the code.


Steps:

- Step 1: 
    - created a initial_feature txt file  and added some text to it.
    - echo "This is a feature file where it contains an Api key and it will captured by pre-commit hooks" > initial_feature.txt
    - echo "Rapid_API_KEY = \"\"" >> initial_feature.txt
    - file created with empty Rapid_API_KEY

- Step 2:
    - go to git hooks folder
    - cd ./.git/hooks
    - created a pre-commit file
    - by using a bash script
    - shell script
        #! C:/Program\ Files/Git/usr/bin/sh.exe
        echo "Running pre-commit hook..."

        # Create a temporary file to store names of empty files
        empty_files=$(mktemp)

        # Check for empty staged files
        git diff --cached --name-only | while read file; do
            if [ ! -s "$file" ]; then  # If file is empty
                echo "$file" >> "$empty_files"  # Store file name in temporary file
            fi
        done

        # Check if any empty files were found
        if [ -s "$empty_files" ]; then  # If the temporary file is non-empty
            echo "Error: The following file(s) are empty and cannot be committed:"
            cat "$empty_files"  # Print the list of empty files
            rm "$empty_files"  # Clean up the temporary file
            exit 1  # Prevent the commit
        fi

        # Clean up the temporary file if no empty files are found
        rm "$empty_files"

        # Check for secrets in the code (generic API keys, AWS, GitHub, etc.)
        if git grep -E -i \
            '([A-Za-z0-9]+_API_KEY\s*=\s*"?[A-Za-z0-9]{32,40}"?)' \
            > /dev/null 2>&1; then  # /dev/null 2>&1 hides the output
            echo "Found a secret"
            exit 1  # Exit with non-zero status to prevent commit
        else
            echo "No secrets found"
        fi

        # --cached: only staged changes
        # --name-only: only file names
        # -s - it is about some content present in the file (size)
        # -E - It is called extended regular expression, and it is used to match the pattern in the file in a custom way.
        # -i - case insensitive
        # > /dev/null - redirect output to null
        # 2>&1 - redirect stderr to stdout (2- stderr, 1- stdout)

    
    - created a commit-msg file
    - by using a bash script

    #! C:/Program\ Files/Git/usr/bin/sh.exe
    # Get the commit message file path
    COMMIT_MSG_FILE="$1"

    # Check if the commit message is at least 4 characters long (ignores newline)
    commit_message=$(<"$COMMIT_MSG_FILE")

    # Check if the message is at least 4 characters long
    if [ ${#commit_message} -lt 4 ]; then
        echo "Error: Commit message must be at least 4 characters long."
        exit 1
    fi

    # Allow commit if the message is valid
    exit 0

    # lt -less than


- Step 3:
    - git add .
    - git commit -m "Initial feature updated"

Output:
    - Running pre-commit hook...
    - 
    git commit -m "Initial feature updated"
    Running pre-commit hook...
    Error: The following file(s) are empty and cannot be committed:
    task-8/empty_file.txt

------------------------ After deleted the empty file and staged the changes ------------------------

    git commit -m "Initial feature updated"
    Running pre-commit hook...
    Found a secret

- Step 4:
   - deleted the empty file and removed the api key, it pass the pre-commit hook
   - git add .
   - git commit -m "In"
    - it will not allow to commit the code as the commit message is less than 4 characters

Output:

Running pre-commit hook...
No secrets found
Error: Commit message must be at least 4 characters long.