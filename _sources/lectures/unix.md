# Introduction to Shell and Bash

This lectures covers an introduction to Unix file system, and Shell/Bash commands. 

**Attribution**
*The content of this lecture are modified from three excellent sources: [Introduction to Bash (Shell)](https://www.earthdatascience.org/courses/intro-to-earth-data-science/open-reproducible-science/bash/) from Earth Lab CU Boulder; [Intro to Unix](https://earth-env-data-science.github.io/lectures/environment/intro_to_unix.html) from Columbia University; and [The Unix Shell](https://swcarpentry.github.io/shell-novice/) from Software Carpentry.*

---

## Background

We interact with computers in many different ways, such as through a keyboard and mouse, touch screen interfaces, or using speech recognition systems. The most widely used way to interact with personal computers is called a graphical user interface (GUI). With a GUI, we give instructions by clicking a mouse and using menu-driven interactions.

While the visual aid of a GUI makes it intuitive to learn, this way of delivering instructions to a computer scales very poorly and it is not reproducible. Imagine the following task: for a literature search, you have to copy the third line of one thousand text files in one thousand different directories and paste it into a single file. Using a GUI, you would not only be clicking at your desk for several hours, but you could potentially also commit an error in the process of completing this repetitive task. This is where we take advantage of the Unix shell. The Unix shell is both a command-line interface (CLI) and a scripting language, allowing such repetitive tasks to be done automatically and fast. With the proper commands, the shell can repeat tasks with or without some modification as many times as we want. Using the shell, the task in the literature example can be accomplished in seconds.

## The Shell

Shell is the primary program that computers use to receive code (i.e. commands) and return information produced by executing these commands (i.e. output). These commands can be entered via a Terminal, which you will work with in this course.

Using a Shell helps you:

- Navigate your computer to access and manage files and folders (i.e. directories).
- Efficiently work with many files and directories at once.
- Run programs that provide more functionality at the command line such as git for version control.
- Launch programs from specific directories on your computer such as Jupyter Notebook for interactive programming.
- Use repeatable commands for these tasks across many different operating systems (Windows, Mac, Linux).

Shell is also important if you need to work on remote machines such as a high performance computing cluster (HPC) or the cloud.

The most popular Unix shell is Bash (the Bourne Again SHell — so-called because it’s derived from a shell written by Stephen Bourne). Bash is the default shell on most modern implementations of Unix and in most packages that provide Unix-like tools for Windows. Note that ‘Git Bash’ is a piece of software that enables Windows users to use a Bash like interface when interacting with Git.


## Terminal Sessions On Your Computer

The terminal program that you use to run `Bash` commands will vary depending upon your computer’s operating system.

**Mac (OS X)**

You can use the program called Terminal, which uses the Bash implementation of Shell and is installed natively on the Mac OS.

You can open Terminal by finding and launching it from Spotlight (or from /Applications/Utilities).


**Linux**

Many Linux computers use the Bash implementation of Shell, which you will learn to test for in the section below.

You can open the program called Terminal (or Terminal Emulator) by finding and launching it from your list of programs.

**Windows**

There are many options for running Bash on Windows. In this course, we recommend using Windows Subsystem for Linux (WSL). WSL is a feature of the Windows operating system that enables you to run a Linux file system, along with Linux command-line tools and GUI apps, directly on Windows, alongside your traditional Windows desktop and apps. You can read more about it [here](https://learn.microsoft.com/en-us/windows/wsl/faq). 

To enable WSL on windows, follow the steps outlined [here](https://learn.microsoft.com/en-us/windows/wsl/install). The default Ubuntu distribution works well with the content of this course, and you do not need to change it. 


## Home Directory
To understand what a “home directory” is, let’s have a look at how the file system as a whole is organized. For the sake of this example, check the following figure that illustrates the file system on Hamed's computer. After this illustration, you’ll be learning commands to explore your own filesystem, which will be constructed in a similar way, but not be exactly identical.

On a Unix computer, the filesystem looks like something this:

```{figure} ../lectures/figures/unix_files.png
---
name: unix
class: bg-primary mb-1
width: 500px
align: center
---
Hamed's file system tree
```

The filesystem looks like an upside down tree. The top most directory is the **root directory** that holds everything else. We refer to it using a slash character, `/`, on its own; this character is the leading slash in `/Users/hamed`.

Inside that directory are several other directories: `bin` (which is where some built-in programs are stored), `lib` (for the software “libraries” used by different programs), `users` (where users’ personal directories are located), `tmp` (for temporary files that don’t need to be stored long-term), and so on.

By default, when you open your terminal it lands in your home directory, which in our example is `/Users/hamed`. We know that this directory is stored inside `/Users` because `/Users` is the first part of its name. Similarly, we know that `/Users` is stored inside the root directory `/` because its name begins with `/`.

``` {tip}
There are two meanings for the `/` character. When it appears at the front of a file or directory name, it refers to the root directory. When it appears inside a path, it’s just a separator.
```

## Bash Commands to Navigate Files and Directories

Now, let's review some of the useful bash commands to navigate and manipulate files and directories in your filesystem.

### Print a List of Files and Subdirectories (`ls`)

`ls` prints the names of the files and directories in the current directory in alphabetical order, arranged neatly into columns. Here is the output of running `ls` inside the directory of this book on a local computer:
```
$ ls
```
```
CONDUCT.md		_config.yml		lectures
CONTRIBUTING.md		_toc.yml		logo.png
LICENSE			assignments		references.bib
README.md		docs			requirements.txt
_build			intro.md
```
We can make its output more comprehensible by using the flag `-F`, which tells `ls` to add a trailing `/` to the names of directories:

```
$ ls -F
```
```
CONDUCT.md		_config.yml		lectures/
CONTRIBUTING.md		_toc.yml		logo.png
LICENSE*		assignments/		references.bib
README.md		docs/			requirements.txt
_build/			intro.md
```
To print all files and directories, including hidden ones, you can add the `-a` flag:
```
$ ls -aF
```
```
./			LICENSE			intro.md
../			README.md		lectures/
.DS_Store		_build/			logo.png
.git/			_config.yml		references.bib
.gitignore		_toc.yml		requirements.txt
CONDUCT.md		assignments/
CONTRIBUTING.md		docs/
```

The `../` directory in the output of `ls -aF` is a special directory name meaning "the directory containing this one" or simply the **parent** of the current directory. You will learn in the following how to navigate to the parent directory. 

### Print Current Working Directory (`pwd`)

To print the name of the current working directory, use the command `pwd`. This commands prints the full path to the directory (meaning that you can see the parent directory).

```
$ pwd
```
```
/Users/hamed
```

### Change Current Working Directory (`cd`)
The command to change locations is `cd` followed by a directory name to change our working directory. `cd` stands for “change directory”.

Let's say we are inside the directory of this book, and we want to move to the `lectures` directory we saw above. We can use the following command:
```
$ cd lectures
```
There is no output from this command. But if you are `pwd` you can confirm that you are in `lectures` directory now. 

You can use the same `cd` command to also go to the parent directory of the current directory:
```
$ cd ..
```

``` {tip}
If you run `cd` without any arguments it will return you to your home directory. This is equivalent to running `cd ~`
```

So far, when specifying directory names, or even a directory path (as above), we have been using **relative paths**. When you use a relative path with a command like `ls` or `cd`, it tries to find that location from where we are, rather than from the root of the file system.

However, it is possible to specify the **absolute path** to a directory by including its entire path from the root directory, which is indicated by a leading slash. The leading `/` tells the computer to follow the path from the root of the file system, so it always refers to exactly one directory, no matter where we are when we run the command.

`````{admonition} A useful shortcut
:class: tip
You can use the `-` (dash) character with `cd` to move into the previous directory you were in. This is very helpful instead of having to remember the full path. 
`````

### Create a New Directory (`mkdir`)

To create a new directory you can use `mkdir` followed by the name you would like to give the new directory. If you only give a name, the new directory will be created in the current directory. You can also give the **absolute path** to `mkdir` to create a new directory anywhere on your file system. The following command will create a new directory in Hamed's home directory named `new-directory`:

```
$ mkdir /Users/hamed/new-directory/
```
### Create a New File Using a Single Command (`touch`)

You can create a new empty file using the single command `touch`. This command was originally created to manage the timestamps of files. However, if a file does not already exist, then the command will make the file.

This is an incredibly useful way to quickly and programmatically create a new empty file that can be populated at a later time. Here is an example:
```
$ touch samples.txt
```

### Edit a File Using Vim

There are various editors that you can use to edit a file in Bash. These are very useful if you need to edit text in a plain text file, or in HTML, LaTex or other markup languages. While these editors might not seem as easy to use as other standard GUI-based editors initially, they can help you become very productive over the long run. 

In this course, we are going to use Vim as editor. Vim can have a steep learning curve, and you do not need to learn all the commands in the beginning. Start with navigating between the *command mode* and the *insert mode*, edit the text and save it to the file. We will practice these commands in the class. For a complete introduction to Vim commands check out [A Beginner's Guide to Vim](https://www.linuxfoundation.org/blog/blog/classic-sysadmin-vim-101-a-beginners-guide-to-vim) on Linux Foundation blog. 


### Copy a File (`cp`)

You can copy a specific file to a new directory using the command `cp` followed by the name of the file you want to copy and the name of the directory to where you want to copy the file. The names can be relative path or absolute path. 

For example, to copy the file  `samples.txt` from the current directory to `/Users/hamed/documents/`

```
$ cp samples.txt /Users/hamed/documents/
```


### Copy a Directory and Its Contents (`cp -r`)
To copy a directory and all its content to a new directory, you need to use the flag `-r` (meaning recursive) with `cp`. 

For example, to copy the directory `documents` (and all its content) from Hamed's home directory to `/Users/hamed/projects/` you can run:
```
$ cp -r /Users/hamed/documents/ /Users/hamed/projects/
``` 

### Delete a File (`rm`)
To delete a specific file, you can use the command `rm` (abbreviated for remove) followed by the name of the file you want to delete.

For example, you can delete the `samples.txt` file under the current directory:

```
$ rm samples.txt
```

### Delete a Directory (`rm -r`)
To delete a directory and all its content (be careful when using this command as Unix doesn't have a trash bin), you can use the `-r` flag with `rm`.

For example, the following command will delete the `projects` directory and all its content from the current directory:
```
$ rm -r projects/
```

## Getting help
Every command in bash has multiple options that you can pass to change the output. There are two ways to find out what options are available:

1. Pass `--help` to any command:
```
$ ls --help
```
2. Read the manual using `man`:
```
$ man ls
```

<p>&nbsp;</p>