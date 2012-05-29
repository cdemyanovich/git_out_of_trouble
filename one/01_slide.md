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

