+++
title = "Building a Personal Website with Hugo and GitHub Pages"
date = "2026-08-20"
draft = false
+++

I wanted to build my own personal website while learning how Hugo, Git, GitHub, and GitHub Pages work together.

This is a practical step-by-step guide based on how I built this site.

### 1. Install Hugo

On macOS, install Hugo with Homebrew:

```bash
brew install hugo
```


Verify the installation:

```
hugo version
```

### 2. Create the Hugo site

Create a new Hugo site and move into the project directory:

```
hugo new site my-site
cd my-site
```

### 3. Add the Apéro theme

I chose the Apéro theme because it provides a clean starting point for a personal website while still allowing customization.

The theme provides layouts for pages such as About and Blog.

### 4. Configure the site

The main Hugo configuration is stored in hugo.toml.

The important settings include:

```
baseURL = "https://yourusername.github.io/"
title = "Your Name"
theme = "hugo-apero"
```

### 5. Create the homepage

The homepage content is stored in:

```
content/_index.md
```

For example:

```
+++
title = "Welcome to my homepage"
subtitle = "Your Name"
description = "Welcome to my personal website."
+++
```

### 6. Add your profile photo

Place your photo under the static directory:


```
static/
└── images/
    └── profile.png
```

Files in static/ are available directly from the website.

For example:

```
static/images/profile.png
```

becomes:

```
/images/profile.png
```

### 7. Create an About page

Create:


```
content/about/_index.md
```

The Apéro theme also provides a more structured About page if you want to customize the header, main content, sidebar, profile photo, and social links.

### 8. Create a CV
Create:
```
content/cv/_index.md
```
The CV can be written entirely in Markdown.
For example:
```
## Professional Experience

### Platform Architect – Posit Platform Modernization

**Client: Takeda, Switzerland · January 2026 – March 2026**
```
This makes the CV easy to maintain and update.
### 9. Create a Blog
Create the Blog section:
```
content/blog/
├── _index.md
└── my-first-post.md
```
A new post can be created with:
```
hugo new content blog/my-first-post.md
```
The post itself uses Markdown and Hugo front matter:
```
+++
title = "My First Post"
date = "2026-08-20"
draft = false
+++
```
### 10. Preview the website locally
Run:
```
hugo server
```
Then open:
```
http://localhost:1313/
```
Hugo automatically rebuilds the site when you make changes.
## Git & GitHub
### 11. Initialize Git
From the Hugo project directory:
```
git init
```
### 12. Configure your Git identity
Set your name and email:
```
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
This ensures commits have the correct author information.
### 13. Create the GitHub repository
Create a GitHub repository using the name:
```yourusername.github.io```
Then connect the local project:
```
git remote add origin git@github.com:yourusername/yourusername.github.io.git
```
Verify the remote:
```
git remote -v
```
### 14. Set up SSH authentication
GitHub no longer accepts account passwords for Git operations.
If you don't already have an SSH key, create one:
```
ssh-keygen -t ed25519
```
Add the public key to your GitHub account and test the connection:
```
ssh -T git@github.com
```
### 15. Commit and push
Add the files:
```
git add .
```
Create a commit:
```
git commit -m "Initial Hugo website"
```
Set the main branch:
```
git branch -M main
```
Push to GitHub:
```
git push -u origin main
```
## GitHub Pages & Deployment
### 16. Configure GitHub Actions
GitHub Actions can automatically build and deploy the Hugo website.
The workflow is stored under:
```
.github/
└── workflows/
   └── hugo.yaml
```
The workflow builds the Hugo site whenever changes are pushed to GitHub.
### 17. Publish the website
The deployment process looks like this:
```
Git push
  ↓
GitHub Actions
  ↓
Hugo build
  ↓
GitHub Pages
  ↓
https://yourusername.github.io/
```
Once the GitHub Actions workflow completes successfully, the website is published.
### 18. The everyday workflow
Once everything is configured, updating the website is simple:
```
hugo server
```
Make and test your changes locally.
Then:
```
git add .
git commit -m "Update website"
git push
```
GitHub Actions builds and publishes the updated website automatically.
## What's next?
This website is still a work in progress.
I'll continue adding projects, technical notes, and things I'm learning while gradually improving the site.
More to come!

Then save it and run:

```bash
hugo server
```
Check:
```
http://localhost:1313/blog/my-first-post/
```
And also:
```
http://localhost:1313/blog/
```

