# Introduction to Version Control and Git

In this lecture, you will learn what version control is and how to use git and GitHub for version control. 

**Attribution**
*The content of this lecture are modified from three excellent sources: [Git and GitHub](https://www.earthdatascience.org/courses/intro-to-earth-data-science/git-github/) from Earth Lab CU Boulder; [Intro to Unix](https://earth-env-data-science.github.io/lectures/environment/intro_to_git.html) from Columbia University; and [Version Control with Git](https://swcarpentry.github.io/git-novice/) from Software Carpentry.*

---

## What is Version Control?
A version control system maintains a record of changes to code and other content. It also allows us to revert changes to a previous point in time.

## Why Version Control?
The following figure is one reason you need version control:

```{figure} ../lectures/figures/final-doc-phd-comics.gif
---
name: date-version-control
class: bg-primary mb-1
width: 500px
align: center
---
Appending a date and number to version control. Source: "Piled Higher and Deeper" by Jorge Cham on [www.phdcomics.com](http://phdcomics.com/comics/archive/phd101212s.gif).
```

Version control is a powerful way to organize, back up, and share your research computing code with collaborators. A Version control system keeps track of a set of files and saves snapshots (i.e. versions, commits) of the files at any point in time. Using version control allows you to confidently make changes to your code (and any other files), with the ability to roll back to any previous state. 

Version control also allows you to share code with collaborators, make simultaneous edits, and merge your changes in a systematic, controlled way. There are different ways that a version control system can help you. Checkout the section on ["How Version Control Systems Work"](https://www.earthdatascience.org/courses/intro-to-earth-data-science/git-github/version-control/) on 	Earth Lab's course. 

## Git and GitHub

In this course, we will be using [git](https://git-scm.com/) for version control. Git is a distributed version control system that you can use locally on your computer, or through [GitHub](https://github.com/) and GitLab. In this course, we will also use GitHub for assignments and projects. 

If you do not have a GitHub account, you need a create one [here](https://github.com/) (it's free). 

``` {Note}
Git is very powerful, and has lots of utility with a steep learning curve. In this course, we will only use a subset of its functionality. You are encouraged to practice with git for your day-to-day research. 
```
First step to get started with git, is to make sure you have git installed on your computer. If you are not sure git is installed on your computer, open terminal and run the following command:
```
$ git --version
```
If git is installed, you will get an output with the version of git installed. Otherwise, you need to install git following the instructions [here](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

## Configure git on Your Computer
The first time that you use git on a computer, you will need to configure your GitHub.com username and email address. This information will be used to document who made changes to files in git. It is important to use the same email address and username that you setup on GitHub.com.

You can set your Github.com username in the terminal by typing:
```
$ git config --global user.name "username"
```
Next, you can set the email for your Github.com account by typing:

```
$ git config --global user.email "email@email.com"
```

Using the `--global` configuration option, you are telling git to use these settings for all git repositories that you work with on your computer. Note that you only have to configure these settings one time on your computer.

## Authentication for GitHub
GitHub requires authentication for any changes to a repo. The preferred method by GitHub is using a SSH key. Setting up SSH involves two steps:

1. Creating the key itself locally on your computer: Follow [these step](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to generate a new SSH key on your computer and add it to ssh-agent. 
2. Adding the key to your GitHub account: Follow [this step-by-step guide](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account) to add your SSH key to your GitHub account. 


## Get Started with a git repository
Create a new directory, use `git init` to initiate git version control system:
```
$ mkdir my_project
$ cd my_project
$ git init
```
At anytime, you can run `git status` to see what files have been modified/added/deleted compared to the previous commit, and what files are staged. 

To stage a file for addition to the repository use the following:
```
$ git add <filename(s)>
```
Then you need to *commit* the staged files to be added to the history of your repository:
```
$ git commit -m "a brief and informative commit message"
```
The commit message should be brief but indicative of what changes are being committed. It's important to stage and commit your changes in a way that it does not contain several unrelated changes to your code. For example, if you are making changes to different modules of your code, make sure to commit them separately, so if you need to revert one of the changes it's easy to do so. 

The following figure gives you a nice perspective on how staging and committing works:

```{figure} ../lectures/figures/git-add-commit.png
---
name: git-add-commit
class: bg-primary mb-1
width: 500px
align: center
---
Modified files are staged using git add. Then, following git commit, all files in the staging area are included in snapshot and become part of the repository's history, receiving a unique SHA-1 hash identifier. Source: Max Joseph, adapted from Pro Git by Chacon and Straub (2014).
```

## Push Changed Files to GitHub
To push your changes to your GitHub repository, you need to create a new repository on GitHub. You can do this using the following steps:
1. In the upper-right corner of any page, use the  drop-down menu, and select New repository.
2. Type a short, informative name for your repository.
3. Click Create repository.

``` {note}
You can choose to initialize your repository with a README. While this is recommended, do not do it for this exercise, otherwise the changes you made locally will be out of sync with your GitHub repository. 
```

Now that you have created your repository on GitHub, you need to copy it's URL and add it to your local git repository. Open your repository on GitHub and click on the green `Code` button and copy the SSH url (see the following figure).

```{figure} ../lectures/figures/git-url.png
---
name: git-url
class: bg-primary mb-1
width: 500px
align: center
---
Accessing the URL of a GitHub repository.
```
Lastly, you need to add the URL to your local repository and push the changes to GitHub:

```
$ git remote add origin <repo url>
$ git push origin main
```

<p>&nbsp;</p>