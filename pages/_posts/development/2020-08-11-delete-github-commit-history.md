---
layout: post
title: "Delete GitHub Commit History"
description: "How to clone a GitHub repository and replace all existing commit history with an initial commit."
image: "/assets/images/development/delete-github-commit-history/github_logo_200x200.png"
categories: [development]
tags: [github, github-commit-history, github-repository]
---

To delete all existing commits and recreate an initial commit.

NB. Some repositories use **main** instead of **master** as a branch name.

### First Method

```
# Clone the project, e.g. "myproject" is my project repository:
git clone << REPO_LINK >>

# Since all of the commits history are in the ".git" folder, we have to remove it:
cd myproject

# Check out to a temporary branch:
git checkout --orphan TEMP_BRANCH

# Add all the files:
git add -A

# Commit the changes:
git commit -am "initial commit"

# Delete the old branch:
git branch -D master

# Rename the temporary branch to master:
git branch -m master

# Finally, force update to the remote repository:
git push -f origin master
```

If this doesn't work, try the next method below.

### Second Method

Use with caution. Deleting the ".git" folder may cause problems.
```
# Clone the project, e.g. "myproject" is my project repository:
git clone << REPO_LINK >>

# Since all of the commits history are in the ".git" folder, we have to remove it:
cd myproject

# And delete the ".git" folder:
git rm -rf .git

# Now, re-initialize the repository:
git init
git remote add origin << REPO_LINK >>
git remote -v

# Add all the files and commit the changes:
git add --all
git commit -am "initial commit"

# Force push update to the master branch of our project repository:
git push -f origin master
```
