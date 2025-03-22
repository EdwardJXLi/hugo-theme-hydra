# 🐲 Hydra - Hugo Theme 🎨

Highly modified and customized version of the **Hugo theme [cactus](https://github.com/monkeyWzr/hugo-theme-cactus)** by **@monkeyWzr**, which is itself a fork from the **Hexo theme [cactus](https://github.com/probberechts/hexo-theme-cactus)** created by **@probberechts**.

The primary goal of this fork is to implement a "mini-blog" layout (interally called `category`), where multiple topics or "categories" can co-exist under the same url. (similar to the "sports" vs the "tech" section of the newspaper)

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

README is WIP. Please read the original README [here](/README.old.md).

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
│   ├── tech *
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
  categoryHeaderLogo = "/tech/icon.png"
  categoryHeaderTitle = "Hydra Theme Demo"
  categoryHeaderSubtitle = "> Technology"
+++
```
- `layout = "post"` is required to select the post-specific rendering layout. 
- `category` field is required for determining the category name. 
- `categoryIcon` field is optional.
- `categoryTitle` field is optional. By default its the category name capitalized. (i.e. `tech` -> `Tech`)
- `categoryHeaderLogo` changes the header logo if `enableBlogCategoryHeaders` is enabled in `[params]`.
- `categoryHeaderLogo` changes the header title if `enableBlogCategoryHeaders` is enabled in `[params]`.
- `categoryHeaderLogo` changes the header subtitle if `enableBlogCategoryHeaders` is enabled in `[params]`.

There also some additional changes and new parameters to `hugo.toml`:
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

### Theme Changes
- Changed colors and themes
- Adjusted SCSS/CSS styling
- Added hr bar to title
- Added global header across all blog pages
- Swaped default logo image to use placeholder image
- Disabled logo greyout
- Swapped `tags` page to use list format
- Added titles to `list` and `terms` layout
- Added customizable category icon

### Misc Changes
- Fixed `resources.ToCSS` deprecation
- Fixed Google Analytics
- Removed example site and github workflows
- Updated FontAwesome
- Moved `post-list` to `partial` layout
- Added default `post-list` rendering for post layout
- Added 404 Page

