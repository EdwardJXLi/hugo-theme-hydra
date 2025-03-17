# 🐲 Hydra - Hugo Theme 🎨

Highly modified and customized version of the Hugo theme [cactus](https://github.com/monkeyWzr/hugo-theme-cactus) by @monkeyWzr, which is itself a fork from the Hexo theme [cactus](https://github.com/probberechts/hexo-theme-cactus) created by @probberechts.

The primary goal of this fork is to introduce a "sub-blog" structure, where multiple topics or "categories" can co-under the same url.

**Before:**
- www.blog.com/posts/thing1
- www.blog.com/posts/thing2
- www.blog.com/posts/thing2.1

**Now:**
- www.blog.com/tech/thing1
- www.blog.com/art/thing2
- www.blog.com/art/thing2.1

> ⚠️ WARNING: This theme differs from the traditional Hugo blog layout! Most likely your existing Hugo content will not render properly. Read more about this below.

README is WIP. Please read the original README [here](/README.old.md).

## Key Changes
TODO

## Misc Changes
- Changes colors and themes
- Made post layout an explicit `post.html` default layout
- Removed example site and github workflows
- Fix `resources.ToCSS` deprecation
- Fix Google Analytics
- Disabled logo greyout
- Swap logo image to use placeholder image
- Made header global across all blog pages
- Swapped tags page to use list format
- Remove "Categories" property (plural)
- Added "Category" property (singular)
- Update FontAwesome
- Customizable category icon
- Move post-list to partial layout
- Added default post-list rendering for post layout
- Add titles to list and terms layout
