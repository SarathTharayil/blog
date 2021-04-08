---
title: "Useful Hugo Commands"
date: 2021-04-09T01:39:36+05:30
toc: false
images:
tags:
  - tips
  - hugo
  - blogging
  - lookup
---

#### Hey I've just created this site and looks what it needs some content!

So, I'm adding some Hugo setup basics here just to make sure I dont forget about the process and seems like some of you might can take inspirations from it.

### Basic Installation

For the Windows users out there  
(Mac/Linux users chill please, I'll add when I revisit this one)

```
choco install hugo -confirm
```
Make sure you have Chocolatey installed. If no, run the below code in Powershell with admin rights
```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

If you want "extended" Sass/SCSS version, do 
```
choco install hugo-extended -confirm
```

#### We need some pre-requisites too
- [Git](https://git-scm.com/)
- [Go](https://golang.org/) (at least Go 1.11)


### Setting up new site
```
hugo new site <sitename>
```
To setup a theme, browse some Hugo themes, get one downloaded/cloned in your 'themes' directory. Then do
```
hugo -t <theme-name>
```
Then to view your site live locally, just do
```
hugo server
```
Isn't that cool, you can code the site and the site will be refreshed when you save your code changes!

Then something I did was adding a submodule to public directory of the site so that the static pages generated will be populated there and I need to have this site only added to the github pages repo to host this site!

### Adding submodule to public directory
- Make sure you have at least one commit on the main branch on the target repository before running this
```
git submodule add -b main YOUR_REPO_URL.git public
```

### Creating deployment script

So, to deploy the site everytime you make some changes or at any new posts, just run the script. Not tested personally but highly likely it would work :P

```
#!/bin/sh

# If a command fails then the deploy stops
set -e

printf "\033[0;32mDeploying updates to GitHub...\033[0m\n"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public

# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site $(date)"
if [ -n "$*" ]; then
	msg="$*"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin main
```

That's it. I'll add more if find something basic and usefull!



