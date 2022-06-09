# Alice gets a tree of files and stores it in git


Alice wants to send a tree of files to Carol, via Bob. She wants to
use Bob as the hub for the sharing of files. Pretend you are Alice.


First, Alice, get some files from github.

`wget https://github.com/oreillymedia/katacoda-examples/archive/refs/heads/main.zip`{{execute}}


Now unzip.

`unzip main`{{execute}}

You will use git. So create a bare git repository.

`git init --bare alice.git`{{execute}}

Why bare?  A bare git repository has only the git directory. That's
enough to store files, trees, commits, references and other
objects. Take a look at it

`ls alice.git`{{execute}}


Now save the tree to git. First we do a `git add`. We explicitly state
the git repository to use, and also the working directory.

```git --git-dir=alice.git \
    --work-tree=./katacoda-examples-main \
    add \
    new-scenario-template
```{{execute}}


We're not allowed to do a `git commit`. Instead, first ask git to
store the treee.

`git --git-dir=alice.git write-tree`{{execute}}


Repeat the command, to store the hash value.
`HASH=$(git --git-dir=alice.git write-tree)`{{execute}}

Here's that hash value again.
`echo $HASH`{{execute}}

Now use `git tag` instead of `git commit`. This creates a reference to the tree.

`git --git-dir=alice.git tag alice-tree $HASH`{{execute}}

We now have a tag.

`git --git-dir=alice.git tag`{{execute}}

Use the tag to access a file in the tree.
`git --git-dir=alice.git cat-file -p alice-tree:new-scenario-template/finish.md`{{execute}}