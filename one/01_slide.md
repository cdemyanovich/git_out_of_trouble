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
