# commands
Various commands to get you out of trouble at random times

## Git

Deletes all local branches that are fully merged in to their remote branch

    git for-each-ref --format '%(refname:short)' refs/heads/ | grep -v \development | xargs git branch -d

- `git` : base git command
    - `for-each-ref` : Iterate over all refs
        - `--format '%(refname:short)'` : formats the output to show only the branchnames
        - `refs/heads/` : that contain 'refs/heads/'
- `grep` : filter the output
    - `-v \development` : that doesn't contain '\development'
- `xargs` : reads output from previous commands and executes the following command
    - `git` : base git command
        - `branch -d` : deletes the supplied branch

## Terminal

Finds all files in the current folder that have a file size larger than 100 Mb

    find . -type f -size +100000k -exec ls -lh {} \; | awk '{ print $9 ": " $5 }'

- `find .` : find in current folder
    - `-type f` : files
    - `-size +100000k` : where the file size is larger than 100Mb
    - `-exec` : executes the command
        - ` ls -lh` : list files with long format and with human readable file sizes
        - `{}` : matching the filename being processed by `find`
        - `\;` : end of the statement to be executed
    - `awk '{ print $9 ": " $5 }'` : uses awk to print the results of the find command as : 'filname: filesize'