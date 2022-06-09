# Alice gets a tree of files and stores it in git


Alice wants to send a tree of files to Carol, via Bob. She wants to
use Bob as the hub for the sharing of files.

Pretend you are Alice. First get some files from github.

`wget https://github.com/oreillymedia/katacoda-examples/archive/refs/heads/main.zip`{{execute}}


Now unzip to get the files.

`unzip main`{{{execute}}}

You will use git to package, store and transport these files. So create a bare git repository.

`git init --bare alice.git`{{execute}}

A bare git repository has no working directory. It only has the git
directory, which git uses to store objects, commits, references and
other objects. Take a look.

`ls alice.git`{{{execute}}}


We now execute a special git command.

```git --git-dir=apple \
    --work-tree=../texlive2022/texdir \
    add \
    texmf-dist/fonts/source/public/knuth-lib/
```{{{execute}}}