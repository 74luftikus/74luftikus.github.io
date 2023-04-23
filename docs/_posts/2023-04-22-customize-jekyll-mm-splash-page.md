---
layout: single
title: "Customizing minimal-mistakes Jekyll theme (II)"
date: 2023-04-22 22:41:00 +0000
categories: jekyll minimal-mistakes
---

## Creating a landing page with a splash page layout

### How-To

1. Create `_pages` directory in the project root directory if it does not exist.

2. Create a new page file (e.g., `home.md`) with the following YAML Front Matter in `_pages` directory.

   ```
   ---
   title: "Dreams are the seedlings of reality"
   layout: splash
   permalink: /
   excerpt: "Napoleon Hill 'Think and Grow Rich'"
   header:
     overlay_color: "#6C757D"
   ---
   ```

   * `title` : Depending on the header overlay configuration, a header image or solid background color is overlaid with the title. This page is configured to use a solid background color.
   * `layout` : It must be set to `splash` in order to apply a splash page layout to the corresponding page.
   * `permalink` : In order to set this page as a landing page, it must be set to "`/`".
   * `excerpt` : Similar to `title`, a header image or solid background color is overlaid with the excerpt. A slightly smaller font size is used for `excerpt`.
   * `header`: It displays a large full-width header image or solid background color. See ["Minimal-mistakes - Headers"](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#headers) or ["Minimal-mistakes - Header overlay"](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#header-overlay) for more details.

3. Delete `index.html` or `index.md` file from the project root directory if it exists.

   NOTE: Make sure that none of them exist in the project root directory. Otherwise, the landing page will not be replaced by your new page created with a splash page layout.

   NOTE: If your `_config.yml` was copied from [`minimal-mistakes` repository](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml), then you might encounter the following warning message during the local deployment:

   ```
   Pagination: Pagination is enabled, but I couldn't find an index.html page to use as the pagination template. Skipping pagination.
   ```

   This occurs because `jekyll-paginate` plugin is enabled with `paginate` and `paginate_path` settings, but it only works on files with name `index.html` which is deleted at this step.
   You can simply ignore the warning message, or disable `paginate` and `paginate_path` settings in `_config.yml`. See [Minimal-mistakes - Paginate](https://mmistakes.github.io/minimal-mistakes/docs/configuration/#paginate) for more details.


## Displaying archive posts in the landing page using a grid view 

### How-To

1. Add the followings after YAML Front Matter in the new page file (e.g., `home.md`) created above.

   <!-- Below {% raw %} / {% endraw %} is an escape method for Liquid tags
        See https://talk.jekyllrb.com/t/how-to-escape-in-markdown/4173
        for more details.
   -->
  
   ```
   <div class="grid__wrapper">
     {% raw %}
     {% for post in site.posts limit:8 %}
       {% include archive-single.html type="grid" %}
     {% endfor %}
     {% endraw %}
   </div>
   ```

2. The above sets to display at most 8 posts on the landing page. If you want to change the maximum number of posts displayed on the landing page, change "`limit:8`".


## References

* [Minimal-mistakes - Splash page layout](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#splash-page-layout)
* [Minimal-mistakes - Headers](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#headers)
* [Minimal-mistakes - Header overlay](https://mmistakes.github.io/minimal-mistakes/docs/layouts/#header-overlay)
* [Minimal-mistakes - Feature row](https://mmistakes.github.io/minimal-mistakes/docs/helpers/#feature-row)
* [Minimal-mistakes - Issue #1251](https://github.com/mmistakes/minimal-mistakes/issues/1251)


