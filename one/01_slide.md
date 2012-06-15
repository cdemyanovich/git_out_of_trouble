!SLIDE
# Git Out of Trouble

!SLIDE bullets incremental
## What is Git?

* open source
* distributed
* fast

!SLIDE center
![Git logo](../images/Git-Icon-1788C_small.png) 1.7.10.4

![Lion](../images/InstallAssistant.175x175-75.png) 10.7

![iTerm2](../images/iTerm_icon_small.jpg) command line

!SLIDE center
### git-scm.com/downloads
![Other Tools](../images/other_tools.png "Other Tools")

!SLIDE
# Trouble

!SLIDE center
![Mistakes](../images/mistakesdemotivator.jpg "Mistakes")

!SLIDE
## Who gets into trouble?

!SLIDE center
![Uncle Sam](../images/UncleSam.gif "Uncle Sam")

!SLIDE center
![Me](../images/me_dodgeball_championship.jpg "Me")

!SLIDE center
![GitHub](../images/octocat_fluid.png "GitHub")

!SLIDE center
![Linus Torvalds](../images/linus-torvalds.jpeg "Linus Torvalds")

!SLIDE center
![Everyone](../images/globe_west_540.jpg "Everyone")

!SLIDE
# An Ounce of Prevention

!SLIDE
"...an Ounce of Prevention is worth a Pound of Cure...."

!SLIDE center
![Benjamin Franklin](../images/427px-Benjamin_Franklin_by_Joseph-Siffred_Duplessis.jpg)

!SLIDE commandline
## RTFM

    $ git help <command>

    $ man git-<command>

