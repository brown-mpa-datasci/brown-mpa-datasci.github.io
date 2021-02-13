# Git Basics
The most popular version control system for code is Git. In this section we will discuss the basic features of a version control system as well as why version control systems are important. We will also go through the basics of Git, in particular, as well as its relative advantages over other version control systems that came before. 

## Why Version Control?
Version control systems exist to solve a number of related problems. First, we would like snapshots of our code that allow us to implement new features and components that map to a particular version tag (e.g., "_Encrypted sharding is available as of version 1.2.0_"). Second, we would like to confidentally make changes to our code while also preserving the ability to "roll back" the code to a known-good state. Being able to experiment with so-called breaking changes before pushing them in to a more production-level release is an essential component of writing code. Third, we would like to be able to code collaboratively such that one person can be working on feature `abc` and another person working on feature `xyz` in the same code base. This last problem (i.e., having _distributed_ version control) is solved particular well by Git. 

### Distributed Version Control
The predecessors of Git were less effective in solving the problem of distributed version control. And since modern code bases are often in the hundreds-of-thousands (or even millions) of lines of code, it would be impossible for a single developer to do all the maintence. Thus, we need large teams to work collaboratively, while also preserving the ability to make changes without "clobbering" each others' work.

You may not have considered this yet, but if you have ever used Google Docs, or any similar product, then you have already used a distributed version control system. Google Docs can be shared and simultaneously editted by an arbitrarilly large number of authors. Moreover, Google also provides some functionality for reversing changes and re-instantiating prior versions of the document. 


## What is a Git Repository?
At a high-level, a Git repository—often called a "repo"—is a directory which we have flagged to be version controlled by Git. Essentially, we have told Git "_Please track changes to files in this directory_". 

A very typical Git workflow is to have a repository per project or per software application. Files are then "checked in" to version control when we tell Git that we want the files tracked. We then take snapshots—known as "commits" in Git parlance—when we make significant or important changes. 


### Local vs. Remote Repositories
A key distinction should be made before we move on. That distinction is between the "local" and "remote" repository. As the name implies, a local repository exists on you "local machine" (e.g., your laptop or desktop). A remote repository, on the other hand, exists in some location other than your local machine; thus, it is remote in the sense that it is elsewhere. Remote repositories are typically housed on purpose-built platforms for code sharing and version control. 

### Github and Remote Repos
Github is one of the most popular code sharing and versioning platforms; other similar platforms currently include Gitlab and Bitbucket. All three of these platforms share a great deal of the same functionality. In particular, they give us a place to store, distribute, and backup our code. These platforms are typically what we use to house our "remote repos" mentioned above. 

## Basic Git Workflow
In this section we walk through a standard Git workflow of creating a repository, then committing code to the repository, making some changes, and then committing the changes. We must first ensure that Git is actually installed on our machine; to confirm this, we can simply open the shell and run `git --version`. This should return some output like we see below.
```
git version 2.20.1
```
If we instead observe an error message suggesting `command not found`, then we must install Git through the standard methods (e.g., `brew install git` on macOS, `apt-get install git` on Debian and Ubuntu, `yum install git` on CentOS and Red Hat, etc.).


### Creating a Git Repo

As mentioned above, a Git repository is a directory that we have asked Git to monitor. Thus, if we are starting a new project, we would often begin by creating the diretory itself. Recall that on Unix-like systems we can create directories using the `mkdir` command. 

Suppose we like the first sentences of novels, and suppose that we are creating a repository to store all our favorite first lines. Let us create a directory called `first_lines`. We do this by issuing the command below. 

```bash
mkdir ~/first_lines
``` 

Note that by specifying `~/first_lines`, we will be creating the directory in our "home" directory, (i.e., in my case, `/Users/paul`). So I should now have a directory at `/Users/paul/first_lines`. To confirm this, we can run the command below.

```bash
ls ~/
```
And we should see the `first_lines` directory in the output of that command.

Now, in order to actually initialize this directory as a git repo, we will first `cd` in to the directory with this command:

```bash
cd ~/first_lines
```

And once we are inside the `first_lines` directory, we can then initialize the directory as a git repository with this command:

```bash
git init
```

This has the effect of telling `git` that we want the changes to the contents of this directory to be tracked. Just to confirm, we can then run this: 

```bash
git status
```

and we should see some output like this:

```
On branch main

No commits yet

nothing to commit (create/copy files and use "git add" to track)
```

As this output suggests, we are on the `main` branch in this repository, and we have not yet made any commits.


### Making our First Commit

Let's open a plaintext editor (e.g., Nano, Vim, Emacs, Sublime) and create a file called `lines.txt` and populate with our first entry, which is the first line of _Jane Eyre_.

