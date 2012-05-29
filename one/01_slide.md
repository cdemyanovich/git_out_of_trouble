!SLIDE commandline incremental
# Problem
## You staged a file by mistake

    $ git add showoff.json
    $ git status
      # On branch master
      # Changes to be committed:
      #   (use "git reset HEAD <file>..." to unstage)
      #
      #        new file:     showoff.json

!SLIDE commandline incremental
# Solution
## Follow the given advice

    $ git reset HEAD showoff.json
    $ git status
      # On branch master
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #        showoff.json

!SLIDE commandline incremental
# Problem
## You removed a file by mistake

    $ git rm references/02_slide.md
    rm 'references/02_slide.md'
    $ git status
     # On branch master
     # Your branch is ahead of 'origin/master' by 2 commits.
     #
     # Changes to be committed:
     #   (use "git reset HEAD <file>..." to unstage)
     #
     #	deleted:    references/02_slide.md
     #

!SLIDE commandline incremental
# Solution
## Follow the given advice

    $ git reset HEAD references/02_slide.md
    Unstaged changes after reset:
    D	references/02_slide.md
    $ git status
     # On branch master
     # Your branch is ahead of 'origin/master' by 2 commits.
     #
     # Changes not staged for commit:
     #   (use "git add/rm <file>..." to update what will be committed)
     #   (use "git checkout -- <file>..." to discard changes in working directory)
     #
     #	deleted:    references/02_slide.md
     #
     no changes added to commit (use "git add" and/or "git commit -a")

!SLIDE commandline incremental
# Solution (continued)
## Again, follow the given advice

    $ git checkout -- references/02_slide.md
    $ git status
     # On branch master
     # Your branch is ahead of 'origin/master' by 2 commits.
     #
     nothing to commit (working directory clean)

!SLIDE commandline incremental
# Problem
## You began work on master, but work is more involved than you thought

!SLIDE commandline incremental
# Solution
## Branch from master; continue working

    $ git checkout -b <new-branch-name>
    $ git commit -m "Add ability to sign in/out"
    $ git checkout master
    $ git merge <new-branch-name>
    $ git push

!SLIDE commandline incremental
# Solution
## Complete work on master; pull upstream changes with a rebase

    $ git add -A
    $ git commit -m "Add ability to sign in/out"
    $ git pull --rebase
    $ git push

!SLIDE commandline incremental
# Problem
## You wrote a bad commit message for the last commit

    $ git commit -m "Whatever"
    [master 1eaaace] Whatever
     1 file changed, 11 insertions(+)

!SLIDE commandline incremental
# Solution
## Amend the last commit

    $ git commit --amend

!SLIDE code smaller

    Whatever

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    # Your branch is ahead of 'origin/master' by 4 commits.
    #
    # Changes to be committed:
    #   (use "git reset HEAD^1 <file>..." to unstage)
    #
    #	modified:   one/01_slide.md
    #

!SLIDE code smaller

    Describe amending commit to fix bad message

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    # Your branch is ahead of 'origin/master' by 4 commits.
    #
    # Changes to be committed:
    #   (use "git reset HEAD^1 <file>..." to unstage)
    #
    #	modified:   one/01_slide.md
    #

!SLIDE commandline
## Your bad log message is fixed

    $ git commit --amend
    [master a4f0c81] Describe amending commit to fix bad message
     1 file changed, 11 insertions(+)

!SLIDE commandline
## WARNING: the SHA changed

    $ git commit -m "Whatever"
    [master 1eaaace] Whatever
     1 file changed, 11 insertions(+)

    $ git commit --amend
    [master a4f0c81] Describe amending commit to fix bad message
     1 file changed, 11 insertions(+)

!SLIDE commandline incremental
# Problem
## You wrote a bad commit message a few commits ago

    $ git commit -m "Whatever"
    [master 1eaaace] Whatever
     1 file changed, 11 insertions(+)


!SLIDE commandline incremental
# Solution
## Interactively rebase, stopping to correct bad message

    $ git rebase -i <sha>

