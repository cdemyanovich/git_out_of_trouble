!SLIDE commandline
# Finding Help

    $ git help <command>

    $ man git-<command>

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

!SLIDE commandline incremental
# Problem
## You don not know if changes are merged into your current branch

    $ git branch
      546826_react_to_pgs_callback
      faster_specs
    * master
      pgs
      refactor_noaa_decline_reasons

!SLIDE commandline incremental
# Solution
## Which branches contain the most recent commit on this branch?

    $ git branch --contains
      faster_specs
    * master
      refactor_noaa_decline_reasons

!SLIDE commandline incremental
# Solution
## What branches are merged into this branch?

    $ git branch --merged
      546826_react_to_pgs_callback
    * master
      pgs

!SLIDE commandline incremental
# Solution
## What branches are NOT merged into this branch?

    $ git branch --no-merged
      faster_specs
      refactor_noaa_decline_reasons

!SLIDE bullets
# Summary

The options --contains, --merged and --no-merged serve three related but different purposes:

    * --contains <commit> is used to find all branches which will need special attention if <commit> were to be rebased or amended, since those branches contain the specified <commit>.
    * --merged is used to find all branches which can be safely deleted, since those branches are fully contained by HEAD.
    * --no-merged is used to find branches which are candidates for merging into HEAD, since those branches are not fully contained by HEAD.

!SLIDE commandline incremental smaller
# Problem
## You want to ignore a file

    $ git status
      # On branch master
      # Your branch is ahead of 'origin/master' by 6 commits.
      #
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.DS_Store
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental smaller
# Solution

    $ echo .DS_Store >> .gitignore

    $ cat .gitignore
    .DS_Store

    $ git status
      # On branch master
      # Your branch is ahead of 'origin/master' by 6 commits.
      #
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.gitignore
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental smaller
# Problem
## You always want to ignore a file

    $ git status
      # On branch master
      # Your branch is ahead of 'origin/master' by 6 commits.
      #
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.DS_Store
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental smaller
# Solution
## Add the file to a global ignore file

    $ git config --global core.excludesfile ~/.gitignore

    $ cat ~/.gitconfig
    ...
    [core]
            excludesfile = ~/.gitignore

    $ echo .DS_Store >> ~/.gitignore

    $ cat ~/.gitignore
    .DS_Store

    $ git status
      # On branch master
      nothing to commit (working directory clean)
