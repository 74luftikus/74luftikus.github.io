---
layout: single
title: "Customizing minimal-mistakes Jekyll theme (I)"
date: 2023-04-20 22:04:00 +0000
categories: jekyll minimal-mistakes
---

## Basic configuration

Here is a list of settings that have changed in `_config.yml` for this site. 

### Changing the skin

See ["Minimal-mistakes - Skin"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#skin) for more details.

```
minimal_mistakes_skin    : "dark"
```

### Setting the site title

By default, it will be shown in the masthead.
See ["Minimal-mistakes - Site title"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-title) for more details.

```
title                    : "Middle aged developer with a new dream"
```

### Setting the site sub-title

By default, it will be shown in the masthead together with the site title.
A slightly smaller font size is used for the sub-title.
See ["Minimal-mistakes - Site subtitle"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-subtitle) for more details.

```
subtitle                 : "새로운 꿈을 꿈꾸는 중년 개발자"
```

### Setting the site name

By default, it will be shown in the footer.
See ["Minimal-mistakes - Site name"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-name) for more details.

```
name                     : "Luftikus' Notepad"
```

### Setting the site description

It does not appear anywhere on the site.
See ["Minimal-mistakes - Site description"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-description) for more details.

```
description              : "This is where I organize what I have learned. If it helps others as well, then it is my pleasure."
```

### Setting the site URL

Since this site is being hosted by GitHub Pages, the site URL must be set to `https://<username>.github.io`.
See ["Minimal-mistakes - Site URL"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-url) for more details.

```
url                      : "https://74luftikus.github.io/"
```

### Setting the site repository

As for the site repository, `<GitHub username>/<repository-name>` must be set.
See ["Minimal-mistakes - Site repository"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-repository) for more details.

```
repository               : "74luftikus/74luftikus.github.io"
```

### Adding the logo

It will be shown in front of site title and sub-title in the masthead.
See ["Minimal-mistakes - Site masthead logo"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-masthead-logo) for more details.

```
logo                     : "/assets/images/luftikus-logo-dark-mode.png"
```

### Adding the site search

By default, it is disabled.
When it is enabled, a magnifying glass icon will appear at the end of masthead for site-wide search functionality.
See ["Minimal-mistakes - Site search"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#site-search) for more details.

```
search                   : true
```

### Adding the breadcrumb navigation

By default, it is disabled.
When it is enabled, a breadcrumb link will appear in each post.
See ["Minimal-mistakes - Breadcrumb navigation"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#breadcrumb-navigation-beta) for more details.

```
breadcrumbs              : true
```

NOTE: The default breadcrumb will be created based on the categories and title set in the YAML Front Matter of each post. For example, the breadcrumb of this post with two categories "`categories: jekyll minimal-mistakes`" and its title "`title: Customizing minimal-mistakes Jekyll theme (I)`" will be created as "`Home / Jekyll / Minimal mistakes / Customizing minimal-mistakes Jekyll theme (I)`".

### Adding the post dates

By default, it is disabled.
When it is enabled, a post date will appear for each post.

In order to enable the post dates, add "`show_date: true`" in YAML Front Matter `defaults` section in `_config.yml` or in each post file.
See ["Minimal-mistakes - Post dates"](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#post-dates) for more details.

```
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      ...
      show_date: true
```

NOTE: The default date format is "`%B %-d, %Y`", which will be displayed like "`February 21, 2023`".

NOTE: The date format is also configurable in `date_format` setting.

### Adding the table of contents

By default, it is disabled.
When it is enabled, auto-generated table of contents for your posts will be displayed on the right side of posts.

In order to enable the table of contents, add "`toc: true`" (optionally, "`toc_sticky: true`") into YAML Front Matter `defaults` section in `_config.yml` or in each post file.
Some other settings related to the table of contents are also available. See ["Minimal-mistakes - Table of contents"](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#table-of-contents) for more details.

```
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      ...
      toc: true
      toc_sticky: true
```

NOTE: Contiguous levels of headings must be used for generating the table of contents properly.

### Disabling the social sharing

By default, it is disabled. See ["Minimal-mistakes - Social sharing links"](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#social-sharing-links) for more details.

NOTE: If your `_config.yml` was copied from [`minimal-mistakes` repository](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml), then it might be already enabled. In order to disable the social sharing, remove "`share: true`" or set it to `false` in YAML Front Matter `defaults` section in `_config.yml`.

```
# Defaults
defaults:
  # _posts
  - scope:
      path: ""
      type: posts
    values:
      ...
      share: false
```

## References

* [Minimal-mistakes - Configuration](https://mmistakes.github.io/minimal-mistakes/docs/configuration)

