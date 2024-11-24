# Git Workshop

Welcome to the **Git Workshop**! This repository will serve as the base for our workshop activities.
Note that this workshop assumes you already have git installed and connected to your GitHub account

## Overview:
1. Learning about local git
2. Committing changes
3. Connecting Local git to GitHub

---

## Introduce Yourself to Git
```
git config --global user.name "Name Here"
git config --global user.email "yourEmail@gmail.com"
```
- *If you have never used git before on your machine*, then you need to introduce yourself!
- We need to tell git who we are. More specifically, we need to tell git which name and email we want to associate with our commits and our account
- Here were configuring a global configuration key, thus it will apply to all git repository's from now on
- you can view all your git config settings using:\
`git config --list`
- Or you can view specific config values:\
`git config <key>`\
`git config user.name`\

## Init a Git Repo
- Git will only work if we tell it which repositories we want it to track. 
- Navigate to the repository you want to track
- Tell git that we want it to track this file\
`git init`
- This will create a `.git` file within your repo. Note that it is a hidden file
- Note also that no branch has been made yet\
`git branch` returns nothing.
- Let's create our main branch\
`git checkout -b main`
- For more information about branches, and what this is doing, see the branch section

## Changes
 There are some handy commands we will be using this tutorial that speeds up the process of changing files\
 ```
touch filename.txt Creates an empty file\
rm filename.txt Deletes the file (Careful, it will not ask for permission and is unrecoverable)\
echo "A line of text" >> filename.txt (Appends (adds) the line of text to the end of the file, or creates a new file if filename.txt does not exist)
    - Note: if you use a single arrow: > instead of a double >> your entire file will be rewritten with just your new line of text so be careful
cat filename.txt (print a file to the terminal)
```

- Assuming that it is an empty repository, there is nothing for our git to track. Let's create a file and start tracking it\
`echo "hello" >> a.txt`

- Using the append command we have created our first, file, a.txt
- There has now been a change to the repository!

### Git status

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

**Untracked Files**
- Untracked, as one would expect, are not tracked by git. Git only tracks files that we explicitly tell it to. 
- Currently, our `a.txt` file is untracked, thus if we were to delete our file, the file and our changes would be lost.
- `git add a.txt` This now adds our file to the staging area.

## Git Add and the Staging Area 
```
git add . (Take a snapshot of your entire reposity and adds it to the staging area)
git add * (Add all new and modified file, does not stage hidden files, does not stage file deletions)
git commit -a (Skip the staging step. Add all files that have been changed/deleted. Does not add untracked files to stageing area)
```
- Note on file deletions. If deleting a tracked file locally,(`rm filename.txt`), we need to tell git that changes have been made to the file. Use `git add filename.txt` to stage individual deletions to the staging area

- Using `git add` on an untracked file will tell git to start tracking that file, and add its current state to the **staging area**
- The staging area is where files have are put, ready used in a commit. 
- The staging area is a snapshot of the file, at the time it is added.
- If further changes of the file are made, we need to update this snapshot, by repeating `git add a.txt`
    - One way to picture the purpose of the staging area, is to think of it as the counter at a restaurant the chef's put the food on for the servers to take to the customers,
    - If the food needs changes (perhaps the chef forgot some salt) changes can still be made to the plate. (using `git add filename` again after changes have been made)
    - If the food (file) is a mistake, and never should have been served, it can be removed from the counter `git rm --cached filename`

---

## Git Commit
```
git commit  (opens text editor to add details about commit)
git commit -a (adds all tracked files to staging area and opens text editor)
git commit -m "Commit message" (commit message in command, does not open text editor)
git commit -am "Commit Message" (Adds all tracked files into staging area, inline commit message)
```

- Let's suppose we are in a place with our repository that we want to save. 
- To be able to come back to this exact point, let's make a commit\
`git commit -m "add file a.txt to the repository"`\
- We've now created a commit, a snapshot of all our tracked file at the point of the commit
- each commit has a commit ID that can be called if we ever want to view this commit later.
- If we ever want to call the ID, we don't have to use the entire commit ID value, just enough to provide uniqueness. A minimum of 4 values. 

---
- Let's create another change, and another commit so that we have a second commit
```
echo "second commit text" >> a.txt
git commit -am "update a.txt"
```
- Here we are combining the -a and -m options, thus through our commit message we are adding any changes in all our tracked files, and adding the commit message within a single line. Very handy
    - Note that the `-a` option does not add untracked files to the staging area
- lets see what happens if we want to go back to our old commit point

## Git Log
```
git log (Show past commits in full)
git log --oneline (Show one line for commit)
git log -5 (Only show the logs of the last 5 commits)
git log --oneline --graph --all --decorate (--graph show a graphical version of the commit history, --all shows all branches, --decorate labels branches)
git log -S "string" (show logs that have changed any lines that contain the string)
git log -patch (or -p for short, Shows line changes within log)
```
- `git log` allows us to view the commit history of a git repository. It provides a lot of in depth information, however it is not very useful as an out of the box tool. 
- Let us add the following options:\
`--oneline` Shorten the commit to just 1 line\
'--all' Shows all branch paths\
'--graph' Visually show the path of the commit history\
`-5` Replace 5 with any number, this limits the output to show the last 5 commits in the history (very useful)\

- Thus let's run our new command:\
`git log --oneline --all --graph -5` 
- Note that since we only have 2 commits, our limit of 5 does nothing

- For a very comprehensive git log that provides oneline, graph, color, relative date of commit, commit hash, and commit message, create the following alias:
```
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
```

