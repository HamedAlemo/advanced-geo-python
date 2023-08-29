# Introduction to Unix

This lectures covers an introduction to Unix system, commands and the file system. 

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