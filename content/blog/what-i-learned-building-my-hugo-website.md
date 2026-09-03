+++
title = "What I Learned Building My Hugo Website"
date = "2026-08-20"
draft = false
+++

Building my personal website with Hugo and GitHub Pages was supposed to be a simple project. It turned out to be a useful hands-on exercise in understanding Hugo, Git, GitHub Actions, and the Apéro theme.

Along the way, I ran into a few problems. Here are the ones that were most useful to understand.

Hugo and the Apéro theme

One of the first lessons was that a Hugo theme is more than just a visual template.

The Apéro theme uses different layouts for different types of pages. The About page, Blog, CV, and Projects pages don't necessarily render content in the same way.

When the About page showed the title but not the content, looking at the actual theme layout helped explain what was happening.

The same thing happened with the CV. Using the standard page layout made the Markdown content render as expected.

Lesson: when Hugo behaves unexpectedly, look at the theme's layout files and understand how the page is being rendered.

The Blog 404

The individual blog post worked:

/blog/my-first-post/

But /blog/ returned a 404.

The problem was in the blog section's front matter. The _index.md file was still marked as a draft.

Changing:

draft = true

to:

draft = false

made the blog listing available.

I also changed the blog layout from the more elaborate Apéro sidebar layout to the simpler list layout because it suited the way I wanted to present my posts.

Git and SSH

Another important part of the project was setting up GitHub correctly.

Initially, GitHub rejected username/password authentication because password authentication is no longer supported for Git operations.

I already had SSH key files on my Mac, so I added the public key to GitHub and configured the repository to use the SSH remote.

After that, the normal workflow became straightforward:

git add .
git commit -m "Update website"
git push
The Hugo theme became a Git submodule

This was probably the most confusing Git problem.

The Apéro theme appeared in Git as:

160000 ... themes/hugo-apero

That meant Git was treating the theme as a submodule rather than as normal files.

GitHub Actions then failed with:

No url found for submodule path 'themes/hugo-apero' in .gitmodules

The solution was to remove the broken submodule reference and add the theme as regular files inside the repository.

After that, GitHub Actions could build the site normally.

The public directory

Hugo generates the public/ directory when the site is built.

I initially saw many generated HTML and XML files showing up in git status, which made it look like they needed to be committed.

They don't.

The generated public/ directory was added to .gitignore, allowing Git to track the Hugo source rather than the generated output.

GitHub Actions deployment

Once Git and the theme were configured correctly, deployment became pleasantly simple.

I make a change locally, test it with:

hugo server

Then:

git add .
git commit -m "Update website"
git push

GitHub Actions builds the Hugo site and publishes it to GitHub Pages.

The first few deployments helped me understand that a successful git push doesn't necessarily mean the website is immediately updated. The GitHub Actions workflow still needs to complete successfully.

The Apéro example configuration

The Apéro theme comes with example content and configuration.

Some of that configuration initially appeared on my site, including:

RStudio as the organisation name
"Anywhere" as the location
Example footer links
Example social links and settings

These were not Hugo problems. They were simply values inherited from the theme's example configuration.

Once I understood where they came from, cleaning them up was straightforward.

What I learned

The biggest lesson wasn't a particular Hugo command or Git configuration.

It was learning to investigate the structure behind the tools.

When something didn't work, looking at:

Hugo's generated output
hugo list
git status
git ls-files
the theme's layout files
GitHub Actions logs

usually gave me the answer.

The site is still simple, and there is plenty more I can improve. But building it myself gave me a much better understanding of how Hugo, Git, GitHub Pages, and GitHub Actions fit together.

And that's probably the most useful outcome of the project so far.
