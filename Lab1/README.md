# CSCI 3212 Lab 1
Guide by [AmCh-Q](https://github.com/AmCh-Q) on GitHub.

## Goals
1. Install Git, Python.
2. Create your own GitHub account and code repository.
3. Create your own ssh key and connect it to GitHub.
4. Learn how to use some Git commands, without using the web interface or desktop apps.

You might need 2-8 hours to complete this. Consider each section below a major goal!

If you have learned these before, just do the following:
1. Create a GitHub repository ``CSCI-3212``
2. Within it create a folder ``Lab1`` and a file ``README.md``, and write something in there.

## Install Git
You need this to learn how to maintain repository, where you will store your classworks.
1. Download and install from here: https://git-scm.com/install/
2. Open git bash and verify successful installation by running this command:
```bash
git --version
```
You should see something like "git version 2.55.0" -- The exact version don't matter.

## Install Python
You'd use Python for the class assignments.
1. Download and install from here: https://www.python.org/downloads/
2. Open git bash and verify successful installation:
```bash
python --version
```
You should see something like "Python 3.14.7" -- The exact version don't matter.

## Create your GitHub account

If you don't have a GitHub account yet, create one now: https://github.com/signup.

You don't have to use your school email, but we will assume you used your school email moving forward.

## Generate your own SSH key
https://docs.github.com/en/authentication/connecting-to-github-with-ssh/  
ssh keys are one way other people verify your identity, and we will use it so GitHub knows who you are.

Open Git bash run this to generate your ssh key:
```bash
ssh-keygen -t ed25519 -C "YourGitHubUserName@users.noreply.github.com" -f ~/.ssh/id_github
```
It will ask you to create a password. Then you should see ``id_github`` and ``id_github.pub`` at ``C:\Users\YourUserName\.ssh`` if you are using Windows.  
If you can't find it, see https://docs.github.com/en/authentication/connecting-to-github-with-ssh/checking-for-existing-ssh-keys

## Register your SSH private key
Your git doesn't recognize this new key yet, so you need to add it:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_github
```
It should ask you for the password you just created, then ``Identity added``.

## Upload your SSH public key to GitHub

An SSH key has two parts:  
``id_github``(with no suffix) is your private secret - **DO NOT give it to ANYONE**.  
If you read something like ``-----BEGIN OPENSSH PRIVATE KEY-----`` **STOP**.  
``id_github.pub`` is your public key - you will upload it to GitHub:

1. Log into GitHub
2. Open https://github.com/settings/ssh/new
3. Give it a title, then copy the content of your ``id_github.pub`` to the "Key" window. It should begin with something like ``ssh-ed25519`` and end with your email.
4. Click "add .ssh key"

Once you have done that, try:
```bash
ssh -T git@github.com
```
If it tells you ``You've successfully authenticated, but GitHub does not provide shell access.`` then success! GitHub can now recognize you from your ssh key.

## Create your class project folder
```bash
mkdir CSCI-3212
cd CSCI-3212
```
The first line creates a folder called "CSCI-3212" on your computer, and the second line move you into it.  
You will use this for your class projects.

## Create your Git Repository locally
```bash
git init
git config user.name "Your Full Name"
git config user.email "YourGitHubUserName@users.noreply.github.com"
```
This turns your folder into a git repository.

## Write something
Go inside ``CSCI-3212``, create a folder ``Lab1``.  
Go inside ``Lab1``, create a text file ``README.md``, write something in there.  
Write whatever you want, but know that **other people can see it** later.  
Alternatively, run the following commands:
```bash
mkdir Lab1
cd Lab1
echo "# CSCI-3212" >> README.md
```

## Commit it
```bash
git add README.md
git commit -m "Initial Commit"
```
The first line stages your file (prepares it to be committed).  
The second line commits it, and gives it a comment.  
This might feel tedious, but this is necessary for large group projects - each person make their own changes and periodically make a single, bulk commit, so that a team can more effectively track each person's contributions.

## Create a remote repository on GitHub
1. Go to https://github.com/ and login.
2. Click the ``+`` on the top right, then ``New Repository``
3. Use ``CSCI-3212`` as your repository name, don't change anything else.
4. Click ``Create Repository``

## Push your local repository to GitHub (remote)
1. Open https://github.com/YourUserName/CSCI-3212/
2. You should see a line saying ``Quick setup — if you’ve done this kind of thing before``
3. Right under it there's a "SSH" button, click it.
4. See the below option ``…or push an existing repository from the command line``
5. Do as it says inside Git Bash:
```bash
git remote add origin git@github.com:YourUserName/CSCI-3212.git
git branch -M main
git push -u origin main
```
It might ask you to confirm, enter ``yes``.  
Once your have done that, refresh your page https://github.com/YourUserName/CSCI-3212/, and you should now see your GitHub repository.

## You are done with the setup!

In the future, you can make any file edits inside the ``CSCI-3212`` folder, then run the following commands to commit your changes locally and push them to GitHub:
```bash
git add -A
git commit -am "Your commit message"
git push
``` 
1. The first line adds any file you've newly created (you can skip this if there are no new files).  
2. The second line commits all files locally; `a` here means ``commit all``, `m` means ``leave a message for the commit``.  
3. The third line pushes changes to remote (GitHub). 
Try making some changes then push again.  

Lastly, here are some useful resources:
1. Git Cheat Sheet: https://git-scm.com/cheat-sheet
2. gitignore: https://git-scm.com/docs/gitignore. This tells git to ignore some files, useful to avoid accidentally pushing junk or sensitive files - your GitHub repository is public, anyone can read your commits, and there are bad people out there.