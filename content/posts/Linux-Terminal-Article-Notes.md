+++
tags = ['Linux', 'Bash']
title = 'How to Use the Terminal Like a Pro'
date = 2025-03-23T16:34:07+01:00
draft = false
+++

**Source:** [Command Line For Beginners](https://www.freecodecamp.org/news/command-line-for-beginners/)

## Shell:

A shell is a **program** that acts as command-line interpreter. It **processes commands** and **outputs the results**. It interprets and processes the commands entered by the user.

## Command line or CLI (command line interface):

The CLI is the interface in which we enter commands for the computer to process. In plain English once again, it's the space in which you enter the commands the computer will process.

![cli](https://cdn-media-0.freecodecamp.org/2022/03/terminal.png)

This is practically the same as the terminal and in my opinion these terms can be used interchangeably.

## Why should I even care about using the terminal?

The first reason is that for many tasks, it's just **more efficient**.

The second reason is that by using commands you can easily **automate tasks**.

The third reason is that sometimes the CLI will be the **only way** in which we'll be able to interact with a computer.

## Our first script

- First thing to do is create a `.sh` file. You can put it wherever want. I called mine `newGhRepo.sh`.
- Then open it on your text/code editor of choice.
- On our first line, we'll write the following: `#! /bin/sh`

```bash
#! /bin/bash
repoName=$1

while [ -z "$repoName" ]
do
   echo 'Provide a repository name'
   read -r -p $'Repository name:' repoName
done

echo "# $repoName" >> README.md
git init
git add .
git commit -m "First commit"

curl -u coccagerman https://api.github.com/user/repos -d '{"name": "'"$repoName"'", "private":false}'

GIT_URL=$(curl -H "Accept: application/vnd.github.v3+json" https://api.github.com/repos/coccagerman/"$repoName" | jq -r '.clone_url')

git branch -M main
git remote add origin $GIT_URL
git push -u origin main

```

- `repoName=$1` declaring a **variable** called repoName, and assigning it to the value of the first parameter the script receives.
- While loop is a **conditional** that keeps asking the user to enter the repo name until that parameter is received.
  - While the repoName variable is not assigned (while [ -z "$repoName" ])
  - Write to the console this message (echo 'Provide a repository name')
  - Then read whatever input the user provides and assign the input to the repoName variable (read -r -p $'Repository name:' repoName)
- Titling a md file, init, add, commit.
- **curl** is a command to transfer data from or to a server, using one of the many supported protocols.
  - And last we're using the -d flag to pass parameters to this command. In this case we're indicating the repository name (for which we're using our repoName variable) and setting private option to false, since we want our repo to be puiblic.
  - Lots of other config options are available in the API, so [check the docs](https://docs.github.com/en/rest/reference/repos#create-a-repository-for-the-authenticated-user) for more info.
- curl the Git_URL repository
- Finally, set main, set repository, sync

### Running Scripts

One option is to enter the shell name and pass the file as parameter, like: `dash ../ger/code/projects/scripts/newGhRepo.sh`.

And the other is to make the file **executable** by running `chmod u+x ../ger/code/projects/scripts/newGhRepo.sh`.

Then you can just execute the file directly by running `../ger/code/projects/scripts/newGhRepo.sh`.

#### bash aliases

To create a new alias, we need to edit the bash configuration files in our system. This files are normally located in the home directory. Aliases can be defined in different files (mainly .bashrc or .bash_aliases).

`alias newghrepo="dash /home/German/Desktop/ger/code/projects/scripts/newGhRepo.sh"`

- This maps `newghreop` to the .sh script

To find absolute path run: `readlink -f newGhRepo.sh`
