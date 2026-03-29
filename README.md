# re-Terminal

A simple, retro terminal-style Jekyll theme.

![re-Terminal](https://github.com/mirus-ua/hugo-theme-re-terminal/blob/main/images/screenshot.png?raw=true)

---

- [Features](#features)
- [Requirements](#requirements)
- [Quick Start](#quick-start)
- [Configuration](#configuration)
- [Creating Content](#creating-content)
- [Customization](#customization)
- [Color Themes](#color-themes)

---

## Features

- **7 color themes** — blue (default), red, orange, green, pink, paper, gooey
- [**Fira Code**](https://github.com/tonsky/FiraCode) as default monospaced font
- **Duotone syntax highlighting** via [PrismJS](https://prismjs.com)
- Fully responsive
- Pagination, tag archives, RSS feed
- Optional table of contents, reading time, cover images with captions
- Banner / call-to-action bar
- Drop-down navigation menus
- Per-page color override
- Light themes: `paper` and `gooey`

---

## Requirements

- Ruby 3.x
- Jekyll 4.3+

---

## Quick Start

1. Add to your `Gemfile`:

   ```ruby
   gem "jekyll", "~> 4.3"
   gem "jekyll-paginate"
   gem "jekyll-feed"
   gem "jekyll-seo-tag"
   gem "jekyll-archives"
   ```

2. Install:

   ```bash
   bundle install
   ```

3. Serve locally:

   ```bash
   bundle exec jekyll serve
   ```

4. Build for production:

   ```bash
   bundle exec jekyll build
   ```

---

## Configuration

Edit `_config.yml`. All options with their defaults:

```yaml
# Site
title: re-Terminal
description: A simple, retro theme for Jekyll
baseurl: ""
url: ""
lang: en

# Theme
theme_color: blue        # blue | green | orange | pink | red | paper | gooey
logo_text: re-Terminal
logo_home_link: /
subtitle: A simple, retro theme for Jekyll
keywords: ""
copyright: ""            # custom footer copyright HTML; omit for default

# Layout
center_theme: true       # center the content column
full_width_theme: false  # full-width layout
one_heading_size: true   # uniform heading sizes

# Posts
reading_time: true       # show reading time on posts
show_last_updated: false # show "Updated" date
updated_date_prefix: "Updated"
minute_reading_time: "min read"
words: "words"
read_more: "Read more"
read_other_posts: "Read other posts"
newer_posts: "Newer posts"
older_posts: "Older posts"

# Navigation
show_menu_items: 3       # items shown before "Show more" overflow
menu_more: "Show more"
nav:
  - name: About
    url: /about/
  - name: Showcase
    url: /showcase/
  # Sub-menus:
  # - name: More
  #   children:
  #     - name: Tags
  #       url: /tags/
  #     - name: Some Page
  #       url: /some-page/
  #       new_tab: true

# 404 page
missing_content_message: "Page not found..."
missing_back_button_label: "Back to home page"

# Table of contents
toc: false
toc_title: "Table of Contents"

# Banner (optional)
# banner:
#   text: "Check it out on GitHub"
#   url: "https://github.com/halfsohappy/hugo-theme-re-terminal"
#   dismissible: false

# Twitter / X card (optional)
# twitter:
#   site: "@yoursite"
#   creator: "@yourcreator"

# Google Analytics (optional)
# google_analytics: G-XXXXXXXXXX

# Favicon (optional — defaults to theme-color icon)
# favicon: /img/favicon.png

# Pagination
paginate: 5
paginate_path: "/page/:num/"

plugins:
  - jekyll-paginate
  - jekyll-feed
  - jekyll-seo-tag
  - jekyll-archives

jekyll-archives:
  enabled: [tags, categories]
  layout: tag
  permalinks:
    tag: /tags/:name/
    category: /categories/:name/
```

---

## Creating Content

### Posts

Create files in `_posts/` named `YYYY-MM-DD-title.md`:

```markdown
---
layout: post
title: "My Post Title"
date: 2024-01-01
author: Your Name
cover: /img/my-cover.jpg
cover_caption: "Optional caption for the cover image"
cover_credit: "Photographer Name"
description: "Short description for list view and SEO"
tags: [tag1, tag2]
keywords: [keyword1, keyword2]
show_full_content: false   # show full post body on list pages
reading_time: true         # override site-level reading_time
hide_comments: false
toc: false                 # table of contents
toc_title: "Contents"
color: ""                  # per-page color override (e.g. "pink")
noindex: false
---

Post content here...
```

### Pages

Create files in `_pages/` with a `permalink`:

```markdown
---
layout: page
title: About
permalink: /about/
---

Page content here...
```

### Home page

`index.html` uses the `home` layout with the paginator:

```html
---
layout: home
title: re-Terminal
---
```

Optional intro content placed above the post list:

```html
---
layout: home
title: re-Terminal
framed: true
---

Welcome to my site!
```

### Tags page

Create `_pages/tags.md`:

```markdown
---
layout: tags
title: Tags
permalink: /tags/
---
```

---

## Customization

### Custom CSS

Create `assets/style.css` in your site to override CSS variables:

```css
:root {
  --accent: #ff6600;
  --accent-contrast-color: white;
}
```

All available variables (with dark-theme defaults):

```css
:root {
  --accent: #23B0FF;
  --accent-contrast-color: black;
  --background: color-mix(in srgb, var(--accent) 2%, #1D1E28 98%);
  --color: white;
  --border-color: rgba(255, 255, 255, 0.1);
  --menu-color: white;

  /* Syntax highlighting */
  --syntax-func-color: ...;
  --syntax-var-color: ...;
  --syntax-value-color: ...;
  /* see _sass/_variables.scss for the full list */
}
```

### Comments

Override `_includes/comments.html` in your own site:

```html
<!-- _includes/comments.html -->
{% if site.disqus.shortname %}
  <div id="disqus_thread"></div>
  <script>
    var disqus_config = function() {
      this.page.url = '{{ page.url | absolute_url }}';
      this.page.identifier = '{{ page.url }}';
    };
    (function() {
      var d = document, s = d.createElement('script');
      s.src = 'https://{{ site.disqus.shortname }}.disqus.com/embed.js';
      s.setAttribute('data-timestamp', +new Date());
      (d.head || d.body).appendChild(s);
    })();
  </script>
{% endif %}
```

### Extended head / footer

Override `_includes/extended-head.html` or `_includes/extended-footer.html` to inject content into `<head>` or before `</body>`.

### Includes for shortcode-style embeds

Use Jekyll `{% include %}` tags as shortcode equivalents:

| Purpose | Usage |
|---|---|
| Figure with caption | `{% include figure.html src="/img/photo.jpg" caption="My caption" position="center" %}` |
| Inline image | `{% include image.html src="/img/photo.jpg" alt="Alt text" position="left" %}` |
| Collapsible code | `{% include code.html language="js" title="app.js" content=some_var %}` |

Create `_includes/figure.html`, `_includes/image.html`, etc. in your site to implement these.

---

## Color Themes

| Name | Accent | Style |
|------|--------|-------|
| `blue` (default) | `#23b0ff` | dark |
| `green` | `#78e2a0` | dark |
| `orange` | `#ffa86a` | dark |
| `pink` | `#ee72f1` | dark |
| `red` | `#ff6266` | dark |
| `paper` | `#1d1e28` | light |
| `gooey` | `#90849c` | light — from [theaterGWD/gooey](https://github.com/halfsohappy/TheaterGWD) |

Set in `_config.yml`:

```yaml
theme_color: gooey
```

Or override per-page:

```yaml
---
color: pink
---
```

---

## License

[MIT](LICENSE.md)
