---
layout: single
title: "Quick start for GitHub Pages using Vagrant (III)"
date: 2023-04-12 10:19:00 +0000
categories: quick-start github-pages jekyll devel-env vagrant
---

## Creating a new Jekyll site on the Ubuntu guest machine

### Prerequisite

* A development environment is already set up as described above, and working without any problem.

### Creating a new Jekyll site using Jekyll's default theme `minima`

1. Create a new directory for your new Jekyll site and move to the directory.

   ```
   $ mkdir <site name>
   $ cd <site name>
   ```

2. Create a new Jekyll site by executing the following:

   ```
   $ jekyll new --skip-bundle .
   ```

   NOTE: This command generates the followings:

   ```
   .
   ├── 404.html
   ├── about.markdown
   ├── _config.yml
   ├── Gemfile
   ├── .gitignore
   ├── index.markdown
   └── _posts
       └── 2023-03-05-welcome-to-jekyll.markdown
   ```

   NOTE: In order to make it run on GitHub Pages, `Gemfile` and `_config.yml` file need to be edited. See ["GitHub Docs - Creating a GitHub Pages site with Jekyll > Creating your site"](https://docs.github.com/en/pages/setting-up-a-github-pages-site-with-jekyll/creating-a-github-pages-site-with-jekyll#creating-your-site) for more details.


3. Add a new page and post according to ["Jekyll Docs - Pages"](https://jekyllrb.com/docs/pages/) and ["Jekyll Docs - Posts"](https://jekyllrb.com/docs/posts/).

   NOTE: Depending on Jekyll theme you use, there might be slightly differences. Please check documents of Jekyll theme you use.

### Local deployment

1. Locally deploying the new Jekyll site for testing by executing the following:

   ```
   $ bundle exec jekyll serve --host 0.0.0.0
   ```

   NOTE: The current development environment is set up on the vagrant Ubuntu guest machine. This means your new Jekyll site is running on your guest machine, but your browser might be running on the host machine. For this reason, Jekyll needs an additional option "`--host 0.0.0.0`" which allows Jekyll server to receive requests from any of system interfaces. Without this option, Jekyll server accepts requests ONLY from `localhost`.

   NOTE: If you encounter "`cannot load such file -- webrick (LoadError)`" error, then add the below into `Gemfile` to resolve the issue.

   ```
   # Added to resolve an issue:
   # https://github.com/jekyll/jekyll/issues/8523
   gem "webrick"
   ```

   NOTE: If you encounter a warning message "`GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.`", then add the below into `_config.yml` to resolve this issue. See ["GitHub Pages Ruby Gem - Issue #399"](https://github.com/github/pages-gem/issues/399) for more details.

   ```
   # Added to resolve an issue:
   # https://github.com/github/pages-gem/issues/399
   github: [metadata]
   ```

2. Now your new Jekyll site is accessible at `http://localhost:4000`.

## References

* [Jekyll Docs - Step by Step Tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)
* [Jekyll Docs - Configuration Options](https://jekyllrb.com/docs/configuration/options/#build-command-options)
* [Jekyll minima Theme](https://github.com/jekyll/minima)