```
There was no possibility of taking a walk that day.
```

Let's save and exit from our text editor. And now we will again run `git status`. This time we get some more interesting output.

```
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	lines.txt

nothing added to commit but untracked files present (use "git add" to track)
```

As we see above, git has now noticed that we have a file that exists in this repo, but it is not yet tracked. And Git even gives us the hint that our next step to add the file to be track is to use the `git add` command, which we do with the command below. 

```bash
git add lines.txt
```

And now when we run `git status` again, we see something like the output below.

```
On branch main

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   lines.txt
```

Git has noticed that we have added a file to the staging area, but no commits have been made yet. We can finally make the commit with the command below.

```bash
git commit -m "added line from jane eyre"
```

The `git commit` command tells Git to add the file(s) from the staging area to the repository, and we pass it a commit message using the `-m` optional flag followed by the message in quotes. Git will then provide some output like we see below to confirm that the commit has been successful.

```
[main (root-commit) aa601ee] added line from jane eyre
 1 file changed, 1 insertion(+)
 create mode 100644 lines.txt
 ```
 
 We can also get more information about the commit by using the `git log` command, which generates output much like what we see below.

```
commit aa601eed8c173947c345fa1d213a919bdf2c11cd (HEAD -> main)
Author: paul <paul@gmail.com>
Date:   Wed Sep 10 18:43:51 2019 -0400

    added line from jane eyre
```

A couple of points ought to be noted here. First, git commits all have unique identifiers that are a 40-character string of alphanumberics. This is how we can uniquely identify a commit. Also note that the commit log stores all the information regarding the commit's author and timestamp. And of course, the commit log has the commit message associated with the commit.


### Adding a New Commit

Suppse we want to add another line to our `lines.txt` file. In this case, let's add the first line of _Anna Karenina_ using our text editor.

```
Happy families are all alike; every unhappy family is unhappy in its own way.
```

Now let's save those changes and close our text editor. And if we run `git status` again, we see something like the output below. 

```
On branch main
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   lines.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

As we can see, Git has noticed that we have made changes to the `lines.txt` file. In order to capture these changes in the repo, we need to use `git add lines.txt` once again. After that, we can move those changes from the staging area to the actual repository with the command below.

```bash
git commit -m "added anna karenina"
```

Now in case we are curious we can explore the differences between Git commits using the `git diff` command. In particular, we use `git diff` in combination with the commit ID (or the first few characters of it), and the file name. 

```bash
git diff aa601 lines.txt
```

As we see in the command above, we tell Git to show us the differences between in the `lines.txt` file in the current state and that of the commit whose commit ID starts with `aa601`.
 
And we would then see some output like this:
```
diff --git a/lines.txt b/lines.txt
index ecc387a..897a0a3 100644
--- a/lines.txt
+++ b/lines.txt
@@ -1 +1,2 @@
 There was no possibility of taking a walk that day.
+Happy families are all alike; every unhappy family is unhappy in its own way.
```


## Remote Repositories

The concept of a "remote repository" highlights one of Git's greatest strength. As mentioned above, a local repository refers to the Git repository on your "local" machine (but note that "local machine" might actually be the server you are using). The "remote repository" is a repository that lives elsewhere—typically on a hosting platform such as Github or one of their counterparts (e.g., GitLab, Bitbucket, etc.). 

Remote repos enable the distributed aspect of version control with Git. For example, we might have two software engineers, Jones and Lee, each working on the same code base. Lee might be adding feature `xyz` and Jones might be adding feature `abc`. They can both implement the features on their local machines, and in many cases, neither needs to be involved in the other's development. Then, once they are finished, they can push their respective changes to the remote repository where they can be integrated. 


### Adding a Remote Repository

For repositories that we have started "from scratch" on our local machines, we can add a remote repo whenever we would like. This has a couple of steps.

  1. Create remote repo
  2. Grab URL of the remote repo
  2. Add remote to local git

The above steps are carried out differently depending on the hosting platform you choose, but they should be fairly transparent once you have done it once or twice. On GitHub, we simply click on the `+` icon in the top-right corner, and then select `New repository`. 

Once we have created the remote in GitHub (or on another hosting platform), we can simply return to our local repo and run this

```bash
git remote add orgin <URL> 
```
where `<URL>` is replaced by the URL for the newly created remote repo. 



### Pushing Commits to a Remote Repo

Once we have added our remote repo, and we have made some commits, we are ready to push these to the remote repo. This is simply done using `git push` command followed by the name of the remote, which we specified above as `origin` as well as the name of the branch. In the example below, we are pushing to the `main` branch. 

```bash
git push origin main
```

