# Deep dive into git

This is the demo repo for a hands-on lab for working with git from the command line.

## Before you start

### Check yor git installation

Make sure git is installed and the version is > 2.23:

```console
$ git --version
> git version 2.35.1
```

If not, [download](https://git-scm.com/downloads) and install git.

### Check your git config

1. Check your name and email address:

```console
$ git config --global user.name
$ git config --global user.email
```

If this does not return the desired values, set the config using these commands:

```console
$ git config --global user.name '<your_name>'
$ git config --global user.email '<your_email_address>'
```

2. Set the default branch to `main`:

```console
$ git config --global init.defaultBranch main
```

3. Check your default editor

Check your default editor (i.e. by running `git config --global --edit`). If you like the editor, then you are good. If your stuck in vim (click <kbd>ESC</kbd> <kbd>:</kbd> <kbd>q</kbd> <kbd>!</kbd> <kbd>Enter</kbd> to exit), then configure the editor of your choice - for example CSCode:

```console
$ git config core.editor 'code --wait'
```

## Practice 1: Understanding git

### Set-up:
Create a local file/folder:

```console
$ mkdir UnderstandingGit
$ cd UnderstandingGit
$ mkdir folder;
$ for d in {1..6}; do echo  "Line ${d}" >> folder/file.txt; done;
```

<details>
  <summary>Important commands for this exercise:</summary>

```
$ git hash-object folder/file.txt
$ git init
$ git add
$ git commit
$ git ls-tree
$ git cat-file [-p | -t]
$ cat
```
</details>
  
A commit is a tree of blobs and trees:

```mermaid
graph BT;
    Tree==>Commit;
    Blob==>Tree;
    Blob2==>Tree;
    Tree2==>Tree;
    Blob3==>Tree2;
    Blob4==>Tree2;
    Tree3==>Tree2;
    Blob5==>Tree3;
```
  
The commits are connected to their parent commits (DAG):
  
```mermaid
graph RL;
    96a85==>49c01;
    7e536==>96a85;
    1e542==>7e536;
    b7e6b==>1e542;
    main-.->b7e6b;
    HEAD-->main;
    5a053==>7e536;
    55805==>5a053;
    branch-.->55805;
    tag-.->55805;
```

Working with patches:

```console
$ git diff
$ git format-patch HEAD~2..HEAD
$ git reset --hard HEAD~2
$ git apply
$ git am
```

## Practice 2: Working with your history

### Set-up:

Create a local history:

```console
$ mkdir WorkingWithYourHistory
$ cd WorkingWithYourHistory
$ git init
$ for d in {1..6}; do touch "file${d}.md"; git add "file${d}.md"; git commit -m "adding file ${d}"; done
```

```mermaid
gitGraph:
options
{
    "nodeSpacing": 150,
    "nodeRadius": 10
}
end
commit
branch newbranch
checkout newbranch
commit
commit
checkout master
commit
commit
merge newbranch
```

<details>
  <summary>Important commands for this exercise:</summary>
  
  ```console
  $ git commit --amend
  $ git reset [--hard | --soft | --mixed]
  $ git reflog
  $ git cherry-pick
  $ git merge [--squash | --rebase]
  $ git rebase [-i]
  ```
  
</details>

## Practice 3: Finding bugs and adding patches

### Set-up:

```console
$ git clone https://github.com/wulfland/DeepDive.git DeepDive
$ cd DeepDive
```

<details>
  <summary>Important commands for this exercise:</summary>
  
  ```console
  $ git bisect start 
  $ git bisect good <SHA>
  $ git bisect bad <SHA>
  $ git bisect start <GOOD> <BAD>
  $ git bisect run ls index.html
  $ git add -p
  ```
</details>
