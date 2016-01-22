Basics
=========

We need to learn about few basic Git commands and terminology.

* `Repository`_ - This is where all the changes will be stored.
* `Stage`_ - This is like listed changes to commit to git repository.
* `Commit`_ - To store all changes to repository along with user info.
* `Branch`_ - To have isolated changes for experimental or bug fixes or future releases etc.
* `Log`_ - To see previous commit history.
* `Diff`_ - To see difference between two commits of a file.
* `Reset`_ - To revert file content to a commit in the past.
* `Stash`_ - To delete the changes in the working directory and to get back to your original working state.

.. _Repository:

First we go to a folder and initialize git repository in to track changes.

.. code-block:: python

    $ git init

We need to configure user details if we need a separate user for this particular repository. If not, just leave it.

.. code-block:: python

    $ git config user.name "Your name"
    $ git config user.email your@email.com

.. _Stage:

**Stage and Commit**

After creating few files and making changes, we want to save those to git repository
First we need to add files to stage then commit those in the stage. This can be done in two steps.

* To add files within current directory and directories in it.

  .. code-block:: python

      $ git add .

* To add files and remove deleted files from repository

  .. code-block:: python

      $ git add --all

* To add a specific file

  .. code-block:: python

      $ git add <file relative path>

.. _Commit:

Now its time to commit those changes

.. code-block:: python

    $ git commit
          or
    $ git commit -m “your commit message”

.. _Branch:

**Branch**

Branching is amazing in SCM and we can create a branch from a branch latest commit or a previous commit in history.

* To create a branch from current branch latest commit

  .. code-block:: python

      $ git branch new_branch_name

* To create a branch from current branch previous commit

  .. code-block:: python

      $ git branch new_branch_name <commit SHA-Hash>

* To switch between branches

  .. code-block:: python

      $ git checkout branch_name

* To list all branches and see the current branch

  .. code-block:: python

      $ git branch

* To create a branch and switch to it

  .. code-block:: python

      $ git checkout -b new_branch_name

* To create a new branch from previous commit and switch into it

  .. code-block:: python

      $ git checkout -b new_branch_name <commit SHA Hash>

* To delete a branch

  .. code-block:: python

      $ git branch -D branch_name

.. _Log:

**Log**

We can see the previous commits and that is possible with log command.

To see previous commits

.. code-block:: python

    $ git log

.. _Diff:

**Diff**

Sometimes we want to see changes done between commits or previous commit to stage.

* To see changed files between two commits

  .. code-block:: python

      $ git diff --name-only SHA1 SHA2

* To see changes in a file between two commits

  .. code-block:: python

      $ git diff $start_commit..$end_commit -- path/to/file

* To see changes in stage files

  .. code-block:: python

      $ git diff --cached

.. _Reset:

**Reset**

Git is very mature and flexible that we can do almost anything related to SCM. Lets see how we can revert unwanted commits permanently.

To revert all commits until a commit in history

.. code-block:: python

    $ git reset --hard <commit SHA Hash>

.. _Stash:

**Stash**

Often you may need to roll back to some other commit or switch to other branches, but you may have some unfinished work which you don't want to commit it, in such cases stash may be useful.

  - Saves your working directory and index to a safe place and
  - Restores your working directory and index to the most recent commit.

* Using stash for stashing your work

  .. code-block:: python

      $ git stash

* Retrieving your stashed work back

  .. code-block:: python

      $ git stash list

* Console demo output:

  .. code-block:: python

      $ stash@{0}: WIP on master: 049d078 added the index file
      $ stash@{1}: WIP on master: c264051 Revert "added file_size"
      $ stash@{2}: WIP on master: 21d80a5 added number to log

* To apply the stash back either in a new branch or same working branch:

  .. code-block:: python

      $ git stash apply stash@{2}

  This way you don't need to commit your incomplete work to complete it on a later point.

* Unapplying a stash

  .. code-block:: python

      $ git stash show -p <stash-name> | git apply -R

* Pop a stash:

  The above command only applies a stash but doesn't remove it from stash list.In cases like that if you want to remove a stash from stash list and apply it to current working tree then use

  .. code-block:: python

      $ git stash pop <stash-name>

If you want to remove an object from stash list without applying to working directory

.. code-block:: python

    $ git stash drop <stash-name>

