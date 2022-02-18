# Workflow

## Owner of official repo sets up the project

See [initial-setup](/setup-docs/initial-setup.md)

## Set up Github forks (including Simon/organization owner)

### Create fork and set upstream to the official repo

1. Create a fork of this repo
2. Git clone your forked repo onto your machine
3. Add the official repo (this one) as the upstream of your forked repo on your computer.
```sh
git remote -v 
git remote add upstream <SSH link of the OFFICIAL REPO>
git remote -v (to verify if upstream is set to the official repo)
```

### Create a virtual environment

UNIX/Linux
1. Open a terminal (using bash or zsh) in Vscode
2. cd into the project folder if not done
3. Create a virtual environment with `python3 -m venv venv`
4. Activate the virtual environment with `source venv/bin/activate`. You should see `(venv)` on front of your shell prompt
5. Install python packages with `pip install -r requirements.txt``

Windows 

1. Open Vscode with `Git bash` as the default terminal profile
2. cd into the project folder if not done
3. Create a virtual environment with `python3 -m venv venv=`
4. Activate the virtual environment with `source venv/Scripts/activate`. You should see `(venv)` on front of your shell prompt
5. Install python packages with `pip install -r requirements.txt``

### Simon adds a remote to point to other team member's work to test PRs in their fork

```sh
git remote -v
git remote add <name + "fork"> <SSH link of the team member fork>
git remote -v
```

## Github workflow
    
### Code and PR

1. Create a branch and switch into it

```sh
git checkout -b <name of your branch>
```

2. Do your work

3. Add, commit, pull, and push your work to your branch on Github (it will create one if it's not made yet)

git add
```sh
git add <your files> or git  add .
```

git commit
```sh
git commit -m "Verb + what you did message"
```

git pull 
```sh
git pull upstream <branch> --rebase
```

git push
```sh
git push origin <name of your branch>
```

4. Submit a pull request 

### Test PR changes and merge them if they are good (Simon only)

1. Pull changes from original repo into my fork

```sh
git pull upstream
```

2. Grab changes from other forks

```sh
git fetch upstream pull/<id of PR>/head:<branch name>
````

3. Git checkout into the branch with the PR

```sh
git checkout <branch name>
```

4. Look at diffs

```sh
git diff
``` 

## Running Flask applications

1. Write the code
2. Open the terminal
3. Type `export FLASK_APP=app.py` to add the app to the path temporarily
4. Type `flask run` and open the link to check the website