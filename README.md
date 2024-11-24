# **Git Workshop 

Welcome to the **Git Workshop**! This repository will serve as the base for our workshop activities.
Note that this workshop assumes you already have git installed and connected to your GitHub account

---
## Overview:
1. Learning about local git
2. Commiting changes
3. Connecting Local git to GitHub

---

## **Getting Started**
### 0. Introduce yourself to git
- *If you have never used git before on your machine*, then you need to introduce yourself!
- We need to tell git who we are. More specifically, we need to tell git which name and email we want to associate with our commits and our account
`git config --global user.name "Name Here"`
`git config --global user.email "yourEmail@gmail.com"
- Here were configuring a global configuration key, thus it will apply to all git repository's from now on
- you can view all your git config settings using: 
`git config --list`
- Or you can view specific config values:
`git config <key>`
`git config user.name`

### 1. Init a git repo
- Git will only work if we tell it which repositories we want it to track. 
- Navigate to the repository you want to track
- Tell git that we want it to track this file
`git init`
- This will create a `.git` file within your repo. Note that it is a hidden file
- Note also that no branch has been made yet
`git branch` returns nothing.
- Let's create our main branch
`git checkout -b main`
- For more information about branches, and what this is doing, see the branch section

### 2. Changes

---
    - There are some handy commands we will be using this tutorial that speeds up the process of changing files
    `touch filename.txt` Creates an empty file
    `rm filename.txt` Deletes the file (Careful, it will not ask for permission and is unrecoverable)
    `echo "A line of text" >> filename.txt` Appends (adds) the line of text to the end of the file, or creates a new file if filename.txt does not exist. 
        - Note: if you use a single arrow: `>` instead of a double `>>` your entire file will be rewritten with just your new line of text
    - We can check the contents of our file using `cat`
    ```
    > cat filename.txt
    A line of text
    ```
---
- Assuming that it is an empty repository, there is nothing for our git to track. Let's create a file and start tracking it
`echo "hello" >> a.txt`

- Using the append command we have created our first, file, a.txt
- There has now been a change to the repository!
#### git status
- `git status` is our best friend. We will be using it a lot. 
- In a way, git status is our home base. It provides general information about our repo, and about the files git is managing
- It is here we start to discuss the git workflow
```
git status
On branch main

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	a.txt

nothing added to commit but untracked files present (use "git add" to track)

```
*Untracked Files*
- Untracked, as one would expect, are not tracked by git. Git only tracks files that we explicitly tell it to. 
- Currently, our `a.txt` file is untracked, thus if we were to delete our file, the file and our changes would be lost.

`git add a.txt` This now adds our file to the staging area.
---
**`git add` and the Staging area**
- Using `git add` on an untracked file will tell git to start tracking that file, and add its current state to the **staging area**
- The staging area is where files have are put, ready used in a commit. 
    - The staging area is a snapshot of the file, at the time it is added.
    - If further changes of the file are made, we need to update this snapshot, by repeating `git add a.txt`
    - One way to picture the purpose of the staging area, is to think of it as the counter at a restaurant the chef's put the food on for the servers to take to the customers,
    - If the food needs changes (perhaps the chef forgot some salt) changes can still be made to the plate. (using `git add filename` again after changes have been made)
    - If the food (file) is a mistake, and never should have been served, it can be removed from the counter `git rm --cached filename`
---


### **1. Fork This Repository**
- Go to the top-right corner of this repository's page.
- Click the **Fork** button to create a copy under your GitHub account.

### **2. Clone Your Fork**
- Copy the URL of your forked repository.
- Run the following command in your terminal to clone the repository locally:
  ```bash
  git clone https://github.com/your-username/git-workshop.git
  cd git-workshop

