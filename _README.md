# LearnGit

Git is an application that **manages source code**. It has **distributed behavior** that allows many developers to change the same code. It is **open source software** under [GNU GPL v2](https://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html) and is provided as is without fees. 

Below are the basic concepts of Git and its most useful commands. 

## Basic Concepts

### Repository (Repo)
A repository is a space where the **project's files and folders** are kept. It can be **local** (on your computer) or **remote** (on a server). What distinguishes a repo from a typical folder is a **.git** subfolder that includes the history of changes and the configuration influencing the behavior of changes. 

### Branch
A branch is a **parallel version** of the repository. It allows **simultaneous work** on different features or fixes without affecting the main codebase. The **default branch** in a new repository is usually called master or main.

### Working Directory
The working directory is where **files and folders are changed**. Changes in the working directory are not tracked by Git until **they are staged**. 

### Stash
The stash is a **local store for recent changes** to the working directory. The stash is **separate from the index** and commits to the current branch. After storing a snapshot of your local files, the state of the **working directory is returned to the previous commit**. You can save multiple stashes on your local computer and you can apply back any of the stashes at a later stage.

### Staging Area (Index)
The staging area (or index) is where you prepare **changes to be committed**. It allows you to review and organize **changes before making a commit**.

### Commit
A commit represents a **snapshot of your repository** at a specific point in time. Each commit has a **unique SHA-1 hash identifier** and includes a **message describing the changes**.

### Merge
Merging is the process of combining **changes from one branch into another**. It helps integrate the work done in different branches.

## Useful Commands

### How to create a new, local repo from an existing, remote repo

1. Set up the Clone Demo. 
    - Update the current directory with `cd /workspaces`. Verify the current directory is updated with `pwd`. 
    - Delete the *LearnGit* subdirectory with `rm LearnGit --recursive --force`. Verify the subdirectory is deleted with `ls LearnGit --all`. 
2. Create the local repo. 
    - Clone the remote repo with `git clone https://github.com/johnsheffinet/LearnGit`. 
    - Update the current directory with `cd LearnGit`. Verify the current directory is updated with `pwd`. 
    - Verify the local repo is created with `git status`.  

    ```
    $ cd /workspaces
    $ pwd
    /workspaces
    $ rm LearnGit --recursive --force
    $ ls LearnGit --all
    ls: cannot access 'LearnGit': No such file or directory
    $ git clone https://github.com/johnsheffinet/LearnGit
    Cloning into 'LearnGit'...
    remote: Enumerating objects: 22, done.
    remote: Counting objects: 100% (22/22), done.
    remote: Compressing objects: 100% (14/14), done.
    remote: Total 22 (delta 4), reused 13 (delta 2), pack-reused 0 (from 0)
    Receiving objects: 100% (22/22), 5.15 KiB | 5.15 MiB/s, done.
    Resolving deltas: 100% (4/4), done.
    $ cd LearnGit
    $ git status
    On branch main
    Your branch is up to date with 'origin/main'.

    nothing to commit, working tree clean
    $ 
    ```

### How to create a new, remote repo from an existing, local directory 

1. Set up the Init Demo. 
    - Update the current directory with `cd /workspaces/LearnGit`. Verify the current directory is updated with `pwd`. 
    - Delete the *.git* subdirectory with `rm .git --recursive --force`. The existing files and folders in the *LearnGit* directory, i.e. *LICENSE* and *README.md* files, are retained. Only the repo's metadata is removed. Verify the subdirectory is deleted with `git status`. 
2. Create the remote repo. 
    - Initialize the local repo with `git init`. 
    - Stage all changes with `git add .`. Verify all changes are staged with `git status`. 
    - Commit all changes with `git commit --message="Initial commit"`. 
    - Push the local repo to the remote repo with `git push https://github.com/johnsheffinet/LearnGit --mirror`. The *--mirror* option creates a new, remote repo. 

    ```
    $ cd /workspaces/LearnGit
    $ pwd
    /workspaces/LearnGit
    $ rm .git --recursive --force
    $ git status
    fatal: not a git repository (or any parent up to mount point /)
    Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
    $ git init
    Initialized empty Git repository in /workspaces/LearnGit/.git/
    $ git add .
    $ git status
    On branch main

    No commits yet

    Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
            new file:   LICENSE
            new file:   README.md

    $ git commit --message="Initial commit"
    [main (root-commit) 4b6728b] Initial commit
    2 files changed, 22 insertions(+)
    create mode 100644 LICENSE
    create mode 100644 README.md
    $ git push https://github.com/johnsheffinet/LearnGit --mirror
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 912 bytes | 912.00 KiB/s, done.
    Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
    To https://github.com/johnsheffinet/LearnGit
    + d59dbb6...4b6728b main -> main (forced update)
    $ 
    ```


### How to undo changes to a working tree, stash, staging area, commit, merge and push. 

1. Set up the Undo Demo. 
    - Update the current directory with `cd /workspaces/LearnGit`. Verify the current directory is updated with `pwd`. 
    - Delete the *.git* subdirectory with `rm .git -rf`. Verify the *.git* subdirectory is deleted with `git status`. 
    - Create the local repo with `git init`. 
    - Stage all changes with `git add .`. Verify all changes are staged with `git status`. 
    - Update the local repo with `git commit -m "Initial commit"`. 
    - Add an alias for the remote repo with `git remote add origin https://github.com/johnsheffinet/LearnGit`. Verify an alias is added for the remote repo with `git remote`. 
    - Update the remote repo with `git push origin --mirror`. 
    - Create a branch from the *main* branch and update the current branch with `git checkout -b UndoDemo main`. 
2. Do and undo the working tree. 
    - Update the file with `echo "Undo Demo" > README.md`. Verify the file is updated with `git status`. 
    - Undo the update with `git restore README.md`. Verify the update is undone with `git status`. 
3. Do and undo the stash. 
    - Redo the update with `echo "Undo Demo" > README.md`. Verify the update is redone with `git status`. 
    - Stash the update with `git stash`. A stash undoes the update to the working tree as well as stores the update in the stash. 
4. Do and undo the staging area. 
    - Redo the stash with `git stash pop`. 
    - Stage the stash with `git add README.md`. Verify the stash is staged with `git status`. 
    - Undo the stage with `git restore --staged README.md`. Verify the stage is undone with `git status`. 
5. Do and undo the commit. 
    - Redo the stage with `git add README.md`. Verify the stage is redone with `git status`. 
    - Commit the stage with `git commit -m "Undo Demo - Do commit"`. 
    - Undo the commit with `git reset HEAD~1`. A reset sets HEAD to the specified commit. The history subsequent to the specified commit is lost. Verify the commit is undone with `git log --oneline`. 
6. Do and undo the merge. 
    - Redo the commit with `git commit -am "Undo Demo - Redo commit"`. 
    - Switch the branch with `git checkout main`. 
    - Merge the branch with `git merge UndoDemo --no-ff -m "Undo Demo - Do merge"`. The *--no-ff* option forces a commit in a fast forward merge. 
    - Undo the merge with `git revert HEAD -m 1`. A revert does a new commit that undoes the specified commit. The history subsequent to the specified commit is kept. The *-m 1* option is required because the merge is reverted. Verify the merge is undone with `git log --oneline`. 
7. Redo and push the merge. 
    - Redo the merge with `git revert HEAD`. A revert of a previous revert is the same as redoing the reverted change. Verify the merge is redone with `git log --oneline`. 
    - Push the redone merge to the remote repo with `git push origin main`. 
8. Tear down the demo. 
    - Delete the branch with `git branch -d UndoDemo`. 
    - Remove the alias for the remote repo with `git remote remove origin`. Verify the alias for the remote repo is removed with `git remote`. 

    ```
    $ cd /workspaces/LearnGit
    $ pwd
    /workspaces/LearnGit
    $ rm .git -rf
    $ git status
    fatal: not a git repository (or any parent up to mount point /)
    Stopping at filesystem boundary (GIT_DISCOVERY_ACROSS_FILESYSTEM not set).
    $ git init
    Initialized empty Git repository in /workspaces/LearnGit/.git/
    $ git add .
    $ git status
    On branch main

    No commits yet

    Changes to be committed:
    (use "git rm --cached <file>..." to unstage)
            new file:   LICENSE
            new file:   README.md

    $ git commit -m "Initial commit"
    [main (root-commit) 46c27a3] Initial commit
    2 files changed, 22 insertions(+)
    create mode 100644 LICENSE
    create mode 100644 README.md
    $ git remote add origin https://github.com/johnsheffinet/LearnGit
    $ git remote
    origin
    $ git push origin --mirror
    Enumerating objects: 4, done.
    Counting objects: 100% (4/4), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (4/4), 912 bytes | 912.00 KiB/s, done.
    Total 4 (delta 0), reused 0 (delta 0), pack-reused 0 (from 0)
    To https://github.com/johnsheffinet/LearnGit
    + 7834a8c...46c27a3 main -> main (forced update)
    $ git checkout -b UndoDemo main
    Switched to a new branch 'UndoDemo'
    $ echo "Undo Demo" > README.md
    $ git status
    On branch UndoDemo
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    $ git restore README.md
    $ git status
    On branch UndoDemo
    nothing to commit, working tree clean
    $ echo "Undo Demo" > README.md
    $ git status
    On branch UndoDemo
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    $ git stash
    Saved working directory and index state WIP on UndoDemo: 46c27a3 Initial commit
    $ git stash pop
    On branch UndoDemo
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    Dropped refs/stash@{0} (e054a05d4439b8c63b59dffd927d8eedc9ee747a)
    $ git add README.md
    $ git status
    On branch UndoDemo
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
            modified:   README.md

    $ git restore --staged README.md
    $ git status
    On branch UndoDemo
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
            modified:   README.md

    no changes added to commit (use "git add" and/or "git commit -a")
    $ git add README.md
    $ git status
    On branch UndoDemo
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
            modified:   README.md

    $ git commit -m "Undo Demo - Do commit"
    [UndoDemo 06679a8] Undo Demo - Do commit
    1 file changed, 1 insertion(+), 1 deletion(-)
    $ git reset HEAD~1
    Unstaged changes after reset:
    M       README.md
    $ git log --oneline
    46c27a3 (HEAD -> UndoDemo, origin/main, main) Initial commit
    $ git commit -am "Undo Demo - Redo commit"
    [UndoDemo 1cf5438] Undo Demo - Redo commit
    1 file changed, 1 insertion(+), 1 deletion(-)
    $ git checkout main
    Switched to branch 'main'
    $ git merge UndoDemo --no-ff -m "Undo Demo - Do merge"
    Merge made by the 'ort' strategy.
    README.md | 2 +-
    1 file changed, 1 insertion(+), 1 deletion(-)
    $ git revert HEAD -m 1
    [main 04c79d4] Revert "Undo Demo - Do merge"
    1 file changed, 1 insertion(+), 1 deletion(-)
    $ git log --oneline
    04c79d4 (HEAD -> main) Revert "Undo Demo - Do merge"
    af7d4f6 Undo Demo - Do merge
    1cf5438 (UndoDemo) Undo Demo - Redo commit
    46c27a3 (origin/main) Initial commit
    $ git revert HEAD
    [main 629be9b] Reapply "Undo Demo - Do merge"
    1 file changed, 1 insertion(+), 1 deletion(-)
    $ git log --oneline
    629be9b (HEAD -> main) Reapply "Undo Demo - Do merge"
    04c79d4 Revert "Undo Demo - Do merge"
    af7d4f6 Undo Demo - Do merge
    1cf5438 (UndoDemo) Undo Demo - Redo commit
    46c27a3 (origin/main) Initial commit
    $ git push origin main
    Enumerating objects: 8, done.
    Counting objects: 100% (8/8), done.
    Delta compression using up to 2 threads
    Compressing objects: 100% (5/5), done.
    Writing objects: 100% (6/6), 832 bytes | 832.00 KiB/s, done.
    Total 6 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
    remote: Resolving deltas: 100% (1/1), done.
    To https://github.com/johnsheffinet/LearnGit
    46c27a3..629be9b  main -> main
    $ git branch -d UndoDemo
    Deleted branch UndoDemo (was 1cf5438).
    $ git remote remove origin
    $ git remote
    $ 
    ```