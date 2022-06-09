# Alice gets a tree of files and stores it in git


Alice wants to send a tree of files to Carol, via Bob. She wants to
use Bob as the hub for the sharing of files.

Pretend you are Alice. First get some files from github.

`wget https://github.com/oreillymedia/katacoda-examples/archive/refs/heads/main.zip`{{execute}}


Now unzip to get the files.

`unzip main`{{execute}}

You will use git to package, store and transport these files. So create a bare git repository.

`git init --bare alice.git`{{execute}}

A bare git repository has no working directory. It only has the git
directory, which git uses to store objects, commits, references and
other objects. Take a look.

`ls alice.git`{{execute}}


Now save the tree to git. First we do a `git add`. We explicitly state
the git repository to use, and also the working directory.

```git --git-dir=alice.git \
    --work-tree=./katacoda-examples-main \
    add \
    new-scenario-template
```{{execute}}


We're not going to do a `git commit`. Instead, first ask git to store
the treee.

`git --git-dir=alice.git write-tree`{{execute}}


Let's do the command again, but store the hash value.
`HASH=$(git --git-dir=alice.git write-tree)`{{execute}}

Here's that hash value again.
`echo $HASH`{{execute}}

Now use `git tag` instead of `git commit`. This creates a reference to the tree.

`git --git-dir=alice.git tag alice-tree $HASH`{{execute}}