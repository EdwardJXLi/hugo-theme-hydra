# 🐲 Hydra - Hugo Theme 🎨

Highly modified and customized version of the **Hugo theme [cactus](https://github.com/monkeyWzr/hugo-theme-cactus)** by **@monkeyWzr**, which is itself a fork from the **Hexo theme [cactus](https://github.com/probberechts/hexo-theme-cactus)** created by **@probberechts**.

The primary goal of this fork is to implement a "sub-blog" structure, where multiple topics or "categories" can co-under the same url.

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

> ⚠️ WARNING: This theme differs from the traditional Hugo blog layout! Most likely your existing Hugo content will not render properly. Read more about this below.

README is WIP. Please read the original README [here](/README.old.md).

## Key Changes

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

