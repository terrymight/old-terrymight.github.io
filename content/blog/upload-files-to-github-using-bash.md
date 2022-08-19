+++
title = "Upload Files TO Github Using Bash"
date = "2022-08-18T09:50:46+02:00"
tags = ["TERMINAL"]
categories = ["TERMINAL"]
description = "This time we would be using bash script to deploy files to github"
authors = ["Tejiri Mayone"]
banner = "/img/post/bash.jpg"

+++

## Introduction
Bash is a Unix shell and command language written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell.


A bash script is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line. 

### Requirement 

You need to have a bieginner knowledge on the following :

* Text editor for this tutorial we would using [Visual Studio Code](https://code.visualstudio.com)
* Terminal
* Git commands
* An account with [Gihub](https://github.com/)

### Procedure

Open your terminal and navigate to the root directory of your project

```
$ cd Documents/projects/bash
```

Now create a file called deploy.sh
```
$ touch deploy.sh
```

then open the file with [Visual Studio Code](https://code.visualstudio.com) editor. It should look like the img blow.


| ![space-1.jpg](/img/post/bash_screenshot.png) | 
|:--:| 
| *share my created bash file with .sh.* |


In the our `deploy.sh` file input the following code, I will explain what each line means what it does.

```
#!/bin/sh

# If a command fails then deploy stops

set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project. 
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`


# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site by $(whoami) $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin main
```

After you have added the code the script you are almost done at this stage. 

On you terminal type this

```
$ chmod +x deploy.sh 
```

After that run this.

```
./deploy.sh
```

At this point you will promoted to enter Git username and token 