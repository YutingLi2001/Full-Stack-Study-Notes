# GitHub Branches
---
- The master branch stores the deployable code 
	- However, any branches can be used as the main finished deployable version of the code 
- Commit practices:
	- Don't end with a period
		- Describe details in the extended description 

# Cloning and Forking Github Projects
---
## Concepts
- Cloning
	- Creates a copy of a repository on your local machine
	- Cloned copies can sync between locations
- Forking
	- Modifies or extends a project without affecting the original project 

## Cloning Process
- Using terminal, type `git clone` and paste the URL of the repository  

## Syncing Local Changes
- Run the `git add <files>` command 
- Run `git commit -m <message>`
- Use `git push`

### Forking Process
- Click Fork button

## Syncing a Fork of a Project
- Create a local clone of the project 
- Configure Git to sync the fork
	- Open a terminal and change to the directory containing the clone
	- To access the remote repository, type `git. remote -v`
	- Type `git remote add upstream <clone directory>`
	- Confirm using `git remote -v`

# Managing Github Projects 
---
## Commonly used commands:
- `git pull` and `git-fetch` - from "origin" to keep up-to-date with the upstream

# All commands
---
- Fork: through Github page 
- Clone: `git clone <HTTPS>`
- Create branch: `git checkout -b <branch name>`
- Merge branches: `git merge <branch name>`
- Revert:
	- Check the log `git log --online`
	- Revert: `git revert <id>`
	- Revert to previous commit: `git revert HEAD`