## Git Checkout
```
git checkout BranchName (Set branchName as current branch)
git checkout -b newBranch (Create newBranch and set as current branch)
git checkout commitID (checkout a specific commit, replacing commitID with first 4-5 values of the commit Hash value)
```

- We can now make a note of the first commit ID, and let's view the repository at a certain point in history\
`git checkout 'commitID'`
- We've now disconnected from the main branch, and are now a floating HEAD.\
**HEAD** - A side note:
- `HEAD` is the pointer to whatever commit we are currently observing.
- Normally `HEAD` is attached to a branch, e.g. main, which it automatically tracks and remains unseen. 
- When we checkout a different branch, we are moving our HEAD to look at the commitID that the branch is currently pointing to. 
- However, we can disconnect our HEAD pointer from the branch and take a look at other commits.\
`cat a.txt` shows that we are looking at a version of our file at the point of the first commit.\
- In general, don't make any changes while floating. If you really need to make changes from a certain point in history, create a new branch at that point, and make changes from here, then merge into main.\
`git checkout main` reattach our HEAD pointer to follow the main branch 
- Check https://learngitbranching.js.org/ for a great visualization of what branches are doing within git, and how we can move the HEAD pointer to different commits in the commit history

## Branches (Finally)
```
git checkout branchName  (swap to sepcified banche)
git checkout -b NewBranchName  (create new branch and move to it)
git branch  (lists local branches)
```
- At long last we get to branches. 
- Using a git branch is a way of making experimental changes to a repository while also maintaining a working copy
- Suppose you have to present an update to your class, and must show a working prototype. The main branch of the git repo is working and we dont want to effect it, but we still want to keep working on the project. What do we do?
- We make a branch!\
`git checkout -b newBranchName`
- We now have a branch that we can make changes to, make commits to, and progress the project further, all while keeping the working copy of the file ready for the demo.
- Once we finish our demo, we can easily merge our experimental branch to our main branch, and continue working from where we left off

### Main

- Say it with me: "**Main is holy**". Main should always be a working copy of your project. If main is not functional, something has gone very wrong. 
- Code updates should be performed on development branches, and only once they are function should they be merged into main.
- It is from main that we merge our other branches into, applying the changes in the code to our own.

### Branch Workflow
- Thus, when we want to make changes, follow the following workflow
```
git checkout -b bugFix
echo "within bugfix" >> a.txt (make changes within bugFix)
git commit -am "fix bug"
echo "second commit within bugifx" >> a.txt (Maybe fix a second bug)
git commit -am "fix second bug"
git checkout main
git merge bugFix
git branch -d bugFix
```
Let's break down what's happening:
1. Create and checkout a new branch called bugFix
2. We make our changes within the branch
3. Add and commit our first fix
4. Fix the second bug in the code
5. Commit the second bug fix
6. Now that our fixBug branch is working perfectly, we checkout main to merge the changes
7. Merge the changes from bugFix into our main branch
8. Now that we have fixed our bug, we can delete or bugFix branch. All this does is remove the pointer to this commit, the commit history still exists. We just want to clean up our git and keep things organized

## Merge Conflicts
```git
Auto-merging a.txt
CONFLICT (content): Merge conflict in a.txt
Automatic merge failed; fix conflicts and then commit the result.
```
**Do not panic!**\
- During merging, Git is pulling in changes from both branches and trying to rectify them
- Conflicts arise when we changed the same line in a file from 2 different branches.
- Running `git status` tells us that we have conflicts to solve
- Git helps us along the way, and gives us instructions on what to do:
```git
On branch main
You have unmerged paths.
  (fix conflicts and run "git commit")
  (use "git merge --abort" to abort the merge)

Unmerged paths:
  (use "git add <file>..." to mark resolution)
        both modified:   a.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
- Let's fix our conflicts ourselves
- If we print our a.txt file well notice that the file looks very different
```git
old text
<<<<<<< HEAD
Goodbye from main
=======
hello
>>>>>>> bugFix
```
- Here we have our conflict line laid out for us
- everything from `<<<<<<<< HEAD` to the `========` is from the main branch (where our HEAD currently points)
- everything from `========` to the `>>>>>>>> bugFix` is from bugFix branch 
- Choose one of the 2 texts or neither and put whatever we want.
- To fix this, open the file within a text editor of your choice.
- Navigate to the problematic lines and replace the whole section (from the `<<<<<<` to the `>>>>>>`) with your fix:
```
old text
hello and Goodbye from main
```
- stage the file
```
git add a.txt
```
- Using `git add` will mark that file as resolved.
- Since we only had 1 file conflict, the conflict can now finish our merging process
- We need to make one more commit. Why? Because changes to files have occurred during our resolution process
```git
git commit -m "reslolve conflict merge with bugFix and Main"
```
- one slight note, we have pulled the changes from bugFix into main, but have not pulled changes from main into bugfix
- What does this mean? Our latest conflict-resolution that has happened is not seen in bugFix
- `git log --oneline --decorate --all --graph` shows that main is ahead of bugFix by one commit
```git
*   467eb2d - (HEAD -> main) fix conflict (2 seconds ago) <DannyPlatt>
|\  
| * b492774 - (bugFix) commit from bugFix (28 minutes ago) <DannyPlatt>
* | 526ec4f - Commit from main to create conflict (27 minutes ago) <DannyPlatt>
```
- This is fine if we are deleting it, however if we intend to keep it around, we must update it to match the changes from main before making changes
```
git checkout bugFix
git merge main
```
- Now the git log will show both branches on the same commit
```
*   467eb2d - (HEAD -> bugFix, main) fix conflict (26 seconds ago) <DannyPlatt>
```
