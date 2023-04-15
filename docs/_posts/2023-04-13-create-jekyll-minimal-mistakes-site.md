---
layout: single
title: "Creating a new Jekyll site with minimal-mistakes theme"
date: 2023-04-13 22:10:00 +0000
categories: jekyll minimal-mistakes
---

## Starting from the scratch

### Prerequisite

* `Jekyll` and all required tools are installed for your operating system. See ["Jekyll Docs - Installation"](https://jekyllrb.com/docs/installation/) for detailed install instructions.
* `bundler` is installed.
* Alternatively, a development environment is set up according to the previous article ["Setting up the development environment from scratch"]({% link _posts/2023-04-12-github-pages-jekyll-devel-env.md %}#setting-up-the-development-environment-from-scratch) or ["Setting up the development environment using pre-configured `Vagrantfile`"]({% link _posts/2023-04-12-github-pages-jekyll-devel-env.md %}#setting-up-the-development-environment-using-pre-configured-vagrantfile).

### How-To

1. Create a new project directory for your new Jekyll site and move to the directory.

   ```
   $ mkdir <site name>
   $ cd <site name>
   ```

2. Create a `Gemfile` in the project root directory.

   There are two options: ["Gem-based method"](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#gem-based-method) or ["Remote theme method"](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#remote-theme-method) (preferred)

   NOTE: If you encounter "`cannot load such file -- webrick (LoadError)`" error, then add the below into `Gemfile` to resolve the issue.

   ```
   # Added to resolve an issue:
   # https://github.com/jekyll/jekyll/issues/8523
   gem "webrick"
   ```

3. Install `minimal-mistakes` theme and and its dependencies by running the following command.

   ```
   bundle install
   ```

4. Copy [`_config.yml`](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml) to the project root directory.

5. Select `theme` or `remote_theme` in `_config.yml`.

   * In case of "Remote theme method", add the following into `_config.yml`. At the time of writing, the latest version is 4.24.0. Please check the latest version when you configure it.

     ```
     remote_theme           : "mmistakes/minimal-mistakes@4.24.0"
     ```

   * In case of "Gem-based method", add the following into `_config.yml`.

     ```
     theme: minimal-mistakes-jekyll
     ```

6. Update the theme by running `bundle update`

7. Copy [`index.html`](https://github.com/mmistakes/minimal-mistakes/blob/master/index.html) to the project root directory.

8. Now you are ready to start your new Jekyll site on your local environment or on GitHub. Please see ["GitHub Pages - Setting up a GitHub Pages site with Jekyll"](https://docs.github.com/en/enterprise-server@3.4/pages/setting-up-a-github-pages-site-with-jekyll) for more details on how to publish your Jekyll site on GitHub or how to locally test your Jekyll site.

   NOTE: In case that your development environment is set up on the virtual machine, please see the previous article ["Local deployment"]({% link _posts/2023-04-12-github-pages-jekyll-minima.md %}#local-deployment).

   NOTE: If you are using `git`, it is recommended to create `.gitignore` file in the project root directory and add the followings:

   ```
   # ignore all files in _site directory
   _site/

   # ignore Gemfile.lock file
   Gemfile.lock
   ```

## Creating a new post

### How-To

1. Create a `_posts` directory in the project root directory.

   NOTE: The directory name must be exactly `_posts`.

2. Create a new post file in the `_posts` directory.

   All post files must begin with YAML Front Matter which is typically used to set a layout or other meta data as following.

   ```
   ---
   layout: single
   title: "Test"
   date: 2023-02-12 21:59:00 +0000
   categories: test
   ---

   A new post
   ```

   NOTE: The `layout` must be set to `single` instead of `post`, or completely removed. When removing the `layout` from the post file, please make it sure that the YAML Front Matter `defaults` section in `_config.yml` is properly configured for posts.

   NOTE: The post file name should comply with the predefined naming convention "`YYYY-MM-DD-<post title>.md`". See ["Jekyll Docs - Posts"](https://jekyllrb.com/docs/posts/) for more details.

   NOTE: The default permalink of the post is created based on the `categories` set in the YAML Front Matter and its file name (excluding the date). See ["Minimal-mistakes - Outputting"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#outputting) for more details.

   NOTE: Jekyll does not display posts with future date and time by default. See ["Jekyll - Issue #6536"](https://github.com/jekyll/jekyll/issues/6536) if you want to publish future posts.

3. Setting YAML Front Matter `defaults` section in `_config.yml`.

   Each post file can be individually configured with `layout` and other toggle settings (e.g., `author_profile`, `read_time`, `show_date`, `toc`). However, all posts can be configured with common settings by setting YAML Front Matter `defaults` section in `_config.yml` as followings. See ["Minimal-mistakes - Front Matter Defaults"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#front-matter-defaults) for more details.

   ```
   defaults:
     # _posts
     - scope:
         path: ""
         type: posts
       values:
         layout: single
         author_profile: true
         read_time: true
         comments: # true
         share: true
         related: true
   ```

## Creating a new page

### How-To

1. Create a `_pages` directory in the project root directory.

   NOTE: The directory name must be exactly `_pages`.

2. Create a new page file in the `_pages` directory.

   Similar to post files, all page files must begin with YAML Front Matter which is typically used to set a layout or other meta data as followings. The followings are copied from [`404.md`](https://github.com/mmistakes/minimal-mistakes/blob/master/docs/_pages/404.md) for custom 404 error page.

   ```
   ---
   layout: single
   title: "Page Not Found"
   excerpt: "Page not found. Your pixels are in another canvas."
   sitemap: false
   permalink: /404.html
   ---

   Sorry, but the page you were trying to view does not exist.
   ```

   NOTE: The `layout` must be set to `single` instead of `page`, or completely removed. When removing the `layout` from the page file, please make it sure that the YAML Front Matter `defaults` section in `_config.yml` is properly configured for pages.

3. Setting YAML Front Matter `defaults` section in `_config.yml`.

   Similar to posts, each page file can be individually configured with `layout` and other toggle settings. However, all pages can be configured with common settings by setting YAML Front Matter `defaults` section in `_config.yml` as followings. See ["Minimal-mistakes - Front Matter Defaults"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#front-matter-defaults) for more details.

   ```
   defaults:
     # _posts
     ...
     # _pages
     - scope:
         path: "_pages"
         type: pages
       values:
         layout: single
   ```

   NOTE: Please make it sure that `_pages` directory is added in `include` section in `_config.yml` as following. This tells `Jekyll` to read and process `_pages` directory.
   ```
   include:
     - _pages
   ```

## References

* [Minimal-mistakes - Starting Fresh](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/#starting-fresh)
* [Minimal-mistakes - Working with Posts](https://mmistakes.github.io/minimal-mistakes/docs/posts/)
* [Minimal-mistakes - Working with Pages](https://mmistakes.github.io/minimal-mistakes/docs/pages/)
* [Minimal-mistkaes - Minimal Mistakes remote theme starter](https://github.com/mmistakes/mm-github-pages-starter)
* [Jekyll Docs - Posts](https://jekyllrb.com/docs/posts/)
* [Jekyll Docs - Front Matter Defaults](https://jekyllrb.com/docs/configuration/front-matter-defaults/)
* [Jekyll Docs - Custom 404 Page](https://jekyllrb.com/tutorials/custom-404-page/)

