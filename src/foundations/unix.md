# Unix Shell

A huge proportion of scientific computing, software engineering, and data science is done using decendants of the Unix operating system. Both Linux and macOS are in the Unix family tree, and as such, they offer a "shell" for talking to the operating system. A shell is essentially a program to launch other programs. 

In practice, the shell is frequently used for issuing commands that manipulate files and folders on the computer, but the shell is a phoenomenally powerful mechanism for performing a huge number of tasks. It is generally accepted that a person who is considered a technologist of any kind will be comfortable working from the operating system (OS) shell.  



## Shell Basics

On Linux and macOS, you can access the shell by opening the `Terminal` application. Once you've opened the terminal, you will see a default command prompt that looks somewhat like the one below. 

```bash
work_macbook@:~ paul$
```

Note that `work_macbook` would actually be the name of your machine, and `paul` would be your username. Your prompt will obviously look a bit different. The key feature is that the prompt will typically end with the `$` character. This is where you issue commands to the operating system.

## Exploring Filesystem 

The filesystem you see when you interact with the prompt is the same as you would see using an application like `Finder` (on macOS). That is, you can see the files and folders as you normally would using the graphical user interface (GUI).

One of the most common commands used for exploring the file system is `ls`. This issues a command to the operating system to "list" the files in the currect directory.


```bash
ls
```

```
Applications         Dropbox (Brown)   Public      software
Creative Cloud Files Library           anaconda3   
Desktop              Movies            globus		
Documents            Music             projects
Downloads            Pictures          scratch
```

The output of `ls` shows a list of the files and directories (i.e., folders) in our current location. Note that by default, our "current location" is probably the "home" directory of our user. We can determine our current directory with the `pwd` command, which is short for **p**rint **w**orking **d**irectory). See the example below.

```bash
pwd
```

```
/Users/paul
```

And in the example above `paul` would be replaced by your username. 

Note that we can use `ls` to show more information or to display the information in slightly different way. This is done by passing optional arguments when calling `ls`. For example, it is very common to run `ls -l`, which produces output like you see below.

```
drwx------@  3 paul  988096886    96 May 15 16:18 Applications
drwx------+  4 paul  988096886   128 Aug 17 09:09 Desktop
drwx------+  9 paul  988096886   288 Jun 19 12:01 Documents
drwx------+ 94 paul  988096886  3008 Aug 24 08:38 Downloads
drwx------@ 10 paul  988096886   320 May 28 09:23 Dropbox (Brown)
drwx------@ 72 paul  988096886  2304 Aug  1 13:02 Library
drwx------+  5 paul  988096886   160 Jun 26 18:38 Movies
drwx------+  3 paul  988096886    96 Jul  5 11:37 Music
drwx------+  7 paul  988096886   224 Jun 19 14:08 Pictures
drwxr-xr-x+  4 paul  988096886   128 May 15 15:47 Public
drwxr-xr-x  27 paul  988096886   864 Jun  4 17:40 anaconda3
drwxr-xr-x   2 paul  988096886    64 Jun 27 12:36 globus
drwxr-xr-x  24 paul  988096886   768 Aug 23 09:11 projects
drwxr-xr-x   6 paul  988096886   192 Aug 20 16:22 scratch
drwxr-xr-x   7 paul  988096886   224 Aug  1 16:19 software
```

Adding the optional `-l` "flag" when calling the `ls` command gives us output that is much more verbose than our original `ls` command. We will explore in greater detail what each of these columns mean, but short explanation is that this gives us information about who owns the files or directories, what the permission settings are, the sizes, and when they were last changed. 

Another very useful flag we can pass when calling `ls` is the `-a` option. This tells the operating system we would like to see a list of _all_ files and directories in the current working directory—this includes those that are "hidden". It is worth noting here that on Unix-like systems, hidden files and directories have the `.` symbol as the first character in their names. Thus, saving a file as `.find_me.txt` on a Unix-like system would cause it to be a hidden file. 

We can also chain together flags when we call `ls`—or any other command. For example, running `ls -la` is very common, and it tells the operating system to list all the files, including the hidden ones, and to do so in the more verbose "long" format. 


We can move around the filesystem using the `cd` command. This command lets us **c**hange the **d**irectory in which we are currently. For example if we are in our home directory (e.g., `/Users/paul`) and we want to change to the `Documents` directory, we would issue the command below.

```bash
cd Documents
```

And now if we issue the `pwd` command, we will see our new current working directory has changed to something similar to the example below.

```
/Users/paul/Documents
```

We can return to our previous directory by typing the `cd ..`, which is the Unix shorthand for "_go back up one level in the file hierarchy_". This leaves us back in the `/Users/paul` directory. Note that if we wanted to back up two levels, we would run `cd ../..`, which would leave us in the `/Users` directory. And of course, we could take that even further by running `cd ../../..` which would take us up three levels in the hierarchy in to the `/` directory, which is the top-level directory.

