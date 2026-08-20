+++
title = "Setting Up Git and SSH for GitHub"
date = "2026-08-20"
draft = false
+++

Once my Hugo website was working locally, I wanted to put it under Git version control and publish it to GitHub.

This is the setup I used for my personal website.

## 1. Initialize Git

From the Hugo project directory:

`git init`

Check the repository:

`git status`

## 2. Configure Git

Set the name and email that Git will use for commits:

`git config --global user.name "Your Name"`

`git config --global user.email "your-email@example.com"`

This avoids Git automatically assigning an identity based on your computer name.

## 3. Create the GitHub repository

I created a new GitHub repository for the website:

`yourusername.github.io`

For a personal GitHub Pages website, this repository name is important because GitHub uses it to identify the personal site.

## 4. Set up SSH

GitHub does not support password authentication for Git operations.

I created an SSH key:

`ssh-keygen -t ed25519`

This creates a private key and a public key.

The public key normally ends with `.pub`.

Display the public key with:

`cat ~/.ssh/id_ed25519.pub`

I then added the public key to my GitHub account under SSH and GPG keys.

The private key stays on my computer and should never be shared.

## 5. Test SSH

Test the connection:

`ssh -T git@github.com`

If the SSH configuration is correct, GitHub confirms that authentication was successful.

## 6. Connect the local project to GitHub

From the Hugo project directory:

`git remote add origin git@github.com:yourusername/yourusername.github.io.git`

Check the connection:

`git remote -v`

## 7. Create the first commit

Add the website files:

`git add .`

Create the commit:

`git commit -m "Initial Hugo website"`

Set the main branch:

`git branch -M main`

## 8. Push to GitHub

Push the project:

`git push -u origin main`

The Hugo project should now appear in the GitHub repository.

## 9. A Git authentication problem I encountered

Initially, GitHub returned an error saying:

"Password authentication is not supported for Git operations."

The problem was that Git was trying to use password-based authentication.

The solution was to use the SSH repository URL:

`git remote set-url origin git@github.com:yourusername/yourusername.github.io.git`

After that, `git push` worked successfully.

## 10. The everyday workflow

Once Git and SSH are configured, updating the website is simple.

First test the website locally:

`hugo server`

Then check what changed:

`git status`

Add the changes:

`git add .`

Commit:

`git commit -m "Update website"`

Push:

`git push`

GitHub Actions can then build and deploy the updated Hugo website automatically.

## What I learned

The setup consists of several pieces working together:

Hugo → Git → SSH → GitHub → GitHub Actions → GitHub Pages → Live website

The initial setup takes a little time, but after that the publishing workflow is very simple:

`git add .`

`git commit -m "Update website"`

`git push`

That is now the workflow I use to maintain this website.
