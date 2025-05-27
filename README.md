# 🐲 Hydra - Hugo Theme 🎨

Highly modified and customized version of the **Hugo theme [cactus](https://github.com/monkeyWzr/hugo-theme-cactus)** by **@monkeyWzr**, which is itself a fork from the **Hexo theme [cactus](https://github.com/probberechts/hexo-theme-cactus)** created by **@probberechts**.

The primary goal of this fork is to implement a "mini-blog" layout (internally called `category`), where multiple topics or "categories" can co-exist under the same URL (similar to the "sports" vs the "tech" section of a newspaper).

**Before:**
- www.blog.com/posts/aaa
- www.blog.com/posts/bbb
- www.blog.com/posts/ccc

**Now:**
- www.blog.com/tech/aaa
- www.blog.com/tech/bbb
- www.blog.com/art/ccc
- www.blog.com/art/eee
- www.blog.com/music/fff

> ⚠️ WARNING: This theme differs from the traditional Hugo blog layout! Most likely, your existing Hugo content will not render properly. Read more about this below.

> NOTE: You can read the original README [here](/README.old.md).

## Key Changes
The old blog layout was as follows:
```
[root]
├── ...
├── content
│   ├── posts
│   │   ├── aaa.md
│   │   ├── bbb.md
│   │   └── ccc.md
│   └── about.md
├── ...
└── hugo.toml
```

The new blog layout is as follows:
```
├── ...
├── content
│   ├── tech *
│   │   ├── _index.md * (new)
│   │   ├── aaa.md
│   │   ├── bbb.md
│   │   └── icon.png * (new, optional)
│   ├── art *
│   │   ├── _index.md * (new)
│   │   ├── ccc.md
│   │   ├── ddd.md
│   │   └── icon.png * (new, optional)
│   ├── music *
│   │   ├── _index.md * (new)
│   │   ├── eee.md
│   │   └── icon.png * (new, optional)
│   ├── posts.md * (new, optional)
│   └── about.md
├── ...
└── hugo.toml * (modified)
```

The primary change is the addition of the `_index.md` which dictates the metadata and specifies the rendering template for all following blog articles in the sub-folder.
```
+++
[cascade]
  layout = "post"
  category = "tech"
  categoryIcon = "fa-gears"
  categoryTitle = "Technology Articles"
  categoryDescription = "Articles about science, tech, and life. Curated for you."
  categoryHeaderLogo = "/tech/icon.png"
  categoryHeaderTitle = "Hydra Theme Demo"
  categoryHeaderSubtitle = "> Technology"
+++
```
- `layout = "post"` is required to select the post-specific rendering layout. 
- `category` field is required for determining the category name. 
- `categoryIcon` field is optional.
- `categoryTitle` field is optional. By default, it's the category name capitalized. (i.e. `tech` -> `Tech`)
- `categoryDescription` field is optional.
- `categoryHeaderLogo` changes the header logo if `enableBlogCategoryHeaders` is enabled in `[params]`.
- `categoryHeaderTitle` changes the header title if `enableBlogCategoryHeaders` is enabled in `[params]`.
- `categoryHeaderSubtitle` changes the header subtitle if `enableBlogCategoryHeaders` is enabled in `[params]`.

There are also some additional changes and new parameters to `hugo.toml`:
- `mainSections` has to list ALL the sections/categories in the blog. (by default only the first one is picked up)
- `displayCategories` parameter is optional. It dictates which categories to hotlink in the posts list.
- `enableBlogCategoryHeaders` parameter is optional. It enables or disables the custom per-category blog header.

Finally, you will need to create a `posts.md` file with the following content for `/posts` to work.
```
---
title: "Posts"
layout: "posts"  # Important!
---
```

> NOTE: The existing `categories` property no longer does anything! Category information is now inherited from the root `_index.md` file.

### Layout Changes
- Switched to an explicit `post.html` default layout
- Removed `categories` property (plural)
- Added `category` property (singular)
- Added `category name` to post list
- Added `displayCategories` section to home page rendering
- Fixed MathJax support
- Removed support for comments
- Removed justified gallery

### Theme Changes
- Changed colors and themes
- Adjusted SCSS/CSS styling
- Added blockquote formatting
- Added quote formatting
- Added customizable favicon
- Added hr bar to title
- Added global header across all blog pages
- Swapped default logo image to use placeholder image
- Disabled logo greyout
- Swapped `tags` page to use list format
- Added titles to `list` and `terms` layout
- Added customizable category icon

### Misc Changes
- Updated Hugo to 0.128.0
- Fixed `resources.ToCSS` deprecation
- Fixed Google Analytics
- Added Plausible Analytics
- Removed example site and GitHub workflows
- Removed unnecessary & deprecated libs
- Switched libs to use CDN
- Updated FontAwesome
- Moved `post-list` to `partial` layout
- Added default `post-list` rendering for post layout
- Added 404 Page

## Install

1. Add hydra as a git submodule to your Hugo site's `themes` folder.
```
git submodule add https://github.com/EdwardJXLi/hugo-theme-hydra.git themes/hydra
```

2. Change your theme to hydra in your site config
```toml
# config.toml

theme = "hydra"
```

3. Config your site. See [Config] or a [complete config sample](exampleSite/config.toml)
4. Test your site
```
hugo server
```

5. Publish your site in your preferred way. See Hugo's doc: [Hosting & Deployment](https://gohugo.io/hosting-and-deployment/)

## Config

### Color themes

```toml
[params]

  colortheme = "white" # dark, light, white, or classic
```

### Custom CSS

```toml
[params]
  css = ["css/custom.css"]
```

You can add multiple custom stylesheets which will be loaded after the main theme css.
For example, the above line will load the CSS-file placed at `/static/css/custom.css`.

### Navigation

```toml
# Main menu which appears below site header.
[[menu.main]]
name = "Home"
url = "/"
weight = 1

[[menu.main]]
name = "All posts"
url = "/posts"
weight = 2

[[menu.main]]
name = "Tags"
url = "/tags"
weight = 3

[[menu.main]]
name = "About"
url = "/about"
weight = 4
```

### Homepage settings

* description: description will be displayed in the homepage. Markdown syntax is supported in the description string.
```toml
[params]

  description = "Hugo is a general-purpose website framework. Technically speaking, Hugo is a static site generator. Unlike systems that dynamically build a page with each visitor request, Hugo builds pages when you create or update your content. Since websites are viewed far more often than they are edited, Hugo is designed to provide an optimal viewing experience for your website's end users and an ideal writing experience for website authors."
```

* Set your main section (used as the link for the "writings" title on the homepage)

```toml
[params]
  mainSection = "posts"
```

* Change the default main section title from Writings, to something else:

```toml
[params]
  mainSectionTitle = "Blog"
```

* Show only the 5 most recent posts (default)

```toml
[params]
  showAllPostsOnHomePage = false
  postsOnHomePage = 5
```
* Show all posts

```toml
[params]
  showAllPostsOnHomePage = true
  postsOnHomePage = 5 # this option will be ignored
```

* Show tags overview (default) or not
* 
```toml
[params]
  tagsOverview = true
```

* Display the table of contents inline on blog posts, rather than as part of the navigation menu:

```toml
[params]
  tocInline = true
```

* Show projects list (default) or not.

```toml
[params]
  showProjectsList = true
  projectsUrl = "https://github.com/monkeyWzr"
```

Projects section will not be shown if no data file is detected. See [Projects list](#projects-list) below.

### Projects list

Create your projects data file `data/projects.yaml|toml|json`. Hugo supports yaml, toml and json formats.
For former hexo cactus users: please assign your json array to a `list` key.

For example, `data/projects.json`:
```json
{
   "list": [
      {
         "name":"Hexo",
         "url":"https://hexo.io/",
         "desc":"A fast, simple & powerful blog framework"
      },
      {
         "name":"Font Awesome",
         "url":"http://fontawesome.io/",
         "desc":"The iconic font and CSS toolkit"
      }
   ]
}
```

### Social media links

```toml
[[params.social]]
  name = "github"
  link = "https://github.com/monkeyWzr"

[[params.social]]
  name = "email"
  link = "monkeywzr@gmail.com" # no need for "mailto:" at the start

[[params.social]]
  name = "linkedin"
  link = "https://www.linkedin.com/in/monkeywzr/"
```

The `name` key expects the name of a [Font Awesome icon](https://fontawesome.com/icons?d=gallery&s=brands).

### Copyright

Assign your copyright to `.Site.Copyright`. Cactus will append the current year to the head.

TODO: Customizable copyright year

```toml
copyright = "Zeran Wu" # cactus theme will use site title if copyright is not set
```

### Highlight

Use Hugo's built-in [syntax highlighting](https://gohugo.io/getting-started/configuration-markup#highlight).

Default config:

```toml
[markup]
  [markup.highlight]
    codeFences = true
    guessSyntax = false
    hl_Lines = ""
    lineNoStart = 1
    lineNos = false
    lineNumbersInTable = true
    noClasses = true
    style = "monokai"
    tabWidth = 4
```

### Analytics

Hydra uses Hugo's built-in analytics templates. Check [Hugo's documents](https://gohugo.io/templates/internal#google-analytics) for details.

Set your tracking id in your site config.
```toml
googleAnalytics = "UA-XXXXXXXX-XX" # or G-XXXXXXXX if you are using Google Analytics v4 (gtag.js)
```

If you are using Google Analytics v3 (analytics.js), you can switch to asynchronous tracking by setting `params.googleAnalyticsAsync` to `true`.
```toml
[params]
googleAnalyticsAsync = true # not required
```

### RSS

The RSS feed is not generated by default. You can enable it in your site config:

```toml
[params]
  rss = true
```

The RSS link will be `https://example.com/index.xml` assuming your `baseURL` is set to `https://example.com/`

Please also check [Configure RSS](https://gohugo.io/templates/rss/#configure-rss)

### Mathjax

Hydra supports mathjax. Just add the `mathjax` option in your site config:
```toml
[params]
  mathjax = true  # not required
```

You can also enable/disable mathjax per post. In your posts' front matter, add:
```yaml
mathjax: true # or false
```

The site config will be ignored when the `mathjax` option exists in front matter.

### Archive 
Pagination on posts archive can be disabled to show all posts in chronological order

```toml
[params]
  showAllPostsArchive = true # or false (default)
```
