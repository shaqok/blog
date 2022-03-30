---
title: "Writing a simple shell"
date: 2022-03-29T23:53:05-05:00
draft: false
categories:
- shell
tags:
- shell
- hugo
---

Hi! This would be my first blog post on this new setting. I do have some posts on my previous blog, but that'll take some time to migrate everything at once. I am probably going to update those whenever I'm available, so hope you enjoy my other posts later!

For this one, I wanted to share my first experience in writing a simple shell script that reduces your time whenever you try to push something to Github.
This came up especially when I was setting up this new blog, which I had to push different submodules every time to update the blog.
Instead, I decided to use a shell script that automates the process of adding, committing, and pushing in all the required repos.
Here' the code below:

```sh
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
# hugo -t <theme
hugo -t hugo-theme-console

# Go To Public folder, sub module commit
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push -f origin main

# Come Back up to the Project Root
cd ..

# blog repository Commit & Push
git add .

msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

git push -f origin main
```

The script is for updating my blog, and you can also write different scripts for different purposes.
For example, I have a repo that archives my solutions for leetcode problems. This process - making commits for each problems - is horribly tedious and repetitive. So, I wrote an even simpler shell script for automating the commit process:

```sh
# filename: solved.sh

# Print the statement
echo Enter the name of the problem you just solved:

# read the input "problem'
read problem

# regular git push process with the commit message "problem"
git add .

git commit -m "Solved $problem"

git push origin main
```

Now I just have to call `./solved.sh` and type the problem that I solved for the input. I didn't know about shell script, but this was surprisingly easy and useful way to make things much productive! Hope you guys enjoyed it, too!