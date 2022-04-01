---
title: "Writing a Simple Shell 2"
date: 2022-04-01T00:06:53-05:00
draft: false
categories:
- shell
tags:
- bash
- shell
- hugo
---

Hi! I came back with another simple bash shell script for organizing the file directories. \
I was keep working on my leetcode practice as usual, and this time I got annoyed by creating a new directory for problem each time I solve.
My repository has a structure like below:

```
└── problem_type1
    ├── problem_1
    │   └── Problem.md
    │   └── problem_1.js
    ├── problem_2
    │   └── Problem.md
    │   └── problem_2.js
    │    
    problem_type2
    ├── problem_1
    │   └── Problem.md
    │   └── problem_1.js
    └── problem_2
        └── Problem.md
        └── problem_2.js
```

If I want to solve a problem, I have to create a `problem` directory under `problem_type` and then create `Problem.md` and `problem.js` under `problem`. Also, if `problem_type` doesn't exist, which means I want to solve a new type of problems, I have to add a `problem_type` directory first. And this is how it worked:


```sh
# Find the problem type
echo "Enter the type of the problem:"

# Show the list of the directories
ls -d */

# Read the input
read pType

if [ ! -d "$pType" ]; then
  # Control will enter here if $DIRECTORY doesn't exist.
  mkdir "$pType"
  echo "$pType folder is created"
fi

# # Print the statement
echo "Enter the name of the problem you want to solve:"

# Read the input "problem'
read problem

# Replace spaces with underscores
problem=${problem// /_}

# # Create a directory for the problem
mkdir "$pType/$problem"

# # Create problem.md and the js file.
touch "$pType/$problem/Problem.md"

touch "$pType/$problem/$problem.js"
```

Also, I forgot to mention in the previous post. Each time you create a script file and try to run it, you will encounter a message saying that the permission to execute the file is denied. To fix this, you just have to give permission to the file:

```
# +x grants permission to execute
chmod +x your_file
```

Now, I just have to type the name of the `problem_type` directory and the name of the `problem` that I am going to solve. Hope this helps!