Another very useful shorthand is using the `cd` command by itself. The default behavior when simply running `cd` is for the operating system to return you to your "home" directory. The "home" directory is the base location in the filesystem where a user will have files and directories belonging to them; in my case `/Users/paul` is my home directory. The files and directories within are "mine". It is also common to return to the home directory by running `cd ~` or sometimes `cd ~/`. All of these have the same effect of returning the user to their home directory.

Note that as we previously used the `cd` command to enter the `Documents` directory, we can also use `cd` to enter the sub-directories within `Documents` directory—that is, those directories that are themselves in the `Documents` directory. This is done using the same `/` notation that we used when moving up two levels in the filesystem hierarchy. That is, instead of running `cd ../..`, we would run `cd Documents/Courses`. Here `Courses` is the sub-directory within Documents.



### The Undeniable Beauty of `<tab>`-Complete

One of the wildly useful and lovely features of Unix-like shells is the ability to use the `<tab>` key to complete a command. For example, suppose we have directory named `my_very_important_cool_project`. And suppose further that we want to `cd` in to that directory. To accomplish this, we would obviously need to type `cd my_very_important_cool_project`. But suppose also that we are lazy and would prefer not to type out a 30-character directory name. This is the beauty of `<tab>`-complete. We can simply start typing our command (e.g., `cd my_very`) and then press `<tab>`, and the operating system will fill in the rest of the directory name. 


### Absolute and Relative Paths

It is worth noting at this point that the `cd` commands we have been running have thus far all been using the "relative" paths of directories. That is, the commands worked because or our position in the filesystem _relative_ to the directory we wanted to access. For example, if we were back in the `/Users` directory, running `cd Documents` would return the error below. 

```
bash: cd: Documents: No such file or directory
```

What this error tells us is that `cd` returned an error because it could not find that file or directory. And this is because the `Documents` directory is in the home directory of the user `paul`. So if we want `cd Documents` to work as we expect, we need to run that from within the `/Users/paul` directory. 

However, we could also acheive the desired result by passing the `cd` command the _absolute path_ of the directory. That is, we could run `cd /Users/paul/Documents`, and this would work exactly as intended. And furthermore, this would work as intended _regardless of where we are in the filesystem_. We could be anywhere, and if we run `cd /Users/paul/Documents`, it would always take us to the `Documents` directory in our home directory.

Note that the above applies for more than just the `cd` command; the concept of relative and absolute paths is also true for `ls` and any other command. For example we could be anywhere on the filesystem, and if we run `ls /Users/paul/Documents`, it will show a list of the files and directories in our `Documents` directory.



## Moving and Renaming Files

We can use the `mv` command both for moving and for renaming files and directories. Lets start by creating a file named `potato.txt`. We can use the `touch` command to create this file.

```bash
touch potato.txt
```

We can then use `mv` to rename the file to be `fries.txt` using the command below.

```bash
mv potato.txt fries.txt
```

And now we can also use `mv` to move the file to a completely different location.

```bash
mv fries.txt /tmp
```
The command above takes the `fries.txt` file and moves it to the `/tmp` directory.



## Creating Directories

We have already seen that `ls` can be used to list the contents of the current working directory. And we have seen that `pwd` will print the full path of our current working directory. Now we examine the command `mkdir`. As you might have guessed from the name, this command is used to **m**ake **d**irectories. For example, suppose we return to our `Documents` directory using the command below.

```bash
cd ~/Documents
```

We can then create the directory `/Users/paul/Documents/mpa2065` by running the following command.

```bash
mkdir mpa2065
```

We can now treat this directory like any other (i.e., create files or directories inside it). 



## Copying Files (and Directories)

We can use the `cp` command to create copies of files and directories. When creating a copy of a file, we simply pass two arguments to `cp`: the name of the "source" file, and the path or name of the copy being made. For example, let's create a file called `foo.txt` in our `Documents` directory. We can do this with the commands below. 

```bash
cd ~/Documents

touch foo.txt
```

Suppose now that we want to create a copy of `foo.txt` and call it `foo2.txt`. We can do this by running the command below.

```bash
cp foo.txt foo2.txt
```

The first argument to `cp` is our source file, and the second is what we want to call the output. 





## Removing Files and Directories

The `rm` command is used to remove (i.e., permanently delete) files and directories. The exact syntax for deleting a file is simply `rm <filename>`, where `<filename>` is the name of the file. So for example, the command below would delete the `foo.txt` file.

```bash
rm foo.txt
```

We can also use `rm` for deleting directories. This is done by passing the `-r` flag when calling `rm`. For example, the commands below creates and then subsequently deletes the directory `baz`. 

```bash
mkdir baz

rm -r baz
```
