# Hugo Book Theme

[![Hugo](https://img.shields.io/badge/hugo-0.65-blue.svg)](https://gohugo.io)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

### [Hugo](https://gohugo.io) documentation theme as simple as plain book

![Screenshot](https://github.com/alex-shpak/hugo-book/blob/master/images/screenshot.png)

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Menu](#menu)
- [Blog](#blog)
- [Configuration](#configuration)
- [Shortcodes](#shortcodes)
- [Versioning](#versioning)
- [Contributing](#contributing)

## Features

- Clean simple design
- Light and Mobile-Friendly
- Multi-language support
- Customisable
- Zero initial configuration
- Handy shortcodes
- Comments support
- Simple blog and taxonomy
- Primary features work without JavaScript
- Dark Mode

## Requirements

- Hugo 0.65 or higher
- Hugo extended version, read more [here](https://gohugo.io/news/0.48-relnotes/)

## Installation

Navigate to your hugo project root and run:

```
git submodule add https://github.com/alex-shpak/hugo-book themes/book
```

Then run hugo (or set `theme = "book"`/`theme: book` in configuration file)

```
hugo server --minify --theme book
```

### Creating site from scratch

Below is example how to create new site from scratch

```sh
hugo new site mydocs; cd mydocs
git init
git submodule add https://github.com/alex-shpak/hugo-book themes/book
cp -R themes/book/exampleSite/content .
```

```sh
hugo server --minify --theme book
```

## Menu

### File tree menu (default)

By default theme will render pages from `content/docs` section as menu in a tree structure.  
You can set `title` and `weight` in front matter of pages to adjust order and titles in menu.

### Leaf bundle menu

You can also use leaf bundle and content of it's `index.md` as menu.  
Given you have this file structure

```
├── content
│   ├── docs
│   │   ├── page-one.md
│   │   └── page-two.md
│   └── posts
│       ├── post-one.md
│       └── post-two.md
```

Create file `content/docs/menu/index.md` with content

```md
+++
headless = true
+++

- [Book Example]({{< relref "/docs/" >}})
  - [Page One]({{< relref "/docs/page-one" >}})
  - [Page Two]({{< relref "/docs/page-two" >}})
- [Blog]({{< relref "/posts" >}})
```

And Enable it by settings `BookMenuBundle: /menu` in Site configuration

- [Example menu](https://github.com/alex-shpak/hugo-book/blob/master/exampleSite/content/menu/index.md)
- [Example config file](https://github.com/alex-shpak/hugo-book/blob/master/exampleSite/config.yaml)
- [Leaf bundles](https://gohugo.io/content-management/page-bundles/)

## Blog

Simple blog supported for section `posts`.  
Blog is not primary use case so book theme so it has only minimal features

## Configuration

### Site Configuration

There are few configuration options you can add to your `config.toml` file.  
You can also see `yaml` example [here](https://github.com/alex-shpak/hugo-book/blob/master/exampleSite/config.yaml).

```toml
# (Optional) Set Google Analytics if you use it to track your website.
# Always put it on the top of the configuration file, otherwise it won't work
googleAnalytics = "UA-XXXXXXXXX-X"

# (Optional) If you provide a Disqus shortname, comments will be enabled on
# all pages.
disqusShortname = "my-site"

# (Optional) Set this to true if you use capital letters in file names
disablePathToLower = true

# (Optional) Set this to true to enable 'Last Modified by' date and git author
#  information on 'doc' type pages.
enableGitInfo = true

# (Optional) Theme is intended for documentation use, therefore it doesn't render taxonomy.
# You can remove related files with config below
disableKinds = ['taxonomy', 'taxonomyTerm']
  
[params]
  # (Optional, default true) Controls table of contents visibility on right side of pages.
  # Start and end levels can be controlled with markup.tableOfContents setting.
  # You can also specify this parameter per page in front matter.
  BookToC = true
  
  # (Optional, default none) Set the path to a logo for the book. If the logo is
  # /static/logo.png then the path would be 'logo.png'
  BookLogo = 'logo.png'
  
  # (Optional, default none) Set leaf bundle to render as side menu
  # When not specified file structure and weights will be used
  BookMenuBundle = '/menu'
  
  # (Optional, default docs) Specify section of content to render as menu
  # You can also set value to "*" to render all sections to menu
  BookSection = 'docs'
  
  # Set source repository location.
  # Used for 'Last Modified' and 'Edit this page' links.
  BookRepo = 'https://github.com/alex-shpak/hugo-book'
  
  # Enable 'Edit this page' links for 'doc' page type.
  # Disabled by default. Uncomment to enable. Requires 'BookRepo' param.
  # Path must point to 'content' directory of repo.
  BookEditPath = 'edit/master/exampleSite/content'
  
  # (Optional, default January 2, 2006) Configure the date format used on the pages
  # - In git information
  # - In blog posts
  BookDateFormat = 'Jan 2, 2006'
  
  # (Optional, default true) Enables search function with flexsearch,
  # Index is built on fly, therefore it might slowdown your website.
  # Configuration for indexing can be adjusted in i18n folder per language.
  BookSearch = true

  # (Optional, default true) Enables comments template on pages
  # By default partals/docs/comments.html includes Disqus template
  # See https://gohugo.io/content-management/comments/#configure-disqus
  # Can be overwritten by same param in page frontmatter
  BookComments = true

  # /!\ This is an experimental feature, might be removed or changed at any time
  # (Optional, experimental, default false) Enables portable links and link checks in markdown pages.
  # Portable links meant to work with text editors and let you write markdown without {{< relref >}} shortcode
  # Theme will print warning if page referenced in markdown does not exists.
  BookPortableLinks = true
```

### Multi-Language Support
Theme supports Hugo's [multilingual mode](https://gohugo.io/content-management/multilingual/), just follow configuration guide there. You can also tweak search indexing configuration per language in `i18n` folder.

### Page Configuration

You can specify additional params per page in front matter

```toml
# Set type to 'docs' if you want to render page outside of configured section or if you render section other than 'docs'
type = 'docs'

# Set page weight to re-arrange items in file-tree menu (if BookMenuBundle not set)
weight = 10

# (Optional) Set to mark page as flat section in file-tree menu (if BookMenuBundle not set)
bookFlatSection = true

# (Optional, Experimental) Set to hide nested sections or pages at that level. Works only with file-tree menu mode
bookCollapseSection = true

# (Optional) Set true to hide page or section from side menu (if BookMenuBundle not set)
bookHidden = true

# (Optional) Set 'false' to hide ToC from page
bookToC = true

# (Optional) If you have enabled BookComments for the site, you can disable it for specific pages.
bookComments = true
```

### Partials

There are few empty partials you can override in `layouts/partials/`

| Partial                                            | Placement                              |
| -------------------------------------------------- | -------------------------------------- |
| `layouts/partials/docs/inject/head.html`           | Before closing `<head>` tag            |
| `layouts/partials/docs/inject/body.html`           | Before closing `<body>` tag            |
| `layouts/partials/docs/inject/footer.html`         | After page footer content              |
| `layouts/partials/docs/inject/menu-before.html`    | At the beginning of `<nav>` menu block |
| `layouts/partials/docs/inject/menu-after.html`     | At the end of `<nav>` menu block       |
| `layouts/partials/docs/inject/content-before.html` | Before page content                    |
| `layouts/partials/docs/inject/content-after.html`  | After page content                     |

### Extra Customisation

| File                     | Description                                                                           |
| ------------------------ | ------------------------------------------------------------------------------------- |
| `static/favicon.png`     | Override default favicon                                                              |
| `assets/_custom.scss`    | Customise or override scss styles                                                     |
| `assets/_variables.scss` | Override default SCSS variables                                                       |
| `assets/_fonts.scss`     | Replace default font with custom fonts (e.g. local files or remote like google fonts) |

### Plugins

There are few features implemented as plugable `scss` styles. Usually this are features that doesn't make it to the core but still might be useful.

| Plugin                            | Description                                                 |
| --------------------------------- | ----------------------------------------------------------- |
| `assets/plugins/_dark.scss`       | Switches site to dark mode                                  |
| `assets/plugins/_numbered.scss`   | Makes headings in markdown numbered, e.g. `1.1`, `1.2`      |
| `assets/plugins/_scrollbars.scss` | Overrides scrollbar styles to look similar across platforms |

To enable plugin add `@import "plugins/{name}";` to `assets/_custom.scss` in your website root. Exception is `_dark.scss` which contains only variables and should be added to `assets/_variables.scss`.

### Hugo Internal Templates

There are few hugo tempaltes inserted in `<head>`

- [Google Analytics](https://gohugo.io/templates/internal/#google-analytics)
- [Open Graph](https://gohugo.io/templates/internal/#open-graph)

## Shortcodes

 - [Buttons](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/buttons/)
 - [Columns](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/columns/)
 - [Expand](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/expand/)
 - [Hints](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/hints/)
 - [KaTeX](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/katex/)
 - [Mermaid](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/mermaid/)
 - [Tabs](https://themes.gohugo.io/theme/hugo-book/docs/shortcodes/tabs/)

## Versioning

Theme follows simple incremental versioning. e.g. `v1`, `v2` and so on. There might be breaking changes between versions.

If you want lower maintenance use one of released versions. If you want to live on the edge of changes you can use `master` branch and update your website when needed.

## Contributing

### [Extra credits to contributors](https://github.com/alex-shpak/hugo-book/graphs/contributors)

Contributions are welcome and I will review and consider pull requests.  
Primary goals are:

- Keep it simple.
- Keep minimal (or zero) default configuration.
- Avoid interference with user-defined layouts.
- Avoid using JS if it can be solved by CSS.

Feel free to open issue if you missing some configuration or customisation option.