!SLIDE commandline small

    $ git
    usage: git [--version] [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
               [-p|--paginate|--no-pager] [--no-replace-objects] [--bare]
               [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
               [-c name=value] [--help]
               <command> [<args>]

    The most commonly used git commands are:
       add        Add file contents to the index
       bisect     Find by binary search the change that introduced a bug
       branch     List, create, or delete branches
       checkout   Checkout a branch or paths to the working tree
    ...

    See 'git help <command>' for more information on a specific command.

!SLIDE commandline incremental
## Experiment

    $ git add --dry-run .
    add '.gitignore'
    add '.rvmrc'
    add 'Gemfile'
    ...

    $ git status
      # On branch master
      #
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.gitignore
      #	.rvmrc
      #	Gemfile
      ...

!SLIDE commandline incremental
## But, do wear safety goggles

`-n`, _usually_ short-hand for `--dry-run`

    $ git help commit
    ...
    -n, --no-verify
               This option bypasses the pre-commit and
               commit-msg hooks. See also githooks(5).
    ...
    --dry-run
               Do not create a commit, but show a list of paths
               that are to be committed, paths with local
               changes that will be left uncommitted and paths
               that are untracked.

!SLIDE
# A Pound of Cure

!SLIDE commandline incremental
# Problem
## You added a file by mistake

    $ git add showoff.json

    $ git status
      # On branch master
      # Changes to be committed:
      #   (use "git reset HEAD <file>..." to unstage)
      #
      #        new file:     showoff.json

!SLIDE commandline incremental
# Solution
## RTFC

    $ git status
      # On branch master
      # Changes to be committed:
      #   (use "git reset HEAD <file>..." to unstage)
      #
      #        new file:     showoff.json

!SLIDE commandline incremental

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

    $ ls references/02_slide.md
    ls: references/02_slide.md: No such file or directory

    $ git status
     # On branch master
     # Changes to be committed:
     #   (use "git reset HEAD <file>..." to unstage)
     #
     #	deleted:    references/02_slide.md
     #

!SLIDE commandline incremental
# Solution
## RTFC

    $ git status
     # On branch master
     # Changes to be committed:
     #   (use "git reset HEAD <file>..." to unstage)
     #
     #	deleted:    references/02_slide.md
     #

!SLIDE commandline incremental small

    $ git reset HEAD references/02_slide.md
    Unstaged changes after reset:
    D	references/02_slide.md

    $ git status
     # On branch master
     # Changes not staged for commit:
     #   (use "git add/rm <file>..." to update what will be committed)
     #   (use "git checkout -- <file>..." to discard changes in working directory)
     #
     #	deleted:    references/02_slide.md
     #
     no changes added to commit (use "git add" and/or "git commit -a")

!SLIDE commandline incremental

    $ git checkout -- references/02_slide.md

    $ git status
     # On branch master
     nothing to commit (working directory clean)

    $ ls references/02_slide.md
    references/02_slide.md

!SLIDE commandline incremental smaller
# Problem
## Some file is cluttering up your status

    $ git status
      # On branch master
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.DS_Store
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental small
## Ignore it!

    $ echo .DS_Store >> .gitignore

    $ cat .gitignore
    .DS_Store

    $ git status
      # On branch master
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.gitignore
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental smaller
# Problem
## You want to ignore a file without updating all repositories

    $ git status
      # On branch master
      # Untracked files:
      #   (use "git add <file>..." to include in what will be committed)
      #
      #	.DS_Store
      nothing added to commit but untracked files present (use "git add" to track)

!SLIDE commandline incremental small
## Use a global ignore file

    $ git config --global core.excludesfile ~/.gitignore

    $ cat ~/.gitconfig
    ...
    [core]
            excludesfile = ~/.gitignore

    $ echo .DS_Store >> ~/.gitignore

    $ cat ~/.gitignore
    .DS_Store

    $ cat .gitignore

    $ git status
      # On branch master
      nothing to commit (working directory clean)

!SLIDE commandline

For more on ignore patterns and precendence of ignore files

    $ git help gitignore

    $ man gitignore

!SLIDE
## But `.DS_Store` is still everywhere!

!SLIDE commandline
## You could...

    $ find . -type f -name ".DS_Store" -print | xargs rm -rf

    $ find . -type d -name ".svn" -print | xargs rm -rf

!SLIDE center
![Mr. Clean](../images/Mr_Clean_small.jpg "Mr. Clean")

!SLIDE commandline

    $ git clean

    $ git clean -d

!SLIDE commandline incremental
# Problem
## You wrote a bad commit message for the last commit

    $ git commit -m "Whatever"
    [master 1eaaace] Whatever
     1 file changed, 11 insertions(+)

!SLIDE commandline incremental
# Solution
## Amend it

    $ git commit --amend

!SLIDE code smaller

    Whatever

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
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
    #
    # Changes to be committed:
    #   (use "git reset HEAD^1 <file>..." to unstage)
    #
    #	modified:   one/01_slide.md
    #

!SLIDE commandline
## Much better

    $ git commit --amend
    ...
    [master a4f0c81] Describe amending commit to fix bad message
     1 file changed, 11 insertions(+)

!SLIDE commandline incremental
## Not just for commit messages

    $ git status
      # On branch master
      # Your branch is ahead of 'origin/master' by 4 commits.
      #
      # Changes not staged for commit:
      #   (use "git add <file>..." to update what will be committed)
      #   (use "git checkout -- <file>..." to discard changes in working directory)
      #
      #	modified:   one/01_slide.md

    $ git commit --amend

!SLIDE code smaller
    Describe amending commit to fix bad message

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    #
    # Changes to be committed:
    #   (use "git reset HEAD^1 <file>..." to unstage)
    #
    #	modified:   one/01_slide.md
    #

!SLIDE commandline
## All changes in one commit

    $ git commit --amend
    ...
    [master 57f0ba9] Describe amending commit to fix bad message
     1 file changed, 4 insertions(+)

!SLIDE center
![Caution](../images/500px-Stop_hand_caution.svg.png)

!SLIDE commandline

    $ git commit -m "Whatever"
    [master 1eaaace] Whatever
     1 file changed, 11 insertions(+)

    $ git commit --amend
    [master a4f0c81] Describe amending commit to fix bad message
     1 file changed, 11 insertions(+)

    $ git commit --amend
    [master 57f0ba9] Describe amending commit to fix bad message
     1 file changed, 4 insertions(+)

!SLIDE
## When using `--amend`, think locally

!SLIDE commandline incremental
# Problem
## You want to clean up your local branches

    $ git branch
      546826_react_to_pgs_callback
      faster_specs
    * master
      pgs
      refactor_noaa_decline_reasons

!SLIDE commandline incremental
## Which branches can I delete?

    $ git branch
      546826_react_to_pgs_callback
      faster_specs
    * master
      pgs
      refactor_noaa_decline_reasons

    $ git branch --merged
      546826_react_to_pgs_callback
    * master
      pgs

!SLIDE commandline incremental
## Which branches should I keep?

    $ git branch
      546826_react_to_pgs_callback
      faster_specs
    * master
      pgs
      refactor_noaa_decline_reasons

    $ git branch --no-merged
      faster_specs
      refactor_noaa_decline_reasons

!SLIDE commandline incremental
## Bonus: Which branches contain `<commit>`?

    $ git branch
      546826_react_to_pgs_callback
      faster_specs
    * master
      pgs
      refactor_noaa_decline_reasons

    $ git branch --contains
      faster_specs
    * master
      refactor_noaa_decline_reasons

!SLIDE bullets incremental
## Use `git branch`

* `--merged` to find all branches which can be safely deleted
* `--no-merged` to find branches which are candidates for merging into `HEAD`
* `--contains <commit>` find all branches which will need special attention if `<commit>` were to be rebased or amended

!SLIDE
## You want to know what changed in a commit

!SLIDE commandline incremental small

    $ git log -p

    commit 8fdd6b1a31ae4eb07ddafa7027c3e54cc4fdc9cc
    Author: Craig Demyanovich <cdemyanovich@gmail.com>
    Date:   Thu Jun 14 21:21:57 2012 -0500

        Bigger text on using an ignore file

    diff --git a/one/01_slide.md b/one/01_slide.md
    index a4a3fa7..b2cff87 100644
    --- a/one/01_slide.md
    +++ b/one/01_slide.md
    @@ -235,7 +235,7 @@ command line
           #        .DS_Store
           nothing added to commit but untracked files present (use "git add" to track)

    -!SLIDE commandline incremental smaller
    +!SLIDE commandline incremental small
     ## Use a global ignore file

         $ git config --global core.excludesfile ~/.gitignore

    commit 175c8c3bce2f2901f42ddc8c332b3d101ee2069a
    Author: Craig Demyanovich <cdemyanovich@gmail.com>
    Date:   Thu Jun 14 21:18:10 2012 -0500

        Better warning about changing SHAs
    ...

!SLIDE commandline incremental small

    $ git show 175c8c3
    commit 175c8c3bce2f2901f42ddc8c332b3d101ee2069a
    Author: Craig Demyanovich <cdemyanovich@gmail.com>
    Date:   Thu Jun 14 21:18:10 2012 -0500

        Better warning about changing SHAs

    diff --git a/one/01_slide.md b/one/01_slide.md
    index 3a90275..a4a3fa7 100644
    --- a/one/01_slide.md
    +++ b/one/01_slide.md
    @@ -325,8 +325,10 @@ command line
         [master a4f0c81] Describe amending commit to fix bad message
          1 file changed, 11 insertions(+)

    +!SLIDE center
    +![Caution](../images/500px-Stop_hand_caution.svg.png)
    +
     !SLIDE commandline
    -## WARNING: the SHA changed

         $ git commit -m "Whatever"
         [master 1eaaace] Whatever

!SLIDE
## You pushed a bad commit

!SLIDE commandline incremental

    $ git commit -am "Killed Mr. Clean"
    [master ece75be] Killed Mr. Clean
     1 file changed, 9 deletions(-)

!SLIDE commandline incremental

    $ git revert ece75be

!SLIDE smaller

    Revert "Killed Mr. Clean"

    This reverts commit ece75be6fa91e135cfc349341aa523d323d92e5b.

    # Please enter the commit message for your changes. Lines starting
    # with '#' will be ignored, and an empty message aborts the commit.
    # On branch master
    # Your branch is ahead of 'origin/master' by 2 commits.
    #
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   one/01_slide.md
    #
    # Untracked files:
    #   (use "git add <file>..." to include in what will be committed)
    #
    #	images/

!SLIDE commandline

    $ git revert ece75be
    ...
    [master 9791a68] Revert "Killed Mr. Clean"
     1 file changed, 9 insertions(+)

!SLIDE commandline incremental small

    $ git log
    commit 9791a68ebe0f454766e0d0a43c1d1e59ea943d01
    Author: Craig Demyanovich <cdemyanovich@gmail.com>
    Date:   Thu Jun 14 23:37:19 2012 -0500

        Revert "Killed Mr. Clean"

        This reverts commit ece75be6fa91e135cfc349341aa523d323d92e5b.

    commit ece75be6fa91e135cfc349341aa523d323d92e5b
    Author: Craig Demyanovich <cdemyanovich@gmail.com>
    Date:   Thu Jun 14 23:36:59 2012 -0500

        Killed Mr. Clean
    ...

!SLIDE commandline

    $ git revert -n ece75be
    $ git revert -n c9099b3
    ...
    $ git revert -n 8fdd6b1

    $ git commit -am "Reverted a few bad commits"

