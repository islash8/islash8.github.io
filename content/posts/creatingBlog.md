---
title: "The creation of a blog!"
date: 2023-03-05T21:47:01+01:00
draft: false
tags: ["tots"]
---

This is a tutorial about how this thing is done maybe it would be useful for someone.

**Quick Introduction**

Hugo is a fast and flexible static site generator, perfect for building blogs and websites. When paired with GitHub Pages, it becomes even more powerful, enabling easy version control and free hosting. In this guide, we will walk through the process of creating a blog using Hugo and deploying it on GitHub Pages.

All of what I am going to mention here in the post can be found in giraffe academy hugo crash course on youtube, you can find it [here](https://www.youtube.com/watch?v=qtIqKaDlqXo&list=PLLAZ4kZ9dFpOnyRlyS-liKL5ReHDcj4G3), So I would highly recommend to check it out too, it would help us understand better and how to deal with static site generators.

**Prerequisites:**

Basic knowledge of Git and GitHub
Hugo installed on your local machine (https://gohugo.io/getting-started/installing/)

## Step 1: Creating a New Hugo Site

Open your command prompt or terminal, and navigate to a directory where you want to create your new blog.
Run the following command to create a new Hugo site:
``` bash
hugo new site my-blog
#Replace "my-blog" with the desired name for your blog.
```

## Step 2: Adding a Theme

Browse the Hugo themes at https://themes.gohugo.io/ and choose one you like.
Once you've chosen a theme, clone its repository into the themes directory of your new Hugo site:
```bash
cd my-blog/themes
git clone <theme-repo-url>
# Edit the config.toml file in the root of your new site, and add the following line to set the theme:
```

```toml
theme = "<theme-name>"
```

## Step 3: Adding Content

To create a new blog post, run:
```bash 
hugo new posts/my-first-post.md
# Edit the newly created markdown file in the content/posts directory, and start writing your blog post.
# Save your changes and preview your site by running:
hugo server -D
```
Visit http://localhost:1313 to see your blog in action.

## Step 4: Setting Up a GitHub Repository

Go to https://github.com/new and create a new repository named <your-github-username>.github.io. 
_Replace <your-github-username> with your GitHub username._
On your local machine, navigate to the root directory of your Hugo site and initialize a new Git repository:
```bash
git init
# Add all files, commit your changes, and link your local repository to the GitHub repository:

git add .
git commit -m "Initial commit"
git remote add origin https://github.com/<your-github-username>/<your-github-username>.github.io.git
git branch -M main
git push -u origin main
```

## Step 5: Deploying Your Blog with GitHub Pages

In the root directory of your Hugo site, create a new .github/workflows folder:
```bash
mkdir -p .github/workflows
```
```yaml
#Create a new YAML file called gh-pages.yml inside the .github/workflows directory and add the following content:

name: GitHub Pages

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v2
      with:
        submodules: true

    - name: Setup Hugo
      uses: peaceiris/actions-hugo@v2
      with:
        hugo-version: 'latest'

    - name: Build
      run: hugo --minify

    - name: Deploy
      uses: peaceiris/actions-gh-pages@v3
      with:
        github_token: ${{ secrets.GITHUB_TOKEN }}
        publish_dir: ./public
        user_name: 'GitHub Actions'
        user_email: 'github-actions[bot]@users.noreply.github.com'
        cname: '<your-custom-domain>'
```

_Replace `<your-custom-domain>` with your custom domain if you have one. If you don't have a custom domain, simply remove the `cname` line._

## Commit and push the changes to the GitHub repository:

```bash
git add .
git commit -m "Add GitHub Pages deployment workflow"
git push
```

The GitHub Actions workflow will automatically build and deploy your Hugo blog to GitHub Pages. You can check the progress in the "Actions" tab of your repository.

Once the deployment is complete, visit `https://<your-github-username>.github.io` to see your live blog. If you set up a custom domain, visit your custom domain instead.


__Finally:__
Congratulations! You have successfully created a blog using Hugo and deployed it on GitHub Pages. Now you can focus on writing great content, knowing that your site is being automatically built and deployed with every push to the `main` branch. Don't forget to explore the many features and customization options that Hugo and GitHub Pages offer to create a unique and engaging blogging experience.